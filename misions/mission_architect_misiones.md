# 🛰️ Mission Architect: Complete Mission Design
*Companion to `mission_architect_contexto.md`*

> **Note on the numbers:** all figures (masses, watts, costs, eclipse %, DSN windows) are **plausible game values** for balancing. They will later be replaced by the values from `orbits.json` (GMAT) and `components.json` (real catalogs). The structure does not change.

---

## 0. Rules common to all missions

### 0.1 Structure of a match
| Phase | CML | Duration | What happens |
|---|---|---|---|
| 1. Briefing | 1–2 | 1 team turn | Science question, orbit, budget |
| 2. Hangar | 3 | Open-ended (or 10-min timer) | The spacecraft is assembled; the spacecraft's deck fills up as you build |
| 3. CML 4 Review | 4 | 1 turn | Margins → approve, iterate or force |
| 4. Launch | — | Animation + validation | Mass vs. launcher; launch roll |
| 5. Cruise / insertion | — | 2 cycles | First cards, orbital insertion maneuver |
| 6. Science operations | — | 8–12 cycles | Core of the game |
| 7. End of mission | — | 1 cycle | Final event depending on the mission |
| 8. Report | — | Screen | Score, ending, chain of causes |

### 0.2 Global resources
- **Budget ($M)**: controlled by the Director. If it hits 0, the mission is cancelled.
- **Schedule (months)**: delays in the Hangar or in reviews reduce the available operating cycles.
- **Power (W and Wh)**: generation vs. consumption; the battery buffers the difference.
- **Temperature (°C per subsystem)**: each has an operating range; outside it, failures appear.
- **Data (Gb)**: generated → stored → transmitted. Only what is transmitted counts.
- **Spacecraft stress (0–100)**: determines how many cards the spacecraft draws and at what level.

### 0.3 The enemy spacecraft: how it draws cards
| Stress | Cards per cycle | Card level |
|---|---|---|
| 0–29 | 1 | Minor |
| 30–59 | 1 | Minor or major (50/50) |
| 60–84 | 2 | Major |
| 85–100 | 2 | Major + 1 critical |

**Stress goes up with:** mass margin < 10% (+10), power margin < 15% (+10), each component with reliability < 0.90 (+5), forcing the CML 4 review (+15), each timer that expires (+5).
**Stress goes down with:** passing a hard engineering roll (−5), a cycle with no alerts (−3), iterating at CML 3 (−10).

### 0.4 Engineering roll
`P(success) = card_base × component_reliability × (1 − stress/200) + role_bonuses`
- **Role bonuses:** the role that owns the affected subsystem adds +10% if it spends its action for the cycle.
- The result can be **success**, **partial success** (it resolves, but leaves a timer) or **failure**.

### 0.5 Actions per cycle
Each role has **1 main action + 1 minor action** per cycle:
- **Director:** approve an expense, reallocate budget, authorize a risk, "call in the experts" (re-roll once per mission).
- **Systems:** redistribute watts, turn on heaters or radiators, repair (roll), put a subsystem into safe mode.
- **Science:** turn instruments on or off, choose the cycle's target, calibrate (roll), compress data (lower quality, more volume).
- **Comms:** point the antenna, reserve a DSN window, prioritize the downlink queue, send recovery commands.

### 0.6 Possible endings (all missions)
| Ending | Condition |
|---|---|
| 🏆 **Total success** | Minimum + extended science met, spacecraft operational at the end, 4/4 personal missions |
| ✅ **Success** | Minimum science met |
| ⚠️ **Partial success** | ≥ 50% of the minimum science |
| ❌ **Mission loss** | The spacecraft dies (battery at 0 during eclipse with no recovery, unresolved critical failure, or budget at 0) |
| 💥 **Launch failure** | Mass > launcher capacity, or failed launch roll |

### 0.7 Scoring
`Points = Science_transmitted × 10 + Budget_remaining × 2 + (100 − Final_stress) + 50 × personal_missions_completed`

---

## 🌙 MISSION 1: "Water on the Moon" (difficulty: introductory)

### Briefing
> *"The permanently shadowed craters at the lunar poles may have held water ice for billions of years. That ice could supply water, oxygen and propellant to future human bases. Your mission: confirm how much water is there, and where."*

