# 🌙 Mission "Water on the Moon": Complete Design
*Mission Architect, NASA Space Apps 2026*
*Game Design Document (GDD) for the playable MVP mission. Contains no code; describes the entire flow, screen by screen and mechanic by mechanic.*

> **Numbers:** gameplay values for balancing. They will be replaced by those from `orbits.json` (GMAT) and real catalogs when ready. The logic does not change.

---

## INDEX
1. Summary and Player Fantasy
2. The Two Vehicles: Orbiter + Rover
3. Resources and Gauges
4. The Spacecraft as the Enemy (Stress System and Deck)
5. Roles, Actions, and Personal Missions
6. Complete Flow, Screen by Screen
   - 6.1 Title and Selection Screen
   - 6.2 Briefing (CML 1)
   - 6.3 Feasibility and Orbit (CML 2)
   - 6.4 Hangar (CML 3)
   - 6.5 Design Review (CML 4)
   - 6.6 Launch
   - 6.7 Cruise and Insertion
   - 6.8 Act I: Orbital Mapping
   - 6.9 Act II: Landing Site Selection
   - 6.10 Act III: Descent and Landing
   - 6.11 Act IV: The Rover Searches for Water
   - 6.12 Act V: Ending
   - 6.13 Post-Mission Report
7. Detailed Rover Mechanics
8. Complete Card Catalog
9. Narrative Events and Dialogues
10. Interface by Role
11. Endings
12. Scoring and Achievements
13. Educational Value and Connection to Real Missions
14. MVP Scope Cut

---

## 1. Summary and Player Fantasy

**Premise:** the team is a NASA project office. It designs, launches, and operates a two-part mission:
1. An **orbiter** that maps the lunar poles from above to find where ice might exist.
2. A **rover** that lands at the best site, enters the darkness of a crater, and **confirms water by drilling into the ground**.

**Fantasy:** "We are Mission Control. The Moon is unforgiving, the spacecraft is too, and every decision we make in design will haunt us until the very last day."

**Central scientific question:**
> Is there water ice in the permanently shadowed craters of the lunar south pole? How much is there, and how accessible is it for future human missions (Artemis)?

**Playthrough duration:** 45–60 minutes.

**Narrative arc:**
| Act | What the player does | Emotion |
|---|---|---|
| Design (CML 1–4) | Negotiates, cuts costs, builds the spacecraft | Strategic tension |
| Launch and Cruise | Sees if their design holds up | Nerves |
| I. Orbital Mapping | Searches for hydrogen "hotspots" | Exploration |
| II. Landing Site | Chooses where to send the rover | Gamble |
| III. Descent | 7 minutes of terror | Peak tension |
| IV. Rover in the Crater | Survives in the dark, drills | Survival + discovery |
| V. Ending | Final data, final sacrifice | Emotional climax |

---

## 2. The Two Vehicles

### 2.1 Orbiter "Selene"
- Orbits the Moon in a polar orbit.
- Carries the mapping instruments.
- **Acts as a communications relay for the rover:** inside the crater, the rover cannot see Earth, so it can only communicate through the orbiter when it passes overhead.
- Designed completely in the Hangar.

### 2.2 Rover "Buscador"
- Arrives on a separate or integrated landing module (lander).
- Runs on battery and solar panels. **Inside the crater there is no Sun**, so it survives solely on battery power and must exit to recharge.
- Equipped with a drill and spectrometer to confirm water.
- Designed in a special section of the Hangar ("Rover Bay").

### 2.3 Why Two Vehicles (Educational Justification)
- From orbit, you can see **where** water might be (hydrogen signature).
- Only on the surface can you **confirm** that it is ice and how much there is.
- This is how real missions work: LRO, LCROSS, VIPER.

---

## 3. Resources and Gauges

### 3.1 Global Resources (Controlled by the Director)
| Resource | Start | If it reaches 0 |
|---|---|---|
| **Budget** | $400M | Mission canceled |
| **Schedule** | 36 months of development | Each extra month in design = −1 operational cycle |
| **NASA Confidence** | 100% | Less than 30%: extended mission is not approved; less than 10%: cancellation |

### 3.2 Orbiter Resources
| Resource | Unit | Controlled by |
|---|---|---|
| Power generated | W | Systems |
| Battery | Wh and % | Systems |
| Temperature (avionics, battery, instruments) | °C | Systems |
| Fuel | kg and m/s of Δv | Systems/Director |
| Storage | Gb | Comms |
| Transmitted data | Gb | Comms |
| Science quality | % | Science |

### 3.3 Rover Resources
| Resource | Unit | Note |
|---|---|---|
| Battery | Wh | Inside the crater, it only drains |
| Internal temperature | °C | Below −40 °C, the electronics die |
| Distance traveled | m | To reach drilling sites |
| Wheel integrity | % | Rough terrain reduces it |
| Analyzed samples | number | Surface science |
| Drill | % life | Each drilling operation wears it down |

### 3.4 Spacecraft Stress
- A single gauge (0–100) for the entire system (orbiter + rover).
- Always visible at the top of the screen, with a color shifting from green to red.
- Details in Section 4.

---

## 4. The Spacecraft as the Enemy

### 4.1 Philosophy
The spacecraft is not evil; it is **physics**. Every design shortcut becomes a card in its deck. During operations, the spacecraft "plays" those cards. The player never feels the game is cheating, because **they built the deck themselves**.

### 4.2 Personification
- The spacecraft "speaks" via console-style telemetry messages: `[SELENE] TEMP BAT 2: -18°C ↓ ... WARNING`.
- When stress exceeds 60, messages become more frequent and the interface flickers.
- With stress greater than 85, the music changes and the warning **"SYSTEM IN CRITICAL STATE"** appears.

### 4.3 How the Deck is Built
1. **Base deck** (always): 4 generic minor cards (telemetry noise, pointing drift, etc.).
2. **Component cards:** every low-reliability part or major omission adds cards (see catalog, Section 8).
3. **Decision cards:** forcing the CML 4 review, choosing a low orbit without enough fuel, etc.
4. **Event cards:** some events add new cards mid-game (e.g., a micrometeoroid leaves "Damaged Panel").

In the Hangar, there is a **"Spacecraft Deck" panel** showing live how many cards it contains and of what type. This lets the player see the consequences while designing.

### 4.4 Draw per Cycle
| Stress | Cards per cycle | Tier |
|---|---|---|
| 0–29 🟢 | 1 | Minor |
| 30–59 🟡 | 1 | 50% minor, 50% major |
| 60–84 🟠 | 2 | Major |
| 85–100 🔴 | 2 | Major + 1 critical |

