# Development Brief — Space Mission Design Game

Working document for whoever builds the game (team members or AI coding assistants).
It turns the challenge ([Space-Mission-Design-Game.md](Space-Mission-Design-Game.md)), the team idea ([Idea-y-Objetivo.md](Idea-y-Objetivo.md)) and the submission rules ([Requisitos-y-Criterios.md](Requisitos-y-Criterios.md)) into concrete build requirements.

- **Constraint:** working prototype for a 2-day hackathon (Nov 14–15, 2026). Submission closes **Sunday, Nov 15, 11:59 p.m.**
- **Priority:** show, clearly and playably, how design decisions change the outcome of a space mission.
- **Base code:** the game is built on top of **Gmat-Web** (a web port of NASA GMAT), which lives in its own repository. See [Base-Gmat-Web.md](Base-Gmat-Web.md) for what it provides, what it lacks, and how it constrains the architecture.
- **Status of open decisions:** scenarios and multiplayer level are still listed under *Pending Team Decisions* in [Idea-y-Objetivo.md](Idea-y-Objetivo.md). This brief does not decide them; where it needs a default it says so.
- **AI disclosure:** this document was drafted with AI assistance (Claude Code) from the team's research notes. Declare it in the SI field and in the project README (see Requisitos-y-Criterios.md, "Rules on AI Use").

---

## 1. What the prototype must demonstrate

The experience must not be "pick parts, watch a launch animation". The core is that choices have **understandable, consistent and visible consequences**.

At minimum the player can:

1. Receive or select a mission objective.
2. Configure a spacecraft and payload through meaningful decisions.
3. Choose a launch vehicle and an orbit that are compatible with the mission.
4. Manage limited resources and constraints.
5. Validate the design before launch.
6. Run a simplified simulation.
7. Get a result that explains what worked, what failed and why.

There is not necessarily one perfect configuration: a decision that improves one indicator can hurt another. This maps to the MVP table in Idea-y-Objetivo.md (visible resources, consequences, validation, simulation, final report, replayable, simple explanations).

## 2. Domain elements the game must represent

| Element | Represents | Consequence to show |
|---|---|---|
| Science objective | What the mission wants to achieve | Determines which instruments, orbit and capabilities are useful |
| Spacecraft / bus | Platform hosting the subsystems | Has mass, cost, electrical capacity and payload capacity |
| Instruments | Equipment that collects data | More science value, but more mass, power, cost and data |
| Launch vehicle | Rocket that delivers the craft | Cost, maximum payload mass, orbit restrictions |
| Orbit | Where the craft operates | Affects science usefulness, communication windows, eclipse/operating conditions |
| Mass | Total mass the launcher must carry | Must not exceed launcher capacity |
| Power | Ability to run the systems | Demand must not exceed generation/availability |
| Budget | Money for development and operations | Total cost must stay within the limit |
| Data | Information produced by instruments | Must be transmitted or stored within capacity |
| Communications | Ability to send data to ground | Insufficient capacity reduces data received |
| Time / lifetime | Planned mission duration | Power, operating budget and design must sustain it |

Real aerospace fidelity is **not** required. Rules must be coherent and the game must state its simplifications (see "Real vs game values" in [Resources-and-Data-Policy.md](Resources-and-Data-Policy.md)).

## 3. Cause–effect rules (core of the game)

- **Add instruments** → more science value, but more mass, cost, power and data.
- **More capable rocket** → carries more mass or reaches more orbits, but costs more.
- **Choose an orbit** → can favour one objective and hurt another; changes communication opportunities.
- **More power capacity** → run more instruments, but extra panels/batteries add mass and cost.
- **More data generated** → no more science if antenna, contact window or storage cannot get it down.
- **Longer lifetime** → more observation time, but higher power and operations needs.
- **Violating a critical constraint** → must raise a warning, block launch, or cause a consequence during simulation. Never ignore it silently.

### 3.1 Resources always visible while designing

Budget used/available · total mass / launcher capacity · power demand / available · data generated / downlink or storage capacity · planned duration · rocket–orbit compatibility · estimated science value or progress toward the objective.

Use bars, indicators and status messages — not only numbers on a technical screen.

### 3.2 Design validation before launch

Explicit checks:

- Cost within budget?
- Total mass fits the selected launcher?
- Available power covers demand?
- Can the launcher reach the selected orbit?
- Does communications capacity recover a useful amount of data?
- Does the configuration serve the chosen science objective?

Three severities:

