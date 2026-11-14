# Team Idea and Goal — Space Mission Design Game

Team working document. The full challenge is in [Space-Mission-Design-Game.md](Space-Mission-Design-Game.md).

## Main Idea (in one sentence)

A game where you build a space mission with limited resources, launch it, and the game shows you **why** it succeeded or failed.

What NASA wants to see is not a realistic simulator. They want the player to feel the **trade-offs**: every decision that improves one thing makes something else worse.

> Example: I add a better camera → more science, but more mass, more power, more data, and higher cost → now I need a bigger rocket and I can no longer afford the budget.

## Our Goal

Deliver a game that is **playable from start to finish** in the browser, where a full match lasts 5 to 10 minutes:

1. Choose a mission (objective).
2. Design the spacecraft (components and instruments).
3. Choose orbit and rocket.
4. Simulate the mission.
5. View a report explaining the result and giving a score.

If those 5 stages work and are understandable without explanation, we meet the challenge. Everything else is extra.

## Must-Haves (MVP)

| Piece | What it means in practice |
|---|---|
| Visible resources | Bars always on screen: mass, power, budget, data, communications, time |
| Decisions with consequences | Each component has numbers (mass, power, cost, data, science value) that move the bars |
| Validation | The rocket must be able to carry the mass and reach the chosen orbit. If not, the game says so and explains why |
| Simulation | Upon launch, the mission progresses through stages and can fail (out of power, data that doesn't get transmitted in time, etc.) |
| Final report | Score + explanation in simple language: what went well, what failed, and what to change |
| Replayable | Button to go back to design, adjust, and simulate again |
| Simple explanations | Short tooltips for each concept (orbit, payload, data rate). The challenge level includes beginners and youth |

## What the Challenge Asks Regarding Multiplayer

The challenge mentions teams of up to 4 players, but says "you may consider". It is not mandatory. It is the most expensive thing to build, so there are three possible levels:

1. **Single player** with all 4 roles. The safest option.
2. **Local turn-based multiplayer** (same screen): each player takes a role and has their own share of the budget. Cheap to make and already counts as collaboration.
3. **Real-time online multiplayer** (rooms, WebSockets). Only if there is time to spare.

Recommendation: build level 1 with roles in mind, and move up to level 2 once the base game is finished.

## Game Ideas (choose one)

### Idea A — "Mission Control" (recommended)

Step-by-step mission builder with a resource dashboard and stage-by-stage simulation.

- Flow: mission → spacecraft → orbit → rocket → simulation → report.
- During the simulation, random events occur (solar storm, antenna failure) that test the margins you left.
- Why: covers almost all points of the challenge, is easy to explain in a demo video, and can be built in parts.

### Idea B — "Mission Cards"

Card game: each component, orbit, and rocket is a card with costs. You build a mission deck within limits.

- Why: very visual and easy to understand for youth. The 4-player mode comes naturally (everyone holds a hand of cards for their role).
- Risk: can feel less like "engineering" if the numbers are hidden too much.

### Idea C — "The Mission Board" (negotiation)

Four roles (science, engineering, communications, finance), each with their own conflicting goals. Players must negotiate a design that everyone approves.

- Why: directly tackles the collaboration and negotiation part of the challenge, which few teams will do well.
- Risk: relies on multiplayer. Without 4 people playing, it loses its appeal.

### Idea D — "Sandbox with Challenges"

Free builder with a spacecraft visualization that changes based on what you add, plus a list of challenges (cheapest mission, most science per kilo).

- Why: the most visually striking.
- Risk: the visual part consumes a lot of time and the educational part remains weak.

**Proposal:** use Idea A as a base and borrow the roles with conflicting goals from Idea C for the team mode.

## Possible Mission Scenarios

2 or 3 are enough. Each one makes a different resource critical:

| Mission | Typical Orbit | Critical Resource |
|---|---|---|
| Earth Observation (wildfires, weather) | Low (LEO) / polar | Data and communications |
| Communications Satellite | Geostationary (GEO) | Mass and launch cost |
| Moon or Mars Probe | Deep space | Power, communications, and time |
| Student CubeSat | LEO | Budget and mass (easy mode) |

## What Can Set Us Apart

- **The report that explains why.** The challenge asks for this several times. A "you failed because the battery doesn't cover the orbit's eclipse" is worth more than pretty graphics.
- **More than one valid solution.** Show other combinations at the end that would have also completed the mission.
- **Data based on real missions.** Use approximate, simplified values of real rockets and instruments. It gives credibility with the judges.
- **Compare designs.** Save the result and compare it with the previous attempt or with other teams (ranking).

## What NOT to Do

- Real orbital physics. A table of orbits with their characteristics is enough.
- Detailed 3D models of the spacecraft.
- User accounts, login, or complex database.
- More than 3 scenarios before the first one is complete.

## Suggested Division of Labor

| Role | Responsibility |
|---|---|
| Game Design & Data | Table of components, orbits, and rockets with their numbers. Scoring rules |
| Logic / Simulation | Resource calculations, validations, simulation engine, and events |
| Interface | Screens, resource dashboard, visualization |
| Content & Presentation | Educational texts, final report, demo video, and project page |

## Pending Team Decisions

- [ ] Which idea do we choose (A, B, C, or D)?
- [ ] Which multiplayer level?
- [ ] What technology do we build it with?
- [ ] Which 2 or 3 mission scenarios?
- [ ] Check submission dates and judging criteria in the official guides (links in the other document).