### 4.5 What Raises and Lowers Stress
**Raises:**
| Cause | Stress |
|---|---|
| Mass margin less than 10% | +10 (once, at launch) |
| Power margin less than 15% | +10 (once) |
| Each component with reliability less than 0.90 | +5 |
| Forcing the CML 4 review | +15 |
| Exploding timer | +5 |
| Orbiter battery less than 20% | +3 per cycle |
| Rover at critical temperature | +5 per cycle |
| Failing a critical roll | +5 |

**Lowers:**
| Cause | Stress |
|---|---|
| Iterating in CML 3 | −10 |
| Passing a difficult roll | −5 |
| Cycle with no alerts | −3 |
| "Full Diagnostics" action (Systems, 1 cycle with no science) | −10 |

### 4.6 Timers
Some cards do not deal immediate damage: they start a **timer** of 1 to 3 cycles. If not resolved in time, it explodes with a worse effect.
Example: "Battery overheating: 2 cycles". If Systems does not reduce the load, the battery permanently loses 30% capacity.
On screen, timers appear as red clocks over the affected subsystem on the spacecraft schematic.

### 4.7 Engineering Roll
`P(success) = base × component_reliability × (1 − stress/200) + bonuses`
- **Bonuses:** +10% if the role owning the subsystem uses its main action; +5% if another role "assists" with its minor action; +15% if the Director spends "Call the Experts" (1/act).
- **Outcomes:**
  - ≥ P: **success**.
  - Up to 15 points below: **partial success**, which resolves the issue but starts a timer.
  - Lower: **failure**.
- The roll is displayed with a "simulation" animation (a filling bar), **not a die**, to maintain the engineering tone.

---

## 5. Roles

### 5.1 Actions per Cycle
Each role has **1 main action + 1 minor action** per cycle. In 1-player mode, the player uses all of them.

#### 🎖️ Mission Director
| Action | Type | Effect |
|---|---|---|
| Approve Spending | Main | Releases $ for repairs, DSN windows, etc. |
| Authorize Risk | Main | Allows dangerous actions (e.g., entering the crater on low battery) |
| Call the Experts | Main (1/act) | +15% to a roll |
| Reschedule Timeline | Main | Changes the order of objectives |
| Press Release | Minor | +10% NASA confidence if an achievement occurred this cycle |
| Assist | Minor | +5% to another role's roll |

#### ⚡ Systems Engineer
| Action | Type | Effect |
|---|---|---|
| Redistribute Power | Main | Move watts between subsystems (sliders) |
| Repair | Main | Roll to resolve a card |
| Thermal Control | Main | Turn heaters and radiators on or off |
| Full Diagnostics | Main | −10 stress, no science this cycle |
| Orbital Maneuver | Main | Spend fuel (station-keeping, changing altitude) |
| Subsystem Safe Mode | Minor | Shuts down a subsystem to protect it |
| Assist | Minor | +5% |

#### 🔬 Science Specialist
| Action | Type | Effect |
|---|---|---|
| Select Target | Main | Which zone to map / what to do with the rover |
| Toggle Instruments | Main | Changes power consumption and generated data |
| Calibrate | Main | Roll; improves quality |
| Analyze Sample (rover) | Main | Process a drill core |
| Compress Data | Minor | +50% transmittable volume, −20% quality |
| Assist | Minor | +5% |

#### 📡 Communications Officer (Comms)
| Action | Type | Effect |
|---|---|---|
| Book DSN Window | Main | Secures a downlink window (Goldstone, Madrid, Canberra) |
| Prioritize Queue | Main | Decides which data downlinks first |
| Recovery Command | Main | Brings spacecraft out of safe mode / resolves software glitches |
| Rover Relay | Main | Schedules orbiter–rover contacts |
| Repoint Antenna | Minor | Roll; resolves "Weak Link" |
| Assist | Minor | +5% |

### 5.2 Personal Missions
Each role has **1 main mission + 1 optional secret mission** (only in 4-player mode; adds tension).

| Role | Main Mission | Secret Mission (Optional) |
|---|---|---|
| Director | **Within Budget:** finish with ≥ $30M | **Press Hero:** confidence ≥ 120% at the end |
| Systems | **Nobody Freezes:** orbiter battery never less than 20% and rover never less than −40 °C | **Zero Exploded Timers** |
| Science | **Confirm Water:** at least 1 drill core with confirmed ice | **Complete Map:** cover all 5 candidate craters from orbit |
| Comms | **Not a Single Bit Lost:** never fill storage to capacity | **Live Broadcast:** downlink the discovery data in real time |

---

## 6. Complete Flow, Screen by Screen

### 6.1 Title and Selection Screen
1. **Title** with the rotating Moon and logo.
2. **Mode:** 1 player / 2 players / 4 players (online).
3. **Role assignment:** each player chooses their character (avatar + role).
4. **Optional tutorial:** a short guided 3-cycle mission.
5. **"Start Mission" button**.

### 6.2 Briefing (CML 1, "Cocktail Napkin")
**Scene:** NASA boardroom. A program director (NPC) introduces the mission.

**NPC Dialogue (summary):**
> "Since 1998, Lunar Prospector detected hydrogen at the poles. In 2009, LCROSS crashed a rocket into Cabeus crater and we saw water vapor. But nobody has **touched** that ice. You are going to do it."

**Decision 1, the scientific question (Science chooses, everyone votes):**
| Option | What it requires | Reward |
|---|---|---|
| A. "Where is there hydrogen?" | Orbiter only, no rover | Easy, score ×1 |
| B. "Is it really ice?" | Orbiter + rover with drill | Normal, ×2 **(recommended)** |
| C. "How much ice is there and at what depth?" | Orbiter + rover + deep drill + radar | Hard, ×3 |

*In the MVP, B is played by default; A and C remain as difficulty variants.*

**Screen output:** the "napkin". A hand-drawn animated sketch summarizing the chosen mission: a circle for the Moon, an orbit, and a rover. It is saved and appears in the final report.

### 6.3 Feasibility and Orbit (CML 2, "Initial Feasibility")
**Scene:** whiteboard with calculations. The game displays numbers visually, without intimidating formulas.