- **Budget:** $300M
- **Schedule:** 36 months of development → 12 operating cycles (1 cycle = 1 month)
- **Available launchers:**
  | Launcher | Capacity to TLI* | Cost |
  |---|---|---|
  | Small | 350 kg | $40M |
  | Medium | 900 kg | $70M |
  | Heavy | 3,000 kg | $120M |
  *TLI = trans-lunar injection

### CML 1: the question (Science decides, the team weighs in)
| Question | Required measurement | Ideal instrument |
|---|---|---|
| A. Is there hydrogen at the poles? | Epithermal neutron flux | Neutron spectrometer (light) |
| B. Is there exposed surface ice? | Infrared reflectance | IR spectrometer |
| C. Is there buried ice, and how much? | Radar backscatter | Synthetic aperture radar (heavy and expensive) |

Choosing **C** gives double the science points, but requires the radar.

### CML 2: the orbit (Comms and Systems report, Director approves)
| Orbit | Polar coverage | Eclipse per orbit | DSN windows/cycle | Insertion Δv | Note |
|---|---|---|---|---|---|
| Low polar (50 km) | Excellent | 47 min | 6 | 900 m/s | Needs orbit maintenance (propellant) |
| High polar (100 km) | Good | 45 min | 6 | 850 m/s | Balanced |
| Near-rectilinear halo (NRHO) | Poor resolution | Almost none | Continuous | 450 m/s | Science −40%, easy comms |

### CML 3: the Hangar
**Mission catalog**
| Component | Mass (kg) | W | $M | Rel. | Cards it adds |
|---|---|---|---|---|---|
| Small bus (structure) | 80 | 15 | 25 | 0.95 | — |
| Medium bus | 140 | 20 | 40 | 0.97 | — |
| GaAs panel 400 W | 25 | +400 | 15 | 0.97 | — |
| Si panel 250 W | 30 | +250 | 6 | 0.88 | Cell degradation |
| Li-ion battery 1 kWh | 8 | — | 4 | 0.95 | — |
| Li-ion battery 2 kWh | 15 | — | 7 | 0.95 | — |
| Battery heaters | 2 | 30 | 1 | 0.98 | (without them: Cold battery) |
| Low-gain antenna | 3 | 15 | 2 | 0.98 | Weak link |
| High-gain antenna | 18 | 40 | 10 | 0.94 | Stuck antenna |
| Chemical propulsion (tank S) | 120 | 10 | 20 | 0.95 | — |
| Chemical propulsion (tank L) | 220 | 10 | 28 | 0.95 | — |
| Avionics shielding | 12 | — | 5 | — | (without it: SEU) |
| Neutron spectrometer | 10 | 15 | 20 | 0.96 | — |
| IR spectrometer | 25 | 35 | 35 | 0.92 | Optical contamination |
| SAR radar | 60 | 150 | 80 | 0.88 | Radar overheating |
| Context camera | 8 | 10 | 8 | 0.97 | — |
| Data recorder 64 Gb | 3 | 5 | 2 | 0.97 | — |
| Data recorder 256 Gb | 5 | 8 | 5 | 0.95 | — |

**Constraints that create conflict between roles**
- The radar (150 W) only works with the GaAs panel **and** the 2 kWh battery. Otherwise it would drain the battery in every eclipse.
- The low orbit needs tank L to hold the orbit for 12 cycles. With tank S it only lasts 8.
- Low-gain antenna + radar: generates data faster than it can be transmitted, and the recorder fills up.

### Personal missions (Moon)
| Role | Mission | Exact condition |
|---|---|---|
| Science | **Water map** | Transmit ≥ 40 Gb of data from the main instrument; bonus if it covers both poles |
| Systems | **Survive the lunar night** | Battery never below 20% during eclipses |
| Comms | **Not a single bit lost** | Recorder never at 100% (no overwritten data) |
| Director | **Within budget** | Finish with ≥ $20M in reserve |

### CML 4 Review
- **Approved** if: mass margin ≥ 10% of the launcher, power margin ≥ 15%, budget ≥ $30M in reserve.
- **If it fails:** iterate (−3 months = −1 operating cycle, −$10M, stress −10) or force (+15 stress, +2 major cards).

### Launch and cruise
- **Launch:** base roll 97% × launcher reliability.
- **Cycle C1, cruise (5 days):** solar panel deployment. Roll using the panel's reliability. On a partial failure, one panel is lost and generation drops by 50% until it is repaired.
- **Cycle C2, orbital insertion (LOI):** engine burn. Δv depends on the chosen orbit. If the tank falls short, the orbit ends up higher and 20% of resolution is lost.

