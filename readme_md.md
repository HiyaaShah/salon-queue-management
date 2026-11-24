# Salon Queue Management System

**Live demo:** https://curious-kitsune-b15732.netlify.app/
**Hosted on:** Netlify (Frontend SPA with real-time cross-tab BroadcastChannel + localStorage sync)

## About
A bilingual (**English & Gujarati**) real-time Salon Queue Management System built following the Vibe Coding specification (`AGENTS.md` + `docs/`). Customers can join the queue remotely from their mobile phone, monitor their live position and wait time, and receive an instant full-screen gold alert when called—while receptionists, barbers, owners, and the waiting-room TV stay synchronized in real time.

## Screens Included
1. **Home (`/`)** — Live wait summary, barber status chips, queue open/closed status, and quick token lookup.
2. **Join Queue (`/join`)** — Mobile-first booking with 10-digit phone validation, up to 3 services, barber preference (`Any` or specific barber), and live cost/wait estimator.
3. **My Status (`/status/:id`)** — Live position tracker, `"Start coming"` alert at #2, and full-screen pulsing gold `"It's your turn!"` takeover + vibration.
4. **Reception Dashboard (`/reception`)** — Tablet-optimized chair management (`[Call next]`), walk-in registration modal, amber >60m wait alerts, and no-show/cancel controls.
5. **Barber View (`/barber/:name`)** — Per-barber station screen with `[Start]` / `[Done]` workflow, running timer, next-in-line preview, and `On break` toggle.
6. **Waiting Area TV (`/display`)** — High-contrast 5-metre TV display with `NOW SERVING` chairs, `UP NEXT` top 5 tokens, gold call flash, and Web Audio chime.
7. **Owner Settings (`/admin`)** — Daily KPI metrics, master Online Queue Open/Closed toggle, barber duty switches, and bilingual service catalog editor.

## Quick Local Setup
```bash
npm install
npm run dev
```