**Decision 2, the orbiter's orbit (Comms and Systems report, Director approves):**
| Orbit | Map Resolution | Eclipse | Rover Contacts | Insertion Δv | Station-Keeping Fuel | Note |
|---|---|---|---|---|---|---|
| Low Polar (50 km) | Excellent (×1.5) | 47 min of 113 | Short and frequent (6/day) | 900 m/s | High (decays on its own) | Needs the large tank |
| High Polar (100 km) | Good (×1.0) | 45 min of 118 | Medium (5/day) | 850 m/s | Medium | Balanced |
| Elliptical Polar (100 × 3000 km) | Variable | Short | **Long over the south pole** | 600 m/s | Low | Ideal for relay, worse for mapping |

**Decision 3, general landing site (preliminary):**
- Rim of Shackleton crater, rim of Cabeus, or Haworth. Can change in Act II.

**Automatic feasibility calculations (screen):**
- Estimated mass vs. available launch vehicles.
- Estimated power vs. eclipses.
- Estimated cost vs. budget.
- Traffic light: 🟢 viable / 🟡 tight / 🔴 unviable.

If 🔴 comes up, the game forces changing the question or the orbit. This teaches what "feasibility" means.

### 6.4 Hangar (CML 3, "Trade Space")
**The main design screen.** Three zones:
1. **Left:** component catalog in cards.
2. **Center:** 2D schematic of the spacecraft (orbiter on top, rover and lander below) with slots.
3. **Right:** live bars for mass, power, cost, and reliability + the **"Spacecraft Deck" panel**.

**Negotiation mechanic:** each role has **"requests"** marked in the catalog (a star in their color). If a request is left out, that role's personal mission becomes harder and the game notifies them.

#### 6.4.1 Orbiter Catalog
| Category | Component | Mass kg | W | $M | Rel. | Card added / note |
|---|---|---|---|---|---|---|
| **Bus** | Small Bus | 80 | 15 | 25 | 0.95 | Max 4 instrument slots |
| | Medium Bus | 140 | 20 | 40 | 0.97 | Max 6 slots |
| **Power** | GaAs Panel 400 W | 25 | +400 | 15 | 0.97 | — |
| | Si Panel 250 W | 30 | +250 | 6 | 0.88 | Cell Degradation |
| | Battery 1 kWh | 8 | — | 4 | 0.95 | — |
| | Battery 2 kWh | 15 | — | 7 | 0.95 | — |
| **Thermal** | Battery Heaters | 2 | 30 | 1 | 0.98 | Without them: Cold Battery |
| | Standard Radiator | 6 | — | 2 | — | — |
| | Premium MLI Blankets | 4 | — | 3 | — | −1 thermal card |
| **Comms** | Low-Gain Antenna | 3 | 15 | 2 | 0.98 | Weak Link; downlink 2 Gb/window |
| | High-Gain Antenna | 18 | 40 | 10 | 0.94 | Jammed Antenna; downlink 10 Gb/window |
| | UHF Relay Radio (for the rover) | 4 | 10 | 5 | 0.96 | **Mandatory if there is a rover** |
| **Data** | 64 Gb Recorder | 3 | 5 | 2 | 0.97 | — |
| | 256 Gb Recorder | 5 | 8 | 5 | 0.95 | — |
| **Propulsion** | Tank S (1,000 m/s) | 120 | 10 | 20 | 0.95 | — |
| | Tank L (1,400 m/s) | 220 | 10 | 28 | 0.95 | — |
| **Avionics** | Radiation-Hardened Computer | 8 | 20 | 18 | 0.99 | — |
| | Commercial Computer | 2 | 10 | 3 | 0.85 | SEU ×2 |
| | Shielding | 12 | — | 5 | — | Without it: SEU |
| **Instruments** | Neutron Spectrometer | 10 | 15 | 20 | 0.96 | Maps hydrogen (detects "hotspots") |
| | Context Camera | 8 | 10 | 8 | 0.97 | Terrain map (needed to select site) |
| | Laser Altimeter | 12 | 25 | 15 | 0.95 | Topography; +20% landing success |
| | Thermal Radiometer | 9 | 12 | 12 | 0.94 | Measures crater temperature; tells if ice can survive |
| | SAR Radar | 60 | 150 | 80 | 0.88 | Radar Overheating; sees buried ice |

#### 6.4.2 Lander and Rover Catalog ("Rover Bay")
| Category | Component | Mass kg | W | $M | Rel. | Note |
|---|---|---|---|---|---|---|
| **Lander** | Small Lander (300 kg payload) | 400 | — | 60 | 0.92 | — |
| | Medium Lander (500 kg payload) | 650 | — | 90 | 0.95 | — |
| | Hazard Sensor (Landing LIDAR) | 15 | — | 12 | 0.95 | Without it: landing roll −25% |
| **Chassis** | Light Rover (4 wheels) | 150 | 20 | 30 | 0.90 | Fast, fragile |
| | Robust Rover (6 wheels) | 300 | 35 | 50 | 0.95 | Slow, resilient |
| **Power** | Rover Battery 3 kWh | 25 | — | 6 | 0.95 | ~8 h inside the crater |
| | Rover Battery 6 kWh | 45 | — | 11 | 0.95 | ~16 h inside the crater |
| | Vertical Rover Panel | 10 | +150 | 5 | 0.95 | The Sun at the pole rises nearly horizontally; the panel must stand upright |
| | Rover Heaters | 5 | 60 | 3 | 0.97 | Without them: death by freezing in 4 h inside the crater |
| **Mobility** | Standard Wheels | — | — | 0 | 0.90 | Stuck in Regolith |
| | Mesh Wheels + Active Suspension | 15 | 20 | 10 | 0.96 | Can "walk" if stuck |
| **Navigation** | Stereo Cameras + Headlights | 6 | 30 | 8 | 0.95 | **Mandatory to enter the shadow** |
| | Autonomous Navigation | 3 | 15 | 15 | 0.92 | Advances without waiting for commands from Earth (saves cycles) |
| **Science** | Rover Neutron Spectrometer | 8 | 12 | 15 | 0.96 | Detects hydrogen beneath the wheels while moving |
| | 1 m Drill | 25 | 100 | 25 | 0.90 | Jammed Drill |
| | 2 m Deep Drill | 40 | 150 | 40 | 0.86 | More ice, more risk |
| | Mass Spectrometer (analyzes sample) | 12 | 40 | 25 | 0.93 | **Confirms what the sample is** |
| | Near-IR Spectrometer | 7 | 20 | 15 | 0.94 | Sees surface ice |