### Operations: 12-cycle script
The **fixed** events provide structure; on top of that, the spacecraft draws cards according to stress.

| Cycle | Fixed event | Key decision |
|---|---|---|
| 1 | **Commissioning:** instrument calibration | Science: calibrate everything (1 cycle with no data) or start right away (−15% quality) |
| 2 | First observations of the south pole | Comms: reserve long or short windows |
| 3 | **Long eclipse season** (3 cycles) | Systems: shut down instruments during eclipse? |
| 4 | Eclipse season continues | Systems: lower the load to protect the battery? |
| 5 | **"Anomalous signal in Shackleton crater"** | Science: divert 2 cycles to observe it? (×2 science bonus, but the north pole stops being covered) |
| 6 | End of the eclipses | — |
| 7 | **Orbit maintenance** | Systems/Director: burn propellant or let the orbit decay |
| 8 | North pole visible | Science: switch targets |
| 9 | **DSN conflict:** another NASA mission requests priority | Director: pay $8M to keep the window or lose 1 downlink cycle |
| 10 | Second eclipse season (shorter) | — |
| 11 | **Extended mission proposal** | Director: if there is propellant and budget, +4 cycles |
| 12 | **Finale:** controlled impact | See below |

### Spacecraft deck (Moon)
| Card | Level | Effect | Response |
|---|---|---|---|
| Cold battery | Minor | −30% capacity during eclipse | Systems turns on heaters (+30 W) |
| Cell degradation | Minor | −5% permanent generation | None; it accumulates |
| Weak link | Minor | −50% downlink this cycle | Comms re-points (roll) |
| Optical contamination | Major | IR spectrometer at −40% | Science: "bake-out" (1 cycle off + 50 W) |
| Radar overheating | Major | 2-cycle timer: radar damaged | Systems lowers power / shuts down the radar |
| Stuck antenna | Major | No downlink until resolved | Comms: shake command (60% roll) |
| SEU in computer | Major | Reboot: safe mode for 1 cycle | Comms sends recovery |
| Propulsion leak | Critical | −30% propellant | Director: abandon the low orbit |
| Loss of attitude | Critical | No solar power or comms; 1-cycle timer before the battery runs out | Everyone: joint roll |

### End of mission: "The Last Descent"
In cycle 12, the spacecraft crashes on purpose into a shadowed crater. LCROSS did exactly this in 2009, when its impact threw up water vapor that confirmed the ice.
- **Team decision:** where to impact?
  - Known crater: +10 guaranteed points.
  - Never-observed crater: roll; if it goes well, +40 science points ("discovery").
- Comms must have the **DSN window reserved** to transmit the impact data in real time. Otherwise, it is lost.
- **Alternative:** if the extended mission was approved, the finale moves to cycle 16.

### Lessons learned (report text)
- Eclipse → battery → mass: *"your battery is heavy because the Moon blocks the Sun for 45 minutes every 2 hours"*.
- Data generated ≠ useful data: *"you generated 120 Gb but only downlinked 35"*.
- Connection to real missions: Lunar Prospector, LRO, LCROSS, Lunar Trailblazer.

---

## ☀️ MISSION 2: "Solar Sentinel" (difficulty: intermediate)

### Briefing
> *"A coronal mass ejection can knock out satellites, power grids and GPS on Earth. Your spacecraft will be a sentinel at the L1 point, 1.5 million km from Earth, between Earth and the Sun. Detect the storms before they arrive and sound the warning in time."*

- **Budget:** $450M
- **Schedule:** 10 operating cycles (1 cycle = 2 months) + 3 cruise cycles
- **Special mechanic: Alerts.** Every CME detected and **warned about in time** to Earth adds "Lives protected". It is a second score shown on screen.
- **Real data:** the game's CMEs can be drawn from historical events in the DONKI API (e.g. the May 2024 storm).

### CML 1: the question
| Question | Instrument |
|---|---|
| A. When does a CME leave the Sun? | Coronagraph (sees the Sun from the side) |
| B. How strong will it be when it reaches Earth? | Magnetometer + plasma analyzer (in-situ measurement) |
| C. Both (full alert system) | All three; expensive and heavy |

