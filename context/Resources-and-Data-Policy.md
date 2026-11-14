# Resources and Data Policy

Inventory of the challenge resources, what each one is good for, and the rules for using data in the game. Complements [Requisitos-y-Criterios.md](Requisitos-y-Criterios.md) ("Use of NASA Data") and the root [references.md](../references.md).

Resources are **references and consultation tools**, not dependencies. Do not download or integrate everything by default: identify the concrete problem first, then consult only the right source.

> **Verification status:** the official Resources tab was unreachable (HTTP 502) when these links were collected, and Requisitos-y-Criterios.md notes the tab was empty when checked. Re-check the tab (resources were scheduled for Nov 13) and confirm each link before citing it. Links marked *unverified* have not been opened.

---

## 1. How to consult

1. Identify the need (mission-engineering question, rule design, orbit, visual model, educational reference, real data).
2. Pick the resource from the table in section 2.
3. Open the original source and check the link works and the content is relevant.
4. Extract only what you need: definition, rule, value, image, example.
5. Record provenance (URL, title, consultation date, which datum was used) — see section 5.
6. Separate facts from simplifications.
7. Avoid needless dependencies: if reading a PDF is enough, do not install a specialised tool.

| Need during development | Consult first |
|---|---|
| Full mission lifecycle and phases | Design and Develop Science Missions |
| Subsystems, mass/power/data estimates, trade studies | Mission Design Lab |
| How a mission concept matures (difficulty levels) | Concept Maturity Levels (CMLs) |
| Trajectories, maneuvers, orbits with more rigour | GMAT |
| Small-mission realism, phases, durations | CubeSat 101 |
| Educational game with science → design decisions | Build It Yourself (Webb telescope) |
| 3D visualisation of bodies and trajectories | NASA Mission Viz |
| Educational tone for younger audiences | CSA Digital Games and Activities |
| Previous visualisation challenge | Space Apps 2023 VR challenge |

## 2. Resource catalog

Nine resources are listed for the challenge: eight from NASA and one from the Canadian Space Agency (CSA). Priorities are for this hackathon.

| # | Resource | Link | Priority | Use in the game | Do not |
|---|---|---|---|---|---|
| 1 | **Design and Develop Science Missions** (NASA PDF, 25 pp.) | https://www.nasa.gov/wp-content/uploads/2025/04/250323-design-and-develop-science-mission.pdf | Very high | Mission cycle, not only a spacecraft configurator. Four segments: **Launch, Space, Ground, User**. Flow: objective → requirements → design → verification → operation → analysis. Data reception and use belong in the result. | Copy the real process as mandatory screens. |
| 2 | **Mission Design Lab (MDL)** — NASA Goddard | https://etd.gsfc.nasa.gov/capabilities/integrated-design-center/mission-design-lab/ | Very high | Choose subsystems and trade-offs; inspire the **team roles** (each player = a discipline) and the comparison screen. Study levels: Office Hours, Concept Development, Trade Study, Point Design. Disciplines: power, comms, propulsion, thermal, structures, avionics, attitude control, cost, risk. | Simulate every subsystem; keep only those that drive implemented mechanics. |
| 3 | **Build It Yourself** — NASA learning game on telescopes | https://science.nasa.gov/mission/webb/game-build-it-yourself/ | Very high (UX) | Science objective drives engineering; disabled options with a reason; 3 complexity levels; change choices until launch; result linked to real similar missions. | Copy its content or visual design. |
| 4 | **CubeSat 101** (NASA CSLI, 96 pp.) | https://www.nasa.gov/wp-content/uploads/2017/03/nasa_csli_cubesat_101_508.pdf (alt: https://www3.nasa.gov/sites/default/files/atoms/files/nasa_csli_cubesat_101_508.pdf) | High if the scenario is a CubeSat | Realistic small-mission scale, phases and durations (good source for the **time** resource). | Extrapolate CubeSat limits to larger or deep-space missions. |
| 5 | **Concept Maturity Levels (CMLs)** — JPL | https://dataverse.jpl.nasa.gov/dataset.xhtml?persistentId=hdl:2014/44299 (also https://ntrs.nasa.gov/citations/20150007816) | Medium | Inspire difficulty/progression: CML 1 idea → 2 feasibility → 3 trade space → 4 point design. | Make the CML scale a mandatory mechanic. |
| 6 | **GMAT** — General Mission Analysis Tool | https://software.nasa.gov/software/GSC-19468-1 · https://github.com/nasa/GMAT | Medium (high only if orbits are modelled more rigorously) | The **physics engine of the project base** (Gmat-Web drives it through `gmatpy`); source of orbital values and cross-check of game formulas. | Replicate its physics in the frontend. See section 4. |
| 7 | **NASA Mission Viz** | https://nasa.github.io/mission-viz/ | Low–medium | Reference for showing spacecraft, bodies, trajectories and events visually. | Treat it as a library to embed. |
| 8 | **Space Apps 2023: Visualize a Space Mission Using VR** | https://www.spaceappschallenge.org/2023/challenges/visualize-a-space-mission-using-virtual-reality/ (*unverified*) | Low | Which mission components past teams considered essential to communicate. | Copy past projects or make VR a requirement. |
| 9 | **CSA Digital Games and Activities** | https://www.asc-csa.gc.ca/eng/youth-educators/digital-games-and-activities.asp | Low–medium | Tone and format for accessible, short educational activities. | Use it as a component database. |

