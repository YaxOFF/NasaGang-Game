# Project Base — Gmat-Web

The game is built on **Gmat-Web**, a web port of NASA's General Mission Analysis Tool (GMAT). It lives in its **own repository**, separate from this one:

- Base repo: https://github.com/YaxOFF/Gmat-Web (branch `main`)
- This repo (`NasaGang-Game`): context, documentation and submission material.
- Neither GMAT nor Gmat-Web is copied into this repository.

> Snapshot taken on Nov 14, 2026 (Gmat-Web commit `1927530`). Gmat-Web moves fast; its `PLAN.md` ("Avance") and `docs/` are the source of truth for its current state.

## 1. What Gmat-Web is

A web app to design space missions and run them with the **real GMAT engine**: create spacecraft, propagators, maneuvers and mission sequences, run them, and see results. Results match desktop GMAT because the calculation is done by GMAT itself (`gmatpy`), not reimplemented.

| Piece | Where | Stack |
|---|---|---|
| Frontend | `frontend/` | React 19 + Vite + TypeScript + Zustand; Monaco script editor; (planned) CesiumJS 3D and uPlot charts |
| Backend API | `backend/` | FastAPI, Python 3.12–3.14 |
| GMAT engine | `GMAT_HOME` (outside the repo) | `gmatpy` R2026a, only inside spawned worker processes |
| Mission model | `shared/mission.schema.json` | JSON ↔ GMAT `.script` parser/serializer (the `.script` is the source of truth) |

License: MIT for Gmat-Web code; GMAT is Apache 2.0 (attribution in its `NOTICE`). Not affiliated with or endorsed by NASA or the GMAT authors.

### Progress (from its PLAN.md)

Done: skeleton, running scripts with live log, script ↔ model parser/serializer (round-trip tested on the 162 GMAT samples), engine-derived field schemas, resource tree with generic forms.
Pending: dedicated editors (Spacecraft/ForceModel/Propagator), mission-sequence editor, **results views (3D, ground track, charts)**, live solvers, UX/templates, **Docker deploy**, E2E tests, optional plugins.

## 2. Hard constraints inherited from the base

- Physics comes from GMAT. Never reimplement propagation, maneuvers or conversions in the frontend.
- The FastAPI process never imports `gmatpy`; everything touching the engine goes through worker processes (the engine is a process-wide singleton).
- Every script goes through `sanitize` before running: no Python/MATLAB/system calls, output paths rewritten to the run's temp folder.
- Opening/saving `.script` must stay compatible with desktop GMAT; the parser never drops lines.
- No NASA logos or branding.

## 3. Running the base locally

Requirements (from its README): the **compiled GMAT R2026a** (not just source) with `GMAT_HOME` pointing at its root (the folder containing `bin/gmatpy`); Python 3.12–3.14 matching a `bin/gmatpy/_pyXY` folder, and `uv`; Node.js 20+.

```text
set GMAT_HOME to the GMAT R2026a folder
./dev.ps1        (Windows)   or   GMAT_HOME=... ./dev.sh
backend  → http://127.0.0.1:8000     frontend → http://localhost:5173
```

## 4. Gaps between the base and the challenge

The base is an engineering tool for people who already know GMAT. The challenge asks for a beginner-friendly game. These gaps decide the work.

| # | Gap | Why it matters | Notes |
|---|---|---|---|
| 1 | **No game layer.** No catalog of buses/instruments/launchers, no resource bars, no validator, no score, no report. | This *is* the challenge. | See Development-Brief.md. Build as a separate module, not inside the GMAT editor. |
| 2 | **UI is Spanish only** (`frontend/src/i18n/es.ts`). | Everything linked in the submission must be in English. | Add an English locale; game screens in English from the start. |
| 3 | **Audience mismatch.** Expert tool with a script editor and generic forms. | Challenge targets beginners/youth; a match should take 5–10 min. | Game flow must hide GMAT complexity (the base's Phase 8 "templates" is related). |
| 4 | **No public deployment yet.** Needs backend + GMAT build running on a server (its Docker phase is not done). Static hosting (e.g. GitHub Pages) cannot run it. | Judging needs a public link with no login/permission. | Decide early: host the backend, or ship a static fallback. See section 5. |
| 5 | **Live runs can be slow or fail.** About 70 of 88 root samples ran clean at last check; runs have timeouts; some features need plugins (event locators) that the base lists as optional. | A demo that hangs is fatal. | Precompute and cache GMAT outputs; do not make gameplay depend on a live call. |
| 6 | **Results views are not built yet** (3D, ground track, charts). | Nice for storytelling, not required for the MVP. | Do not block the core loop on them. |
| 7 | **Two repositories.** | Judges look at one "Link to Final Project". | Team decision, see section 6. |

## 5. Proposed integration (proposal for the team — not decided)

Idea generation and design choices belong to the team (AI-use rules in Requisitos-y-Criterios.md). This is only a starting option.

1. **Game layer as its own module** in the frontend (catalog JSON, pure TypeScript calculator/validator/simulator/report), independent from the GMAT editor screens.
2. **Use GMAT where it earns its place:** run a small set of GMAT scripts (for the 2–3 orbits and the scenario) to get real orbital values — period, Δv, eclipse fraction, contact time — and store them in the catalog tagged `real`, with script, GMAT version and inputs recorded.
3. **Two modes:** the game runs from the precomputed catalog (works anywhere, including static hosting); an optional "verify with GMAT" action calls the backend live when it is available. This makes the demo robust and still keeps NASA's tool central to the mechanics.
4. **English locale** and a beginner flow (briefing → design → review → launch → report) wrapped around, not inside, the GMAT editor.

| Game quantity | Where it comes from |
|---|---|
| Orbital period, Δv to reach/transfer between orbits | GMAT (e.g. `Ex_HohmannTransfer`-style script) |
| Eclipse fraction → power/battery sizing | GMAT eclipse locator (verify plugin works) |
| Contact time per day → data downlink | GMAT contact locator (verify plugin works) |
| Mass, cost, instrument data and science value, budget, score | Game values (`game`) or cited NASA sources (`real`) |

## 6. Open decisions

- [ ] **Where does the game code live?** (a) inside the Gmat-Web repo (branch/fork) with this repo kept for docs and submission, or (b) the base is copied into this repo. Affects the "Link to Final Project".
- [ ] **How is it published?** Host the backend + GMAT, or static precomputed build, or both.
- [ ] **Who gets the GMAT engine set up locally** and keeps one working shared environment for the team.
- [ ] **Scenario and multiplayer level** (still open in Idea-y-Objetivo.md).