### CML 2: the orbit
| Orbit | Advantage | Disadvantage |
|---|---|---|
| Halo at L1 | Continuous view of the Sun, no eclipses | 3-cycle cruise; the Sun sits close to the Earth-spacecraft axis and adds noise to comms |
| Lissajous at L1 | Less insertion Δv | More frequent windows with solar interference |
| LEO (trap option) | Cheap and close | Eclipses, the magnetosphere blocks the measurement. Science −70% |

### Hangar particulars
- **No eclipses:** the battery barely matters, and **thermal control** becomes the main problem (Sun always in front).
- **High radiation:** shielding is almost mandatory. Without it, the SEU card enters the deck ×3.
- **New components:**
  | Component | Mass | W | $M | Rel. | Cards |
  |---|---|---|---|---|---|
  | Coronagraph | 35 | 40 | 60 | 0.92 | Stray light |
  | Magnetometer (with 6 m boom) | 6 | 5 | 15 | 0.95 | Undeployed boom |
  | Plasma analyzer | 15 | 20 | 30 | 0.93 | Saturation |
  | Reinforced shielding | 30 | — | 12 | — | — |
  | Radiation-hardened computer | 8 | 20 | 18 | 0.99 | — |
  | Commercial computer | 2 | 10 | 3 | 0.85 | SEU ×2 |
  | Large radiator | 15 | — | 6 | — | — |

### Personal missions (Sun)
| Role | Mission | Condition |
|---|---|---|
| Science | **Catch the great storm** | Detect and measure the extreme CME of cycle 7 |
| Systems | **Cold skin** | No subsystem out of thermal range for more than 1 consecutive cycle |
| Comms | **Early warning** | ≥ 4 alerts sent on time (before impact on Earth) |
| Director | **Public service mission** | ≥ 1,000,000 cumulative "Lives protected" |

### Alert mechanic (core of this mission)
1. The Sun launches a CME (event). The spacecraft has to **detect it**: coronagraph on and a roll.
2. **Measure it:** magnetometer + plasma determine how dangerous it is.
3. **Warn:** Comms has to transmit within the same window. If not, the alert arrives late.
4. A correct alert adds lives protected according to intensity. **A false alarm subtracts trust**, which works as a multiplier.
- Constant dilemma: the very instruments that give the warning are the ones the CME damages.

### 10-cycle script
| Cycle | Fixed event | Key decision |
|---|---|---|
| C1–C3 | **Cruise to L1** | C2: magnetometer boom deployment (roll). C3: halo insertion |
| 1 | Calibration with a "quiet" Sun | Science: calibration time vs. immediate data |
| 2 | **Minor CME** (tutorial of the alert mechanic) | — |
| 3 | Rising solar activity | Systems: deploy an extra radiator? |
| 4 | **Solar conjunction:** the spacecraft sits "behind" the Sun as seen from Earth, and there is 1 cycle of comms at 20% | Comms: store the data or compress it? |
| 5 | **Double CME** | Science: only one can be measured well. Which one? |
| 6 | **X-class flare: proton storm** | Everyone: preventive safe mode (−science, protects the spacecraft) or take the risk? |
| 7 | **🌋 THE GREAT STORM** (extreme event, Carrington-class) | See below |
| 8 | Post-storm recovery | Systems: repair damage |
| 9 | **Station-keeping order** | Director/Systems: propellant |
| 10 | **Finale:** the handover | See below |

### Cycle 7: the great storm (climax)
- Phase 1: detect it (coronagraph).
- Phase 2: measure it while it hits the spacecraft. When the protons arrive, stress goes up +20.
- Phase 3: warn Earth. The alert is worth ×10 lives protected.
- **The dilemma:** to measure, the instruments have to be on just when the radiation can burn them out. Shutting them down saves the spacecraft but loses the most important data of the mission.

### Spacecraft deck (Sun)
| Card | Level | Effect |
|---|---|---|
| Stray light | Minor | Coronagraph −30% (Science resolves it by recalibrating) |
| Solar heating | Minor | +10 °C on the avionics |
| SEU | Major | Reboot, 1 cycle in safe mode |
| Plasma analyzer saturation | Major | No in-situ measurement this cycle |
| Undeployed boom | Major | Magnetometer picks up spacecraft noise (−60%) |
| Radiation degradation | Major | −10% generation and −0.05 overall reliability |
| Memory latch-up | Critical | Stored data is lost, unless Comms has already downlinked it |
| Star tracker blinded | Critical | Loss of attitude: 2-cycle timer |