#### 6.4.3 Launch Vehicles
| Launch Vehicle | TLI Capacity | $M | Rel. |
|---|---|---|---|
| Light | 500 kg | 40 | 0.95 |
| Medium | 1,500 kg | 70 | 0.97 |
| Heavy | 4,000 kg | 120 | 0.98 |

#### 6.4.4 Compatibility Rules (The "Trade-offs" it Teaches)
- **A rover without a relay radio on the orbiter cannot communicate from the crater.** The game highlights it in red.
- **Drill + mass spectrometer** = ice confirmation. Either one alone only gives "hints".
- **The radar (150 W)** requires a GaAs panel **and** a 2 kWh battery.
- **The low orbit** requires Tank L to last through all cycles.
- **Cameras + headlights** are mandatory to enter the shadow; without them, the rover only explores the illuminated rims (science −60%).
- **Autonomous navigation:** the rover travels double the distance per cycle.
- **Lander:** its payload capacity must be ≥ the rover's mass.

#### 6.4.5 "Archetype" Designs (For Balance and Tutorial)
| Archetype | Description | Cost | Initial Stress |
|---|---|---|---|
| "Stingy" | Everything cheap, no redundancy | $210M | 55 |
| "Balanced" | GaAs, 2 kWh, robust rover, 1 m drill | $330M | 20 |
| "Ambitious" | Radar, deep drill, autonomous navigation | $395M | 35 (due to tight mass) |

### 6.5 Design Review (CML 4, "Point Design")
**Scene:** a NASA review panel (3 NPCs) inspects the design.

**Criteria (shown as an animated checklist):**
| Criterion | Requirement | Reviewer |
|---|---|---|
| Mass margin | ≥ 10% below launch vehicle capacity | Systems Engineer NPC |
| Power margin | ≥ 15% in worst-case scenario (eclipse) | Power Engineer NPC |
| Budget reserve | ≥ 10% of total | Cost Analyst NPC |
| Science traceability | Instruments answer the chosen question | Scientist NPC |
| Rover communications | Relay radio present | Comms Engineer NPC |

**Outcome:**
- **✅ Approved:** proceeds to launch. Confidence +10%.
- **❌ Rejected:** two options:
  1. **Return to CML 3 (iterate):** −3 months (−1 operational cycle), −$10M, stress −10. The game explains: *"This is how JPL works: going back to explore options is part of the process, not a failure."*
  2. **Force launch:** stress +15, +2 major cards, confidence −20%.
- Players can iterate a **maximum of 2 times**.

**Educational moment:** when a criterion fails, the NPC reviewer says **why** it matters. Example: *"Without a power margin, the first long eclipse will drain your battery. The Moon blocks the Sun for 45 minutes every two hours."*

### 6.6 Launch
**Scene:** launch pad with countdown.

1. **Mass validation:** if total mass exceeds launch vehicle capacity, **the mission fails here** (💥 ending) with an educational message.
2. **"Go / No-Go" poll:** each role confirms their system. It is a ceremonial moment animated on screen.
   - If a role has an unresolved issue (e.g., low margin), they can call **"Hold"**: delays 1 cycle and costs $5M, but removes a card.
3. **Launch roll:** launcher rel. × 1.0 (unaffected by stress).
4. **Animation:** liftoff → stage separation → trans-lunar injection.
5. **Message:** *"Selene and Buscador are on their way to the Moon. Cruise time: 5 days."*

### 6.7 Cruise and Insertion (2 cycles)
**Cycle C1, cruise:**
- **Fixed event: solar array deployment.** Roll using the panel's reliability.
  - Success: all nominal.
  - Partial: one panel at half capacity (−25% generation) until Systems repairs it.
  - Failure: −50% generation. 3-cycle timer before the battery suffers.
- **Fixed event: instrument checkout.** Science powers on each instrument once (consumes power, reveals "hidden" quality cards).
- The spacecraft draws its first card.

**Cycle C2, Lunar Orbit Insertion (LOI):**
- **The tensest moment of the cruise.** The engine must fire at the exact right moment.
- Roll: propulsion reliability.
- Success: chosen orbit achieved.
- Partial: higher orbit (−20% resolution) and extra fuel spent to correct.
- Failure: **the spacecraft flies past the Moon.** Uses the **Director's re-roll** ("Call the Experts"), and if it fails again → ❌ ending.
- **Lander separation:** the lander + rover stay "parked" with the orbiter until Act III.

### 6.8 Act I: Orbital Mapping (Cycles 1 to 4)
**Objective:** find the best hydrogen "hotspots" across the **5 candidate craters**.

**Screen:** 2D map of the lunar south pole (top-down view) with the 5 craters. Each crater starts **"no data"** (gray).

**The 5 candidate craters** (actual values are hidden at the start and revealed when mapped):
| Crater | Actual Hydrogen (hidden) | Temperature | Terrain | Note |
|---|---|---|---|---|
| Shackleton | Medium | −180 °C | Steep rims | Famous; near the Artemis site |
| Cabeus | **High** | −230 °C | Smooth | Where LCROSS impacted |
| Haworth | High | −210 °C | Rocky | High landing risk |
| de Gerlache | Low | −170 °C | Smooth | Easy and safe site, low science |
| Faustini | Medium-high | −220 °C | Very steep | Difficult for the rover to enter |

**Mapping mechanic:**
- Each cycle, Science picks **1 or 2 craters** to map (depending on powered instruments).
- Each instrument reveals a "layer":
  - **Neutron spectrometer:** hydrogen amount (from "?" to Low, Medium, or High).
  - **Camera:** terrain (safe, rocky, or steep).
  - **Laser altimeter:** exact slopes (improves landing).
  - **Radiometer:** temperature (if greater than −160 °C, ice cannot survive and it is a false lead).
  - **Radar:** buried ice (reveals exact value).
- **Mapping quality:** depends on calibration, orbit, and active cards. Low quality = data with **uncertainty** (the map shows ranges instead of exact values).

**Resource management in Act I:**
- More powered instruments = higher consumption = more battery drained during eclipses.
- More data = recorder fills up = Comms must downlink during windows.

**Act I Script:**
| Cycle | Fixed Event | Decision |
|---|---|---|
| 1 | **Commissioning:** calibration | Science: calibrate everything (no data this cycle, +20% quality for the rest) or start immediately |
| 2 | First maps | Comms: choose DSN station (Goldstone, Madrid, or Canberra depending on the time) |
| 3 | **Long eclipse season** (lasts through cycle 4) | Systems: turn off instruments during eclipse? (−science, +battery) |
| 4 | **Event: "Surface ice?"** The radiometer detects an ultra-cold spot in Cabeus | Science: focus the cycle there? (reveals Cabeus completely) or stick to the plan |