### Additional sources (not part of the official nine — do not present them as such)

| Source | Link | Use | Caution |
|---|---|---|---|
| NASA Technical Reports Server (NTRS) | https://ntrs.nasa.gov/ (API: https://ntrs.nasa.gov/api/citations/search) | Published mass, power, instrument, cost data to justify game values | Costs/masses use different assumptions across documents; record context and unit. |
| NASA Image and Video Library | https://images.nasa.gov/ (API: https://images-api.nasa.gov/search) | Briefing and info-screen imagery | Check credit and usage terms per asset. |
| NASA 3D Resources | https://github.com/nasa/NASA-3D-Resources | Recognisable 3D models if needed | Check format, scale, polygon count, license; never let model hunting delay the logic. |

Further candidate NASA sources for real values (rocket payload by orbit, real spacecraft mass/power, Deep Space Network) are listed in Requisitos-y-Criterios.md.

## 3. What to consult for each part of the game

| Part | Consult | Questions to settle |
|---|---|---|
| Objectives and requirements | Design and Develop Science Missions · Build It Yourself · CMLs | What result does the mission seek? Which measurements? Which instrument gets them? What makes the design viable? |
| Spacecraft and subsystems | MDL · CubeSat 101 (if CubeSat) · NTRS | Which subsystems are essential here? Attributes of each component? Effect on mass, power, data, cost, risk? |
| Launcher and orbit | MDL · GMAT (concepts) · NTRS | Which orbit serves the objective? What limits does the launcher impose? Which simplifications does the game assume? |
| Communications and data | MDL · Design and Develop Science Missions · NTRS | How much data does an instrument produce? How much can be stored/transmitted? How does data loss affect the science result? |
| UI and educational experience | Build It Yourself · Mission Viz · CSA | What does the player need to know at each step? How is an incompatibility explained? What is shown visually vs as data? |

Suggested order for the hackathon: (1) Design and Develop Science Missions for the flow, (2) MDL for subsystems and trade-offs, (3) Build It Yourself for progression and feedback, (4) CubeSat 101 only if the scenario is a CubeSat, (5) GMAT / NTRS only to justify an orbital mechanic or real datum, (6) Mission Viz / 3D Resources / Image Library after the loop works.

## 4. GMAT: how it is used here