### End of mission: "The Handover"
NASA launches a successor that will reach L1 in cycle 10.
- **Decision:** pass the baton and shut the spacecraft down (clean ending, +20 points) or keep it as a backup (extended mission; requires propellant and stress < 60).
- If the spacecraft is badly damaged, Comms performs the **"last message"**: transmit everything stored in one final window.

### Lessons learned
- Why L1: constant view of the Sun, no eclipses.
- Radiation is cumulative: what you save today you pay for in cycle 7.
- Real-world connection: SOHO, ACE, DSCOVR, SWFO-L1.

---

## 🔭 MISSION 3: "Distant Worlds" (difficulty: advanced)

### Briefing
> *"Around other stars there are planets that might have atmospheres with water or methane. To see them, your telescope has to be colder than anything on Earth and stiller than a rock. At L2, 1.5 million km behind the Earth, anything that heats or moves the spacecraft ruins the observation."*

- **Budget:** $700M
- **Schedule:** 12 operating cycles (1 cycle = 1 month) + 4 cruise/cooldown cycles
- **Special mechanic: Mirror temperature.** The telescope only produces science below **−230 °C** (≈ 40 K). Every degree above that reduces quality.
- **Special mechanic: Scheduled transits.** Each planet has a fixed **transit window**, when it passes in front of its star. If the telescope is not pointed, cold and stable in that cycle, the transit is lost and does not come back for the rest of the match.

### CML 1: the question
| Question | Requirement |
|---|---|
| A. How many Earth-sized planets are there? | Precise photometry (lots of observing time) |
| B. What gases are in a planet's atmosphere? | IR spectroscopy (very cold) |
| C. Are there signs of water on a temperate planet? | B + extreme stability. Maximum score |

### CML 2: the orbit
| Orbit | Advantage | Disadvantage |
|---|---|---|
| Halo at L2 | Sun, Earth and Moon on the same side: a single thermal shield | 4-cycle cruise, weak signal |
| Earth-trailing | Thermally stable | Drifts farther every cycle: comms get worse over time |
| LEO (trap) | Cheap | The Earth heats the telescope. IR science impossible |

### Hangar particulars
- **The sunshield is the heart of the design:** it is very heavy and has to deploy without failures.
- **Cooling:** passive (shield + radiators, cheap but slow) or active cryocooler (cools fast, but **vibrates and draws 200 W**).
- **New components:**
  | Component | Mass | W | $M | Rel. | Cards |
  |---|---|---|---|---|---|
  | 1 m telescope | 250 | 50 | 150 | 0.93 | — |
  | 2 m telescope | 600 | 80 | 280 | 0.90 | Segment misalignment |
  | 3-layer sunshield | 80 | — | 40 | 0.90 | Shield tear |
  | 5-layer sunshield | 140 | — | 70 | 0.93 | Complex deployment |
  | Active cryocooler | 40 | 200 | 50 | 0.90 | Microvibrations |
  | IR spectrograph | 45 | 30 | 70 | 0.92 | — |
  | Precision photometer | 20 | 15 | 30 | 0.96 | — |
  | Reaction wheels ×4 | 40 | 60 | 15 | 0.90 | Wheel failure |
  | Reaction wheels ×6 (redundancy) | 60 | 80 | 22 | 0.95 | — |
  | Ka high-gain antenna | 25 | 60 | 18 | 0.94 | — |

### Personal missions (Exoplanets)
| Role | Mission | Condition |
|---|---|---|
| Science | **First light of a world** | Capture ≥ 3 of 5 transits; bonus if it includes the temperate planet |
| Systems | **The silence of the spacecraft** | Mirror < −230 °C and low vibration in every captured transit |
| Comms | **The great data dump** | Transmit ≥ 200 Gb (this mission generates huge amounts of data) |
| Director | **Perfect deployment** | Shield and mirror deployed without spending re-rolls |

### Cruise: "the days of terror" (4 cycles)
Inspired by the James Webb deployment: hundreds of mechanisms that all have to work.
| Cycle | Deployment | Roll |
|---|---|---|
| C1 | Panels + antenna | Normal |
| C2 | **Sunshield** | Hard. On a partial failure, the mirror never drops below −200 °C (science −50%) |
| C3 | **Secondary mirror + alignment** | Hard |
| C4 | L2 insertion + start of cooldown | Normal |
- Each failed roll can be retried by spending $15M and +5 stress, but it breaks the Director's personal mission.