**At the end of Act I:** **"Candidate Map"** screen. Each crater displays its revealed info. Unmapped craters remain "?".

### 6.9 Act II: Landing Site Selection (Cycle 5)
**Scene:** team meeting around the map. This is the game's big gamble.

**Each role gives their opinion using data from their panel:**
- **Science:** "Cabeus has the most hydrogen."
- **Systems:** "Cabeus is at −230 °C; the rover won't last as long there."
- **Comms:** "From Haworth we get better relay contacts with our chosen orbit."
- **Director:** "The easy site (de Gerlache) is safe, but NASA expects results."

**Decision matrix shown by the game:**
| Site | Expected Science | Landing Risk | Rover Survival Time | Relay Quality |
|---|---|---|---|---|
| (filled with mapped data, with uncertainty where unmapped) | | | | |

**Decision:**
1. Choose the **landing site**: always on the **illuminated rim** of the crater, because the rover needs Sunlight to recharge.
2. Choose the **entry route** into the crater (shorter and steeper, or longer and smoother).
3. **Vote** (in 4-player mode). The Director breaks ties.

**If the team didn't map a crater and picks it anyway:** they play blind with uncertainty. It could turn out much better or much worse (revealed upon landing).

### 6.10 Act III: Descent and Landing (Cycle 6) "The 7 Minutes of Terror"
**Scene:** camera feed of the descending lander. Screen with real-time telemetry: altitude, velocity, fuel.

**4-stage sequence, each with a quick decision (15-second timer in 4-player mode):**

| Stage | What happens | Who decides | Options |
|---|---|---|---|
| 1. Deorbit (15 km) | Braking burn | Systems | Long burn (safe, more fuel) / short (saves fuel, risky) |
| 2. Approach (2 km) | LIDAR scans the terrain | Science | Trust the planned site / divert to a safer alternate site (less science) |
| 3. Hazard Alert (500 m) | **Mandatory landing card:** boulder, slope, or unexpected shadow | Comms + Systems | Divert (spends fuel) / hold course (roll) |
| 4. Touchdown (50 m) | Final descent | Director | "Authorize touchdown" (final roll) / "Abort and retry" (only if fuel remains) |

**Final landing roll:**
`P = 0.85 × lander_rel × terrain_modifier × (LIDAR ? 1.0 : 0.75) × (altimeter mapped site ? 1.2 : 1.0) × (1 − stress/200)`

| Outcome | Effect |
|---|---|
| Perfect landing | Rover deployed, +10 confidence |
| Hard landing | Rover deployed with −20% wheel integrity or one damaged instrument |
| Tilted landing | Ramp blocked: **extra deployment roll** in cycle 7 |
| Failure | Lander lost → skips to **alternate ending "Plan B"** (orbiter impact, see Act V) |

**Success message:**
> `[BUSCADOR] TOUCHDOWN CONFIRMED. TILT 4°. ALL SYSTEMS NOMINAL.`
> *Applause in the control room (animation of the 4 characters).*

### 6.11 Act IV: The Rover Searches for Water (Cycles 7 to 11)
**The heart of the mission.** The timescale shifts: **1 cycle = 1 "lunar workday"** (about 24 h of operations).

**Rover screen:**
- Top-down crater map with a grid of **zones** (see 7.1).
- Rover schematic with its gauges (battery, temperature, wheels, drill).
- **"Next orbiter contact"** line (countdown).
- Rover camera (stylized image, with headlights illuminating the darkness).

**Act IV Script:**
| Cycle | Fixed Event | Key Decision |
|---|---|---|
| 7 | **Deployment and first wheels on the Moon.** Mobility test on the illuminated rim | Science: first surface hydrogen reading (serves as calibration). Systems: charge to 100% before entering |
| 8 | **Entering the darkness.** The rover crosses the shadow line | Director authorizes entry. Systems sets the **"point of no return"** (see 7.3) |
| 9 | **First drill** | Science: drill here or push deeper to a more promising zone? |
| 10 | **Event: "Anomalous Reading"** The rover's spectrometer detects a massive hydrogen spike 200 m deeper inside | Everyone: go for the spike (tight battery) or turn back to recharge? **Central dilemma of the game** |
| 11 | **Return to the light or final drill** | See Act V |

**What each role does during Act IV:**
- **Science:** decides where to drill, analyzes samples, and interprets results.
- **Systems:** manages the rover's battery and heaters and calculates whether there is enough power to return.
- **Comms:** schedules relay contacts; without contact, the rover receives no orders (unless equipped with autonomous navigation).
- **Director:** authorizes risks and decides when the mission has "won enough".

### 6.12 Act V: Ending (Cycle 12)
Depends on what happened. There are **three paths**.

#### Path A: "The Return" (the rover made it back to the light)
- The rover recharges on the rim. The team can request an **extended mission** (+4 cycles) if confidence is ≥ 30% and budget is ≥ $20M.
- **Final orbiter event:** it runs out of fuel. Decision: **controlled impact into Cabeus** (LCROSS-style; the dust plume yields extra data, +science) or leave it in a high orbit as a relay for future Artemis missions (+confidence).

#### Path B: "The Last Message" (the rover remains in the darkness)
- Battery is not enough to return. The rover has **1 final cycle of life**.
- **Emotional decision:** spend the remaining power on:
  1. One **final drill** at the hydrogen spike (huge science if transmitted).
  2. One **final transmission** of all stored data (secures what has already been gathered).
- There isn't enough power for both. Comms needs a relay window on that exact cycle.
- **Rover's final message:** `[BUSCADOR] BATTERY 2%. TEMPERATURE -52°C. TRANSMITTING... ` → silence.
- *Educational moment:* the report explains that VIPER was specifically designed to avoid getting trapped in the shadow.

#### Path C: "Plan B" (if the landing failed)
- No rover. The orbiter continues mapping for additional cycles.
- **Ending:** deliberate impact of the orbiter into the most promising crater (like LCROSS). Roll; if successful, the dust plume **confirms water from orbit**. Achieves a "Partial Success" with a redemption message.

### 6.13 Post-Mission Report
**Final screen in 5 sections:**
1. **Mission outcome:** achieved ending (🏆 / ✅ / ⚠️ / ❌ / 💥) with an illustration.
2. **Science:**
   - Final south pole map showing discoveries.
   - Confirmed ice: yes or no, how much, at what depth.
   - Transmitted vs. generated data.