| Level | Meaning | Example |
|---|---|---|
| **Blocking** | Cannot launch | Mass above launcher capacity |
| **Warning** | Can launch, but a risk or probable loss exists | Limited downlink capacity |
| **Tip** | Optional improvement that teaches an alternative | "A bigger antenna would recover the lost data" |

## 4. Game loop

Matches **Idea A — "Mission Control"** (recommended in Idea-y-Objetivo.md). A full match should take 5–10 minutes.

1. **Briefing** — objective, context, budget and constraints.
2. **Design** — pick spacecraft components, instruments, launcher and orbit.
3. **Review** — live indicators, incompatibilities and recommendations.
4. **Launch** — short visual transition.
5. **Operation / simulation** — compute mission performance from the configuration (random events optional, small and explained).
6. **Report** — success, science result, resources used, data recovered, causes of penalties or failure, other valid combinations.
7. **Retry** — back to design with no stale data from the previous run.

Minimum content (all values are **game values** unless sourced): 1 scenario with a concrete science objective (2–3 if time allows), 2–3 instruments, 2 launchers, 2–3 orbits, 2–3 power/subsystem options, budget and mass/power/data limits, deterministic simulation or a small explained random variation, final screen with breakdown.

Optional, only after the full loop works: more scenarios and difficulty levels, random events, sandbox, design comparison, save/share, leaderboard, local turn-based multiplayer with roles, up-to-4 cooperative play, detailed 3D / advanced orbit visuals.

## 5. Educational UX