### 12-cycle script
| Cycle | Fixed event | Key decision |
|---|---|---|
| 1 | **Cooldown** (passive: 2 cycles; cryocooler: 1) | Systems: turn on the cryocooler? Faster, but it vibrates |
| 2 | **Fine mirror alignment** | Science: roll; improves the quality of everything |
| 3 | 🪐 **Transit 1** (hot planet, easy) | Transit tutorial |
| 4 | Filler observations | Science: photometry or spectroscopy |
| 5 | 🪐 **Transit 2** + **micrometeoroid burst** | Everyone: turn the spacecraft to protect the mirror? The transit is lost |
| 6 | **Momentum saturation:** the wheels fill up | Systems: thruster desaturation (loses stability for 1 cycle) |
| 7 | 🪐 **Transit 3** (cloudy planet) | — |
| 8 | **DSN conflict** + recorder almost full | Comms: which data gets sacrificed? |
| 9 | 🪐 **Transit 4: THE TEMPERATE PLANET** (climax) | See below |
| 10 | **Cryocooler aging / helium leak** | Systems: keep it on until the end? |
| 11 | 🪐 **Transit 5** | — |
| 12 | **Finale:** the great data dump | See below |

### Cycle 9: the temperate planet (climax)
- Requires **everything at once**: mirror < −230 °C, cryocooler off (to avoid vibration) **or** a well-designed passive system, stable wheels, spectrograph on (30 W), recorder with free space and a DSN window reserved for cycle 10.
- The spacecraft plays **2 mandatory cards** this cycle, regardless of stress.
- **If captured with quality ≥ 80%:** "Possible water vapor detected" event (+100 points, unlocks the 🏆 ending).

### Spacecraft deck (Exoplanets)
| Card | Level | Effect |
|---|---|---|
| Microvibrations | Minor | −20% quality of the current transit |
| Mirror thermal drift | Minor | +5 °C |
| Pointing drift | Minor | Science recalibrates (roll) |
| Reaction wheel failure | Major | With 4 wheels: stability −40%. With 6: compensated |
| Segment misalignment | Major | Quality −30% until realigned (1 cycle) |
| Micrometeoroid hit on the mirror | Major | −10% permanent quality |
| Shield tear | Critical | +30 °C: the mirror warms up within 2 cycles |
| Cryogen leak | Critical | The cryocooler dies in 2 cycles |

### End of mission: "The Great Data Dump"
- Comms has 1 last cycle with all the DSN antennas (Goldstone, Madrid, Canberra). You must **prioritize** which data to downlink first if not everything fits.
- Prioritization mini-game: file queue, size vs. science value.
- **Director's final decision:** request an extended mission (if there is propellant to keep station and the shield is intact) or archive.

### Lessons learned
- Why IR telescopes go to L2: a single shield blocks the Sun, Earth and Moon.
- Vibration and heat are the enemies of precision.
- Science depends on timing: a missed transit does not repeat.
- Real-world connection: James Webb, Kepler, TESS, Roman, Ariel.

---

## 4. Progression between missions (campaign)
1. **Moon** unlocks **Sun**: teaches power, eclipses and data.
2. **Sun** unlocks **Exoplanets**: teaches radiation, thermal and alerts.
3. **Cross-mission achievements:**
   - *"Flawless engineering"*: finish a mission without forcing CML 4.
   - *"Against all odds"*: success with final stress > 85.
   - *"NASA saver"*: finish with > 30% of the budget left.
   - *"Iterator"*: go back to CML 3 twice and still achieve total success.

## 5. 1-player vs. 4-player mode
- **1 player:** controls all 4 roles. Each role still gets 1 action per cycle (4 actions in total) and all 4 personal missions are shown.
- **2 players:** Director + Science / Systems + Comms.
- **4 players:** each sees **only their own panel** and the global screen. You have to communicate by voice or chat. That is where the cooperative tension lies.

## 6. The bare minimum for the hackathon MVP
If time runs short, implement in this order:
1. **Moon mission only**, 1 player, 8 cycles.
2. Deck with 6 cards and stress.
3. Fixed events for cycles 3, 5 and 12.
4. Report with chain of causes.
5. Sun and Exoplanets are presented in the pitch as "designed content", with this document as evidence.
