# Prompts Log — Salon Queue Management System

**Live App:** https://curious-kitsune-b15732.netlify.app/

Below is the chronological log of every prompt used during the design, build, debugging, and deployment phases—including prompts that needed refinement.

---

## Prompt 1 — Initial Attempt (Too Broad / Did Not Work Well)
> Make a salon queue management app with customer booking, reception dashboard, barber screen, TV screen, and owner admin panel in React.

* **Outcome:** Did not work as intended. Without structured specifications, the agent invented generic layouts, omitted Gujarati translations, and mixed queue logic directly into UI components. Following the Vibe Coding Lab guide, I discarded this approach and created `AGENTS.md` and `docs/` (`01-brief.md`, `02-screens.md`, `03-flows-rules.md`) first.

---

## Prompt 2 — Specification Analysis & Project Scaffolding
> Read `AGENTS.md` and all files in `docs/`. Summarize the app in 8 bullets and confirm all queue rules without writing code yet. Then set up a React + Vite + Tailwind CSS project with routes for all 7 screens (`/`, `/join`, `/status/:id`, `/reception`, `/barber/:name`, `/display`, `/admin`), the dark charcoal (`#1F2937`) and gold (`#D4A017`) theme, and an English/Gujarati (`EN`/`GU`) toggle.

* **Outcome:** Worked cleanly. Produced the project skeleton, theme colors, routing structure, and centralized bilingual dictionary (`src/lib/i18n.js`).

---

## Prompt 3 — Core Queue Engine & Cross-Tab Real-Time Sync
> Implement `src/lib/queueEngine.js` strictly following `docs/03-flows-rules.md`. Include forward-only status transitions (`Waiting -> Called -> In chair -> Done`, `No-show`, `Cancelled`), FIFO + barber-preference `Call next` matching, the dynamic wait-time formula (`totalMinutesAhead / activeBarbers`), one-active-spot-per-phone validation, and realistic Indian salon seed data (barbers Ravi, Amit, Imran). Sync state across phone, tablet, and TV browser tabs in under 1 second using `localStorage` + `BroadcastChannel`.

* **Outcome:** Worked. Kept all queue rules in a single source of truth and enabled real-time multi-window updates without requiring a separate backend server.

---

## Prompt 4 — Customer Screens (`Home`, `Join Queue`, `My Status`)
> Build Screen 1 (`/`), Screen 2 (`/join`), and Screen 3 (`/status/:id`) as specified in `docs/02-screens.md`. Enforce 10-digit Indian mobile number validation and a maximum limit of 3 services per booking. On `/status/:id`, build the circular wait countdown, the amber `"Start coming to the salon"` alert when 2nd in line, and a full-screen pulsing gold `"It's your turn!"` screen with device vibration when status becomes `Called`.

* **Outcome:** Worked. Verified live price/duration totals on `/join` and duplicate-phone redirection to existing tokens.

---

## Prompt 5 — Bug Fix: Barber Preference & Estimated Wait Calculation
> Bug: When Customer A selects `Ravi` and Customer B selects `Any`, clicking `Call next` for `Amit` should skip Customer A and call Customer B. Also verify that when `Imran` is toggled `On break`, the active barber divisor decreases so estimated wait times recalculate immediately. Explain the cause first, then fix `src/lib/queueEngine.js` without changing the UI.

* **Outcome:** Fixed. Confirmed `findNextCustomerForBarber` filters by `(preferredBarber === 'Any' || preferredBarber === barberName)` and `getActiveBarbersCount` excludes barbers on break.

---

## Prompt 6 — Staff Screens (`Reception` & `Barber View`) + PIN Gate
> Build Screen 4 (`/reception`) for a 10-inch landscape tablet and Screen 5 (`/barber/:name`) per `docs/02-screens.md`. Include barber station cards with progress bars and `[Call next]`, a waiting list highlighting waits over 60 minutes in amber, a `[+ Add walk-in]` modal, `[Start]` / `[Done]` chair timers on Barber View, and a staff PIN gate (`1234`) with a 1-tap demo unlock button.

* **Outcome:** Worked. Tested walk-in additions, no-show handling, and live chair timers across separate windows.

---

## Prompt 7 — Waiting Area TV (`/display`) & Owner Settings (`/admin`)
> Build Screen 6 (`/display`) with high-contrast typography readable from 5 metres, `NOW SERVING` chair cards, `UP NEXT` top-5 list, gold flash animation, and a Web Audio API chime when a token is called. Build Screen 7 (`/admin`) with daily KPI cards, master `Online Queue Open/Closed` toggle, 30-minute pre-closing online cutoff, barber duty switches, and bilingual service catalog controls.

* **Outcome:** Worked. Verified that toggling a service off in `/admin` immediately hides it from `/join`.

---

## Prompt 8 — Checklist Verification & Production Deployment
> Go through every item in the test checklist in `docs/03-flows-rules.md`, fix any Gujarati text overflow on mobile viewports, and configure SPA fallback routing so refreshing `/reception` or `/display` on Netlify/Vercel never returns a 404 error.

* **Outcome:** Passed all 10 checklist items and deployed live to `https://curious-kitsune-b15732.netlify.app/`.