3. **Personal missions:** each role with ✅ or ❌ and a one-liner.
4. **Causal chain** (the most educational feature): a timeline connecting decisions to consequences.
   > *"Cycle 3: no battery heaters → 'Cold Battery' card → battery at 12% → safe mode → Haworth mapping lost."*
   > *"Hangar: you chose the robust rover → in cycle 10 you survived getting stuck in regolith."*
5. **Comparison with real missions:** "Your mission resembles…" (LRO, LCROSS, VIPER, Lunar Prospector), with a real fact about each.
6. **The napkin** from CML 1 alongside the final spacecraft: *"From idea to the Moon."*

**Buttons:** retry with same design / redesign / next mission / share result.

---

## 7. Detailed Rover Mechanics

### 7.1 The Crater as a Board
- The crater is divided into a **grid of zones** (e.g., 5 × 5).
- **Rim zones (illuminated):** the rover recharges via its vertical panel. Temperature from −50 °C to −20 °C.
- **Slope zones (partial shadow):** no charging; moderate cold (−100 °C).
- **Floor zones (permanent shadow):** −200 °C or colder. **That is where the ice is.**
- Each zone has **hidden** values: hydrogen, terrain, and ice presence. Revealed when driven over or drilled.
- Zones mapped from orbit in Act I show **clues** (faint colors).

### 7.2 Movement
- Each cycle, the rover can move **1 zone** (or **2 with autonomous navigation**).
- Moving costs battery depending on terrain:
  | Terrain | Battery | Risk |
  |---|---|---|
  | Smooth | 300 Wh | — |
  | Rocky | 500 Wh | "Wheel Damage" card (roll) |
  | Steep | 700 Wh | "Slippage" card |
  | Loose regolith | 600 Wh | "Stuck" card |
- While moving, the **rover's neutron spectrometer** reveals hydrogen in the current and adjacent zones.

### 7.3 Battery and "Point of No Return"
- **Core rule:** inside the shadow, **there is no charging**. Each cycle drains battery for:
  - Heaters: 60 W × 24 h ≈ 1,440 Wh (**the largest drain**; without them, the rover freezes to death).
  - Base systems: 35 W × 24 h ≈ 840 Wh.
  - Moving, drilling, and analyzing: depending on the action.
- **"Point of No Return" indicator** on Systems' interface: calculates live **how much battery is needed to return to the light** from the current zone. When the battery nears that threshold, the bar turns red.
- **Crossing the point of no return** triggers Path B (the last message).
- **Tactical decision:** save power by turning off heaters for one cycle (−600 Wh drain, but roll against cold damage).

*With these numbers, a 3 kWh battery cannot survive a full 24-hour cycle in the shadow with heaters on. This forces players to bring the 6 kWh battery or make short sorties. This is intentional: it is a trade-off learned through play.*

### 7.4 Rover Temperature
- Initial internal temperature: +20 °C.
- In permanent shadow, without heaters: −15 °C per cycle.
- With heaters: remains stable.
- Thresholds:
  | Temp | Effect |
  |---|---|
  | Greater than −10 °C | Nominal |
  | −10 to −30 °C | Battery at −20% efficiency |
  | −30 to −40 °C | Instruments fail (roll per use) |
  | Less than −40 °C | **Electronics death** (end of rover) |

### 7.5 Drilling (Star Mechanic)
**Science action (main) + Systems support (power).** Costs 100–150 W during the cycle.

**Steps:**
1. **Choose depth:** 25 cm / 50 cm / 1 m (or 2 m with the deep drill). Deeper = higher probability of ice, more battery, and higher risk of jamming.
2. **Drill roll:** `drill_rel × (1 − depth × 0.1) × (1 − stress/200)`.
   - Success: sample obtained.
   - Partial: sample obtained, drill −20% life.
   - Failure: **"Jammed Drill"** (timer: free it within 1 cycle or it is lost).