- The project base, **Gmat-Web** ([Base-Gmat-Web.md](Base-Gmat-Web.md)), runs the real GMAT **R2026a** engine (`gmatpy`) behind its backend. GMAT is therefore a runtime dependency of the base, and a genuine use of a NASA tool in the mechanics (Relevance criterion).
- Neither GMAT nor Gmat-Web is stored in this repository. GMAT is installed separately (the compiled `gmat-win-R2026a` / Ubuntu build, pointed to by `GMAT_HOME`). A GMAT *source* checkout is not enough to run it and is not needed.
- Use in the game: obtain orbital values (orbital period, Hohmann Δv, eclipse fraction → power, ground-station contact time → data downlink). Reference scripts shipped with GMAT: `Ex_HohmannTransfer`, `Ex_EclipseLocation`, `Ex_Contact_Location_Station_Mask`, `Ex_LEOStationKeeping`, `Ex_GEOTransfer`. The eclipse/contact examples use GMAT's event-locator plugin, which Gmat-Web lists as an optional phase: verify it works before relying on it.
- A value obtained from GMAT is tagged `real` only when the script, GMAT version and inputs are recorded; otherwise `game`.
- Never re-implement GMAT's physics in the frontend. If the game simplifies orbits anywhere, say so in the UI and report: "educational approximations".
- Attribution: GMAT is Apache 2.0; keep the `NOTICE` from Gmat-Web, and do not use NASA logos or marks.

## 5. Data policy

1. Prefer primary sources: NASA, JPL, CSA (and other partner agencies).
2. **Never invent figures and attribute them to NASA.** If no reliable value exists, create a game-balance parameter and mark it `game`.
3. Every number carries an explicit unit: kg, W, Wh, bit/s, MB, km, days, USD or game credits.
4. Do not mix magnitudes: power (W) ≠ energy (Wh); data rate (bit/s) ≠ data volume (MB).
5. State assumptions (e.g. "communication windows are summarised as total capacity per day").
6. Keep internal consistency: mass, power, data, comms and budget must relate coherently even in a simplified model.
7. Do not treat educational resources as technical specifications: the telescope game inspires UX; it is not a source for spacecraft power values.
8. External software is integrated only where the base already does it (GMAT via the Gmat-Web backend); do not add other engines or services without a clear need.
9. Respect attribution and licenses for any model, image, audio or code.
10. Keep a source register: every real datum goes into `references.md` and the form fields **NASA Data** and **Space Agency Partner Data and Other References**.
11. NASA data must **feed the mechanics** (components, rockets, orbits) — not only appear as a link. This is half of the Relevance score.

### Real vs game values

Every number in the catalog is tagged:

- `real` — taken from a cited source (URL + location).
- `game` — hand-balanced for gameplay, shown to the player as a "simplified simulation value", never as a real hardware spec.

### Recommended record format

```text
Datum:             reference mass of the subsystem
Value:             2.5
Unit:              kg
Mission/component: [name]
Source:            [direct URL to the document]
Location:          [page, table or section]
Consulted on:      YYYY-MM-DD
Use in the game:   [parameter / comparison / validation]
Type:              published datum / estimate / game-balance value
Assumptions:       [if any]
```

## 6. Instructions for AI coding assistants

- Treat this file as an index, not an order to download everything.
- Before integrating a resource, state what problem it solves and what it costs.
- Prefer reading a page or PDF over installing a heavy tool.
- GMAT comes through the Gmat-Web base. Do not add external APIs, databases or other third-party services without a clear need approved by the hackathon scope.
- If a source is unavailable, do not invent its content: report the limitation and find another reliable source, or ask the team for the text/PDF.
- Keep reference data and game-balance values separate.
- Keep the source link and attribution for any asset derived from NASA/CSA material.
- Do not block development on research that does not affect the prototype: use a documented approximation and move on.

**Do not sacrifice the working prototype chasing engineering fidelity that cannot be implemented and validated in two days.**