- Plain language; introduce a concept at the moment a decision needs it.
- Explain *why* a choice affects other subsystems; never only "correct/incorrect".
- Before/after comparison when a component changes.
- Short intro or tutorial; state must be readable without aerospace background.
- Disabled options show the reason for the incompatibility (as in NASA's *Build It Yourself* telescope game).

Useful feedback:

> "The high-resolution instrument raises science value, but uses more power and produces more data. With the current antenna, part of the data cannot be transmitted."

Useless feedback: "Insufficient power."

## 6. Simulation model — simple, explicit, testable

Game formulas, not a physics engine. Coefficients and units are defined and balanced by the team.

```text
total_mass_kg   = bus + sum(instruments) + power_system + comms
total_cost      = bus + sum(instruments) + launcher + operations
power_demand_w  = bus + sum(instruments)
power_avail_w   = generated + usable_battery
data_generated  = sum(per-instrument data)
data_received   = min(data_generated, comms_capacity * contact_time)

mass_ok   = total_mass_kg <= launcher_capacity_kg
budget_ok = total_cost    <= budget
power_ok  = power_demand_w <= power_avail_w
```

Then derive the result from: critical-constraint compliance, instrument fit to the objective, data actually recovered, operating duration, risks/penalties.

Keep three layers **separate**:

1. **Eligibility rules** — can the mission launch?
2. **Performance** — how well does it meet the objective?
3. **Score** — summary for gameplay.

A mission can be launchable and still score low; that teaches "can launch" ≠ "good mission". The score must be transparent: the report shows which factors contributed. Normalise quantities before combining different units.

## 7. Architecture principles

The base is **Gmat-Web**: React + Vite + TypeScript frontend, FastAPI backend that drives the real GMAT engine (`gmatpy`) through worker processes. Details and gaps in [Base-Gmat-Web.md](Base-Gmat-Web.md). These rules apply on top of it:

- **Two kinds of numbers, two homes.**
  - *Orbital quantities* (period, Δv, eclipse, contact time, etc.) come from **GMAT through the backend**. Never re-implement propagation, maneuvers or conversions in the frontend (a hard rule inherited from Gmat-Web).
  - *Game quantities* (mass, power, cost, data, science value, score) are game formulas in the game layer.
- **Data-driven catalog** (instruments, buses, launchers, orbits, scenarios) in plain data files, not hard-coded in UI.
- **Pure domain logic** (calculator, validator, simulator, report builder) with no dependency on UI objects, so it can be unit-tested.
- **UI only renders** and sends selections; it never contains the main formulas. No button computes its own totals.
- Recompute indicators on every selection change; centralise formulas and limits.
- Explicit units in names (`massKg`, `costCredits`, `powerW`, `dataMBPerDay`).
- The game must not *depend* on a slow or fragile live GMAT call to be playable: prefer GMAT results precomputed into the catalog (tagged `real`), with live GMAT runs as an add-on. See "Proposed integration" in Base-Gmat-Web.md.
- No accounts or database (same as Gmat-Web v1). The game must run from a public link with no login (judging requirement).

Data flow:

```text
Catalog ──> MissionConfiguration <── UI selections
                    │
                    v
             MissionValidator ──> errors / warnings / tips
                    │
                    v
             MissionSimulator
                    │
                    v
              MissionReport ──> results screen
```

Stack: inherited from Gmat-Web (React 19, Vite, TypeScript, Zustand; FastAPI on Python 3.12–3.14; pytest for the backend). Game-layer logic should be plain TypeScript modules that can be unit-tested without the UI.

## 8. Acceptance criteria

- [ ] Player can start a mission and understand its objective.
- [ ] Player can select components and see their attributes.
- [ ] Mass, budget, power and data indicators update correctly.
- [ ] At least one invalid configuration is detected per critical constraint implemented.
- [ ] A configuration that violates a blocking rule cannot launch.
- [ ] A valid configuration simulates to the end.
- [ ] Changing a selection changes indicators/results coherently.
- [ ] Final report explains the result and its causes.
- [ ] Player can return to design and try another configuration.
- [ ] Completable without advanced space-engineering knowledge.

## 9. Minimum tests

1. **Valid design** — budget, mass and power within limits → can launch.
2. **Mass excess** — above launcher capacity → launch blocked.
3. **Budget excess** — above budget → blocked or redesign required.
4. **Power deficit** — demand above availability → warn or block per the defined rule.
5. **Insufficient comms** — more data than can be sent → mission continues, report shows data loss.
6. **Instrument incompatible with objective** — lower usefulness or a warning.
7. **Change launcher or orbit** — compatibility and limits update.
8. **Retry** — modified design produces a new result with no leftover data from the previous simulation.

## 10. Risks to avoid

- Only a selection screen, with no simulation behind the choices.
- Launch animation without consequences (decoration, not simulation).
- Too many features (multiplayer, realistic orbits, huge inventory, long narrative) leaving the core loop unfinished.
- Numbers with no explanation of what they mean.
- Impossible combinations allowed without feedback.
- Arbitrary scoring; the report must show where the result comes from.
- False scientific precision: never present invented parameters as real NASA data.
- Coupling formulas to the UI.
- Testing with one configuration only; test edge cases.

## 11. Two-day plan

Aligned with the submission deadline and the "demo person from day one" rule in Requisitos-y-Criterios.md.

### Day 1 (Sat, Nov 14) — playable end to end

1. Agree the scenario scope and pending decisions; get the base running locally (GMAT engine, backend, frontend — see Base-Gmat-Web.md).
2. Small catalog of components with attributes (tagged `real` or `game`).
3. Configuration model, validations and calculations.
4. Briefing and configuration UI, live indicators, configuration errors.
5. Test valid and invalid configurations.
6. Start the references list and the demo/project-page draft (do not leave for the end).

**Deliverable:** configure a mission, validate constraints, compute a basic result.

### Day 2 (Sun, Nov 15) — simulation, polish, submit (before 11:59 p.m.)

1. Launch and operation flow.
2. Final report explaining causes; educational feedback; UI polish.
3. Run the minimum tests, fix bugs.
4. Prepare a demo mission plus an alternative that fails for a visible reason.
5. Publish on an open link (needs the backend + GMAT build hosted, or a static fallback — see Base-Gmat-Web.md); verify in an incognito window.
6. Record the ≤30 s demo (or ≤7 slides), complete the form, submit.

## 12. Rules for anyone (or any AI assistant) coding on this project

1. Inspect the repo structure first; do not assume it is empty. Reuse what exists.
2. Do not build every optional feature. Priority: `complete playable loop > coherent rules > educational feedback > visual clarity > extra content > visual effects`.
3. If a design decision is missing, choose the simplest option that keeps the cause–effect relations, and write the assumption down.
4. Keep formulas in testable logic modules, not UI code; keep component data configurable.
5. Implement and test critical constraints before animations or effects.
6. Never invent real NASA data. Illustrative numbers are labelled game values.
7. No new dependencies, external services, database, accounts or multiplayer without justifying need and cost. (The FastAPI backend and GMAT engine already come with the base.)
8. Work in small runnable increments; check the project builds after each.
9. All user-facing text and all linked material in **English**. Gmat-Web's UI is Spanish (`frontend/src/i18n/es.ts`): the game screens need English text from the start.
10. Log every external library, image, dataset and generated asset in `references.md` from the first commit; mark AI-generated code, data, images and audio as the guide requires.
11. Game and design ideation belongs to the team. AI helps implement and document; it should not be the source of the solution concept.
12. When done, report what was implemented, how to run it, what was tested and known limitations.