3. **Analysis (next cycle or same cycle, depending on power):** mass spectrometer.
4. **Result** (based on the zone's hidden value and depth):
   | Result | Science Points | Message |
   |---|---|---|
   | Dry regolith | 5 | "No trace of water." |
   | Hydrogen (not necessarily water) | 15 | "Hydrogen detected; could be hydroxyl." |
   | Trace ice (less than 1%) | 30 | "Trace ice detected!" |
   | **Confirmed ice (1–5%)** | 60 | "💧 **WATER ICE CONFIRMED.**" |
   | **Rich vein (greater than 5%)** | 100 | "💧💧 **Rich deposit! Viable resource for Artemis.**" |
5. **Transmit:** the sample only counts if Comms downlinks it during a relay window.

**Without a mass spectrometer:** the highest possible result is "Hydrogen (not necessarily water)". This teaches why having the right instruments matters (scientific traceability).

### 7.6 Rover Communications (Relay)
- The rover **cannot see Earth** from inside the crater.
- It only communicates when the **orbiter passes overhead**. Frequency depends on the orbit chosen in CML 2:
  | Orbit | Rover contacts per cycle | Duration |
  |---|---|---|
  | Low polar | 3 | Short (1 Gb each) |
  | High polar | 2 | Medium (2 Gb each) |
  | Elliptical | 1 | **Long (6 Gb)** |
- **Without autonomous navigation:** the rover **can only execute actions planned during a contact**. If a cycle has no contact (e.g., due to a card), the rover sits idle draining battery.
- **With autonomous navigation:** the rover can move without contact, though it cannot drill.
- **Comms mechanic:** plan which commands to uplink and which data to downlink during each contact, within limited bandwidth.

### 7.7 Wheels and Integrity
- Initial integrity: 100% (−20% if the landing was hard).
- Rocky terrain: −10% per move if the roll fails.
- Below 30%: the rover can only move on smooth terrain.
- At 0%: **immobilized**; it can drill where it stands, but cannot move.
- **Stuck in regolith:**
  - Standard wheels: 50% roll to break free (spends 1 cycle).
  - Mesh + active suspension: "walk" out (85% roll).

---

## 8. Complete Card Catalog

### 8.1 Orbiter Cards
| Card | Tier | Origin | Effect | Response | Timer |
|---|---|---|---|---|---|
| Telemetry Noise | Minor | Base | −10% data quality this cycle | None | — |
| Pointing Drift | Minor | Base | Mapping −20% | Science recalibrates (90% roll) | — |
| Weak Link | Minor | LG Antenna | −50% downlink | Comms repoints (80% roll) | — |
| Cold Battery | Minor | No heaters | −30% capacity in eclipse | Systems: manual heaters (+30 W) | — |
| Cell Degradation | Minor | Si Panel | −5% permanent generation | None (stackable) | — |
| Solar Heating | Minor | Base | +10 °C in avionics | Systems orients radiator | 2 cycles |
| Optical Contamination | Major | IR Spectrometer / camera | Camera −40% | "Bake-out" (1 cycle off, +50 W) | — |
| Radar Overheating | Major | Radar | Radar damage | Systems lowers power / turns off | 2 cycles |
| Jammed Antenna | Major | HG Antenna | No downlink | Comms: wiggle command (60% roll) | — |
| Computer SEU | Major | No shielding / comm. comp. | Safe mode 1 cycle | Comms: recovery command | — |
| Battery Overheating | Major | Low power margin | −30% permanent capacity if it explodes | Systems reduces load | 2 cycles |
| Damaged Panel | Major | Micrometeoroid event | −25% generation | Systems repairs (70% roll) | — |
| Corrupted Recorder | Major | Cheap recorder | 20% of stored data lost | Comms downlinks before timer expires | 1 cycle |
| Thruster Leak | Critical | Stress greater than 85 | −30% fuel | Director: abandon low orbit | — |
| Loss of Attitude | Critical | Stress greater than 85 | No power or comms | Joint roll (all 4 roles) | 1 cycle |
| Relay Radio Failure | Critical | Stress greater than 85 | Rover loses communications | Comms: backup radio (50% roll) | 2 cycles |

### 8.2 Landing Cards (Cycle 6 Only)
| Card | Effect | Response |
|---|---|---|
| Uncharted Boulder | Hazard at touchdown point | Divert (−fuel) or roll |
| Excessive Slope | Lander could tip over | Divert or roll |
| Unexpected Shadow | LIDAR loses accuracy | Roll −15% |
| Kicked-Up Dust | Cameras blind in the final 20 m | Trust the LIDAR (if equipped) |
| Underperforming Engine | More fuel required | Systems: abort or continue? |

### 8.3 Rover Cards
| Card | Tier | Origin | Effect | Response | Timer |
|---|---|---|---|---|---|
| Dust on Cameras | Minor | Base | Navigation −30% | Science: cleaning (shake) | — |
| Blown Headlight | Minor | Base | Movement in shadow costs double | None (loses 1 headlight) | — |
| Power Spike | Minor | Base | −200 Wh | None | — |
| Wheel Damage | Major | Standard wheels / rocky terrain | −15% integrity | Systems: traction adjustment | — |
| Stuck in Regolith | Major | Standard wheels | Immobilized | Roll to break free | 2 cycles (permanent immobilization afterward) |
| Jammed Drill | Major | Drill | No drilling | Science + Systems: free drill (roll) | 1 cycle |
| Faulty Heater | Major | Stress greater than 30 | −15 °C per cycle | Systems: reroute power | 2 cycles |
| Cold-Degraded Battery | Major | Temp less than −10 °C | −20% permanent capacity | None | — |
| Slippage | Major | Steep terrain | Rover slides down 1 zone (deeper inside) | Braking roll | — |
| Loss of Contact | Critical | Stress greater than 60 | No contact this cycle | Comms: reschedule relay | — |
| Mass Spectrometer Failure | Critical | Stress greater than 85 | Cannot confirm ice | Systems: reboot (40% roll) | — |
| Imminent Thermal Death | Critical | Temp less than −30 °C | Temperature −20 °C | All power to heating or flee to the light | 1 cycle |

---

## 9. Narrative Events and Dialogues

### 9.1 NPC Characters
| NPC | Role | When they appear |
|---|---|---|
| **Dr. Elena Ríos**, Program Director | Gives briefing, approves extended mission | CML 1, ending |
| **Review Panel** (3 engineers) | CML 4 Review | CML 4 |
| **"Houston"**, DSN Operator | Notifies of windows and conflicts | During operations |
| **Press** | Reacts to successes and failures | Key events |

### 9.2 Narrative Events (In Addition to the Script)
Can trigger randomly 1–2 times per playthrough:
| Event | Possible Cycle | Decision |
|---|---|---|
| **"DSN Conflict"**: another mission needs the dish | Any | Director: pay $8M to keep it or lose 1 downlink |
| **"Collaboration Proposal"**: an allied agency offers an extra instrument in exchange for data sharing | Act I | Director: accept (+science, −exclusivity, +confidence) |
| **"Budget Cut"**: Congress slashes $30M | Act I–II | Director: what gets sacrificed? (operational days or reserves) |
| **"Meteor Shower"**: the Moon passes through a micrometeoroid stream | Act I | Systems: slew the spacecraft (−science) or risk the solar panel |
| **"Artemis Request"**: NASA asks for photos of a human landing site | Act I | Science: spend 1 cycle (+confidence, −own science) |
| **"Live with Students"**: educational broadcast with schools | Act IV | Comms: bandwidth for video (−data, +confidence) |

### 9.3 Telemetry Lines (Console Examples)
- `[SELENE] ECLIPSE IN 00:12:00. BATTERY CHARGE 64%.`
- `[SELENE] ⚠ TEMP BAT2 -18°C ↓ HEATERS INACTIVE.`
- `[BUSCADOR] ENTERING PERMANENT SHADOW. EXT TEMP -187°C.`
- `[BUSCADOR] EPITHERMAL NEUTRONS ↓ 32%. POSSIBLE HYDROGEN.`
- `[BUSCADOR] DRILL 48cm... 49cm... ANOMALOUS RESISTANCE.`
- `[BUSCADOR] 💧 H₂O CONFIRMED. CONCENTRATION 3.2%.`
- `[DSN-MADRID] SIGNAL ACQUISITION. DOWNLINK 2 Mbps.`

---

## 10. Interface by Role

### 10.1 Global Screen (Visible to All)
- Top bar: current cycle, budget, confidence, and **stress gauge**.
- Center: spacecraft schematic (orbiter or rover depending on the act) with status-colored subsystems and timer clocks.
- Bottom: scrolling telemetry console with live messages.
- Sidebar: active spacecraft cards and which component spawned them.

### 10.2 Director Panel
- Budget with breakdown.
- Approval buttons (light up when another role requests authorization).
- NASA confidence gauge.
- "Call the Experts" counter (1/act).
- Mission timeline.

### 10.3 Systems Panel
- **Power sliders** per subsystem, showing live generation vs. consumption.
- Projected battery graph heading into the next eclipse.
- Spacecraft thermal map (color-coded by temperature).
- In Act IV: rover **"Point of No Return" indicator**.
- Remaining fuel.

### 10.4 Science Panel
- Instrument switches showing power draw and data per cycle.
- South pole map (Act I) / crater map (Act IV).
- Data quality by instrument.
- Sample and results list.
- Traceability matrix (question → measurement → instrument) with checkmarks.

### 10.5 Comms Panel
- **Window schedule** for DSN (Act I) and relay contacts (Act IV).
- Storage bar (turns red as it fills up).
- Draggable **data queue** for prioritization.
- Antenna status and link quality.
- Command queue for the rover.

---

## 11. Endings

| Ending | Condition | Illustration and Text |
|---|---|---|
| 🏆 **Historic Discovery** | Confirmed ice (≥ 1–5%) + rover returns to the light + 4/4 personal missions | Rover on the rim with Earth in the background. *"They found the water that will make returning to the Moon to stay possible."* |
| 💧 **Water Confirmed** | Ice confirmed and transmitted | Spectrometer graph. *"For the first time, a human machine touched lunar ice."* |
| 📡 **The Last Message** | Ice confirmed, but the rover is lost in the shadow | Rover with headlights fading out. *"Buscador remained in the darkness, but its last message made it home."* |
| ⚠️ **Hints** | Only hydrogen detected / orbital map | Heat map. *"They know where to look. The next mission will go get it."* |
| ☄️ **Plan B** | Failed landing, successful orbiter impact | Dust plume. *"Like LCROSS in 2009: sometimes you have to crash to discover."* |
| ❌ **Mission Lost** | Orbiter dies before landing, or budget or confidence reaches 0 | Static screen. *"Physics does not forgive. Review the causal chain."* |
| 💥 **Launch Failure** | Mass greater than capacity or failed launch roll | Rocket on the pad. *"The mission ended before it began. Mass margin is not optional."* |

---

## 12. Scoring and Achievements

### 12.1 Formula


Points = Transmitted science (sample + mapping points)
+ Remaining budget ($M) × 2
+ (100 − Final stress)
+ 50 × completed personal missions
+ Ending bonus (🏆 +300 / 💧 +200 / 📡 +150 / ⚠️ +50 / ☄️ +75)


**Multiplier:** based on the CML 1 question (×1 / ×2 / ×3).

### 12.2 Ranks
| Points | Rank |
|---|---|
| Less than 200 | Intern |
| 200–499 | Junior Engineer |
| 500–899 | Mission Engineer |
| 900–1,299 | Principal Investigator |
| ≥ 1,300 | JPL Legend |

### 12.3 Achievements
| Achievement | Condition |
|---|---|
| **Flawless Engineering** | Pass CML 4 on the first try |
| **The Iterator** | Return to CML 3 twice and still win 🏆 |
| **On the Edge** | Return to the light with less than 5% battery |
| **Eagle Eye** | Map all 5 craters in Act I |
| **NASA Saver** | Finish with greater than 25% of the budget |
| **Mother Lode** | Find a rich deposit (greater than 5%) |
| **Tribute to LCROSS** | Ending with controlled impact into Cabeus |
| **Against All Odds** | Win with final stress greater than 85 |
| **Feather Landing** | Perfect landing without LIDAR |

---

## 13. Educational Value and Connection to Real Missions

### 13.1 What the Player Learns (and When)
| Concept | Where it is learned |
|---|---|
| Concept Maturity Levels (CML) of a mission | Entire design phase |
| Mass, power, and cost trade-offs | Hangar |
| Margins and reserves | CML 4 Review |
| Iterating is not failing | Option to return to CML 3 |
| Eclipses and energy storage | Act I |
| Generated vs. transmitted data | Comms, entire game |
| How water is detected (neutrons → hydrogen → spectrometry) | Acts I and IV |
| Why the right instruments are needed (traceability) | Drilling without a mass spectrometer |
| Relay communications | Act IV |
| Extreme cold as a threat | Rover in the shadow |
| The relationship between risk and science | Cycle 10 dilemma |

### 13.2 Real Missions Referenced
| Mission | Year | What it did | Where it appears in the game |
|---|---|---|---|
| Lunar Prospector | 1998 | Detected hydrogen at the poles using a neutron spectrometer | Briefing, orbiter spectrometer |
| LRO | 2009 → | Maps the Moon; its radiometer measured the coldest craters in the solar system | Camera, altimeter, radiometer |
| LCROSS | 2009 | Impacted Cabeus and detected water in the plume | Plan B ending, achievement |
| Chandrayaan-1 (M3) | 2009 | Detected surface ice at the poles | IR Spectrometer |
| VIPER | (designed for the south pole) | Rover to search for ice in shadowed craters with a 1 m drill | All of Act IV |
| Artemis | Current | Human return to the Moon; water is a key resource | Narrative, events |

### 13.3 NASA Resources Used
- **CML (JPL):** structure of the entire design.
- **GMAT:** orbital parameters (eclipse, windows, Δv) → `orbits.json`.
- **LRO / Lunar Prospector data:** basis for crater hydrogen and temperature values.
- **NASA lunar textures (LRO, public domain):** south pole maps.
- **NASA Small Spacecraft State of the Art:** basis for the component catalog.

---

## 14. Hackathon MVP Scope Cut
If time runs short, implement in this order and pitch the rest as design:

| Priority | What to include | What to leave out |
|---|---|---|
| **P0 (essential)** | Simplified briefing (fixed question B), orbit choice, Hangar, CML 4 review, launch, 3-cycle Act I, 8 cards, basic report | Multiplayer, narrative events |
| **P1 (highly desirable)** | Landing (4 stages), Act IV with 3 × 3 grid, drilling, point of no return, 💧 / 📡 / ⚠️ endings | Secret missions, achievements |
| **P2 (if time permits)** | Full causal chain, all endings, 3D orbit view, NPCs with dialogue | — |
| **P3 (pitch)** | 4-role multiplayer, Sun and Exoplanet missions, narrative events | — |

**Ideal 3-minute demo for the judges:**
1. (30 s) Hangar: show how cutting heaters adds the "Cold Battery" card to the deck.
2. (30 s) CML 4 Review rejected → iterate.
3. (45 s) Act I: the eclipse, the card that triggers, and how Systems resolves it.
4. (45 s) Rover: the cycle 10 dilemma and drilling → "💧 WATER ICE CONFIRMED".
5. (30 s) Report with the causal chain.