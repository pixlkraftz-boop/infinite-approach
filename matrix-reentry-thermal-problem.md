# LOCKED SYSTEM MATRIX — Why Reentry Is a Thermal Problem Not a Speed Problem
**Skill 1 output · Source class: documented real-world system (canonical physics) · Serves locked package from Skill 0 (GREENLIGHT 44/50)**

---

## 1. ENGINE STATEMENT

A returning spacecraft is an energy disposal problem. Orbital velocity stores roughly thirty megajoules per kilogram, the atmosphere is the only brake available, and survival depends on forcing that energy to convert into heat inside the air instead of inside the vehicle.

---

## 2. MODULE TABLE

| # | Module | Mechanism (systemic) | Inputs → Outputs | Failure mode | Layout architecture | Accent role |
|---|---|---|---|---|---|---|
| M1 | The Energy Ledger | Kinetic energy scales with the square of velocity. At orbital speed every kilogram of vehicle carries ~30 megajoules — about twice the energy needed to vaporize that kilogram if it were aluminium. The energy cannot be cancelled, only relocated. | velocity, mass → stored kinetic energy total | Treating reentry as a braking problem instead of an energy-routing problem | Live Terminal Code Matrix (the half m v squared relationship resolving live) | Cyan on the velocity term · Red on the resolved energy total |
| M2 | The Compression Wall | At hypersonic speed, air cannot move aside fast enough. It piles up and compresses violently ahead of the vehicle, forming a detached bow shock. Heating is compression-driven, not friction-driven — the common intuition is wrong. | velocity + air density → shock layer, extreme gas temperature | Misattributing heating to friction leads to wrong design instincts (sharp noses) | Split-Screen Mechanical Node Diagram (vehicle node vs incoming air column) | Red on the shock layer · Cyan on diverted flow lines |
| M3 | The Energy Partition | The shock layer becomes the disposal route. The vast majority of converted heat is carried away in the air flowing past; only a small fraction conducts into the vehicle. The entire engineering problem is minimising that fraction. | shock layer heat → air-stream share vs vehicle share | The vehicle share rising beyond what the structure can absorb | 3-Column Bento Grid (total energy / share into air / share into vehicle) | Amber on the vehicle-share column — the limiting quantity |
| M4 | The Entry Corridor | Entry angle sets the trade. Too steep concentrates the energy conversion into too little time — heating and deceleration spike beyond limits. Too shallow and the vehicle skips off the atmosphere or decays slowly through repeated heating. Survival exists only inside a narrow corridor. | entry angle, velocity → heating rate over time profile | Steep: structural/thermal overload. Shallow: skip-out or prolonged heat soak | Linear Vector Timeline (altitude–velocity trajectory with corridor band) | Amber corridor boundaries · Red zones outside the band |
| M5 | The Blunt Body Paradox | A sharp nose attaches the shock to the surface and feeds heat straight into the structure. A blunt face pushes the shock off the body, holding the hottest gas at a standoff distance so the air keeps the heat. The survivable shape is the unintuitive one. | body geometry → shock standoff distance → vehicle heat share | Sharp-body intuition: minimising drag maximises heat transfer into the structure | Split-Screen Mechanical Node Diagram (sharp body vs blunt body, shock geometry compared) | Cyan on the blunt-body standoff gap · Red on the sharp-body attached shock |
| M6 | Disposal Strategies | Thermal protection systems are energy disposal mechanisms, not shields. Ablators sacrifice material, carrying heat away as the surface chars and erodes. Insulating tiles refuse conduction and re-radiate heat back to the air. Both are ways of routing energy off the vehicle. | vehicle heat share → ablation mass loss / re-radiated flux | Ablator depletion before velocity is shed; tile damage opening a conduction path | 3-Column Bento Grid (ablative / insulating-radiative / heat-sink strategies) | Amber on the depletion margin · Cyan on rejected heat paths |

All six modules map to canonical layout architectures. No module cut.

---

## 3. PHASE SEQUENCE

| Phase | Modules | Loop function | Narrative job |
|---|---|---|---|
| P1 — The Ledger | M1 | **OPEN (cold open loop)** | State the impossible arithmetic: the vehicle carries roughly twice its own vaporization energy. The loop: how does anything survive this? |
| P2 — The Wall | M2 | Escalate | The brake is a wall of air that cannot get out of the way. Kill the friction misconception. Stakes rise: the brake itself is the furnace. |
| P3 — The Partition | M3 | Escalate + **FORESHADOW one third** | Reveal the real game: the question is never whether the energy converts, only where the heat ends up. Foreshadow line: the answer will turn out to be the opposite of every intuition about speed. |
| P4 — The Corridor | M4 | Obstacle | Even with the partition understood, the time profile can kill. The corridor shows survival as a narrow band, not a solved problem. |
| P5 — The Paradox | M5 | **FORESHADOW two thirds → pivot** | The blunt body reveal. The shape that looks wrong is the shape that lives. Standoff distance is the mechanism that makes the partition winnable. |
| P6 — The Disposal | M6 | **CLOSE (grand payoff)** | Close the cold open loop: the vehicle survives by refusing the energy — giving it to the atmosphere through geometry and sacrifice. Reentry was never about surviving heat. It was about routing it. |

The cold open loop (P1) closes in the final third (P6), foreshadowed at P3 and P5, satisfying loop discipline.

---

## 4. SOURCE LEDGER

**Source class:** canonical aerospace physics and engineering history. No supplied text; deconstruction draws on canonical knowledge.

| Claim | Status |
|---|---|
| Low Earth orbital velocity approximately seven point eight kilometres per second | VERIFIED canonical |
| Kinetic energy at that velocity approximately thirty megajoules per kilogram | VERIFIED (half × 7,800² ≈ 30.4 MJ/kg) |
| "Roughly twice the energy needed to vaporize aluminium" | PLAUSIBLE HEURISTIC — aluminium total ≈ 13–14 MJ/kg from ambient; ratio ≈ 2.2×. Soften to "roughly twice" or verify before voiceover |
| Heating is compression-driven, not friction-driven | VERIFIED canonical |
| Shock-layer gas temperatures (thousands of kelvin; higher for lunar-return speeds) | NEEDS CHECK — exact figures vary by entry profile; verify any specific temperature before voiceover |
| Majority of heat carried away by the shock layer for blunt bodies; small fraction into vehicle | PLAUSIBLE HEURISTIC — widely cited; exact percentage NEEDS CHECK, avoid a precise figure unless verified |
| Blunt body theory: H. Julian Allen (with Alfred Eggers), NACA, early nineteen fifties | VERIFIED canonical — exact year NEEDS CHECK if stated |
| Skip-out at shallow entry angles; lunar-return corridor narrowness | VERIFIED canonical concept — any quoted corridor width in degrees NEEDS CHECK |
| Apollo used ablative Avcoat; Shuttle used insulating silica tiles | VERIFIED canonical |

**Carry-forward instruction for Skill 2:** every NEEDS CHECK item above must appear in the script's pre-flagged factual claims list. Prefer soft quantities ("thousands of degrees", "a narrow band") over precise figures unless verified — audio is the most expensive layer to re-render.

---

**MATRIX LOCKED.** One matrix per greenlit package. Skill 2 scripts from this document only.
