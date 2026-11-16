# Ball Battles balance update: Bow, Hammer, and Lance

**Run date:** 2026-11-16  
**Code revision:** `834f231`  
**Matrix/documentation revision:** `282d0c2`  
**Arena:** 560×560  
**Roster:** 11 balls, 55 unique pairings  
**Sample:** 50 seeded fights per pairing, 25 starts from each side  
**Blended total:** 2,750 fights  
**New tests:** 1,350 fights across 27 affected pairings  
**Test cap:** 360 seconds per fight

## Changes tested

- **Bow:** Moved the rendered bow outward so its grip is beyond the ball's front edge. Increased the on-screen arrow size. These are presentation changes; Bow's hit damage and firing cadence were not buffed.
- **Hammer:** Starts at spin speed 1. Its current spin speed is also its hit damage. Every hit increases maximum spin speed by 0.5 and resets current speed to 1. It then winds up toward its new maximum. The wind-up rate is 0.5 speed units per second.
- **Lance:** Charge direction is captured from the angle the weapon is pointing when the charge begins. Charge speed starts at 16px/s and accelerates at 420px/s² to a cap of 440px/s. The Lance sprite is rendered at 1.28× scale; this changes the art size, not the collision reach.

## Method and sample scope

The same `simulateOneMatchup` function used by the in-game Matchup Simulator was run directly from the current `index.html` code. Each run uses the engine's deterministic matchup seed. Starting sides alternate, giving each weapon 25 starts on the left and 25 on the right within every 50-fight pairing.

All 27 unique pairings containing at least one of Bow, Hammer, or Lance were rerun after the changes: **1,350 seeded fights**. A fight still active at 360 seconds is a timeout/draw. The updated pairings had **173 timeouts** and **1,177 decisive finishes**.

The remaining 28 pairings do not include Bow, Hammer, or Lance, so their prior 50-fight results were carried forward from the full-roster baseline report. That contributes 1,400 fights and 130 timeouts. The combined matrix therefore represents **2,750 fights, 2,447 decisive finishes, and 303 draws/timeouts**.

This is a mixed-revision matrix by design: only pairings affected by these weapon changes were rerun. The unchanged 28 pairings were not redundantly simulated. Matrix percentages are wins out of all 50 fights in each pairing, so draws remain part of the denominator. Average and median fight durations below use decisive finishes only.

## Overall results

Every weapon appears in 500 pairings across the combined matrix: 50 fights against each of the other ten weapons. Draw counts below are the number of drawn fights in that weapon's ten pairings.

| Rank | Ball | Wins / 500 | Win rate | Draws / 500 |
|---:|---|---:|---:|---:|
| 1 | Scythe | 458 | 91.6% | 0 |
| 2 | Lance | 433 | 86.6% | 0 |
| 3 | Sword | 432 | 86.4% | 10 |
| 4 | Duplicator | 279 | 55.8% | 32 |
| 5 | Hammer | 250 | 50.0% | 53 |
| 6 | Dagger | 210 | 42.0% | 76 |
| 7 | Axe | 152 | 30.4% | 75 |
| 8 | Chakram | 151 | 30.2% | 85 |
| 9 | Trident | 57 | 11.4% | 29 |
| 10 | Spear | 23 | 4.6% | 119 |
| 11 | Bow | 2 | 0.4% | 127 |

## Current matchup matrix

Each cell is the row ball's wins out of 50 fights against the column ball. Remaining fights were won by the opponent or ended as draws.

| Ball | SWD | DAG | SPR | AXE | HAM | SCY | CHK | TRI | BOW | LNC | DUP |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 86 | 100 | 98 | 98 | 44 | 84 | 100 | 100 | 54 | 100 |
| Dagger | 4 | — | 62 | 80 | 12 | 0 | 72 | 94 | 74 | 2 | 20 |
| Spear | 0 | 0 | — | 0 | 2 | 0 | 0 | 40 | 4 | 0 | 0 |
| Axe | 0 | 2 | 78 | — | 2 | 0 | 12 | 100 | 60 | 0 | 50 |
| Hammer | 2 | 64 | 82 | 74 | — | 0 | 72 | 100 | 86 | 16 | 4 |
| Scythe | 56 | 100 | 100 | 100 | 100 | — | 100 | 100 | 100 | 60 | 100 |
| Chakram | 8 | 8 | 62 | 52 | 10 | 0 | — | 90 | 66 | 0 | 6 |
| Trident | 0 | 4 | 40 | 0 | 0 | 0 | 6 | — | 64 | 0 | 0 |
| Bow | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 4 | — | 0 | 0 |
| Lance | 46 | 98 | 100 | 100 | 84 | 40 | 100 | 100 | 100 | — | 98 |
| Duplicator | 0 | 66 | 92 | 42 | 86 | 0 | 82 | 100 | 88 | 2 | — |

## Updated pair-by-pair results

Format: **A wins – B wins – draws**, followed by average and median duration among decisive finishes. A and B follow the order shown.

| Pairing | A–B–Draws | Avg. decisive time | Median |
|---|---:|---:|---:|
| Sword – Hammer | 49–1–0 | 116.5s | 110.7s |
| Sword – Bow | 50–0–0 | 104.5s | 104.3s |
| Sword – Lance | 27–23–0 | 135.9s | 134.2s |
| Dagger – Hammer | 6–32–12 | 220.8s | 206.2s |
| Dagger – Bow | 37–0–13 | 252.2s | 232.9s |
| Dagger – Lance | 1–49–0 | 201.0s | 187.5s |
| Spear – Hammer | 1–41–8 | 223.9s | 220.8s |
| Spear – Bow | 2–0–48 | 343.8s | 354.9s |
| Spear – Lance | 0–50–0 | 184.8s | 174.7s |
| Axe – Hammer | 1–37–12 | 223.9s | 200.7s |
| Axe – Bow | 30–0–20 | 273.6s | 283.8s |
| Axe – Lance | 0–50–0 | 179.6s | 182.7s |
| Hammer – Scythe | 0–50–0 | 105.5s | 104.9s |
| Hammer – Chakram | 36–5–9 | 230.7s | 218.4s |
| Hammer – Trident | 50–0–0 | 197.8s | 193.7s |
| Hammer – Bow | 43–0–7 | 217.0s | 208.5s |
| Hammer – Lance | 8–42–0 | 174.2s | 175.4s |
| Hammer – Duplicator | 2–43–5 | 168.4s | 152.8s |
| Scythe – Bow | 50–0–0 | 111.7s | 110.4s |
| Scythe – Lance | 30–20–0 | 136.6s | 136.7s |
| Chakram – Bow | 33–0–17 | 256.6s | 250.1s |
| Chakram – Lance | 0–50–0 | 172.3s | 155.1s |
| Trident – Bow | 32–2–16 | 316.3s | 324.9s |
| Trident – Lance | 0–50–0 | 159.7s | 155.0s |
| Bow – Lance | 0–50–0 | 186.8s | 183.6s |
| Bow – Duplicator | 0–44–6 | 171.0s | 151.0s |
| Lance – Duplicator | 49–1–0 | 125.2s | 123.6s |

## Balance read

- **Hammer is now viable.** It went from 42 wins in the old 500-fight sample (8.4%) to 250/500 (50.0%) in the blended matrix. Its new damage ramp matters: it won 36–5 against Chakram, 50–0 against Trident, and 43–0 against Bow. It still loses to Scythe and Lance, and Duplicator is a hard counter.
- **Lance remains one of the top performers, but it is no longer an automatic winner.** It now has 86.6% wins overall. The new charge loses 23–27 to Sword and 20–30 to Scythe, and Hammer takes 8 wins from it. It still wins decisively against most of the remaining field.
- **Bow remains critically underpowered.** The visual changes make its model and arrows clearer, but do not improve its damage or projectile reliability. It won only 2/500 overall and timed out 127 times. Spear–Bow still drew 48/50 fights, showing that this is partly a finishing/reliability issue rather than only raw damage.
- **Scythe is still the overall leader** at 91.6%, slightly ahead of Lance and Sword. The bigger balance issue now is the gap between the top three and the bottom group, especially Bow and Spear.
- **Draws remain material.** The 303 timeouts account for 11.0% of the combined sample. Bow and Spear are involved in a disproportionate share of stalemates.

The next balance pass should focus on Bow's ability to land and finish with arrows, and then Spear's ability to break stalemates. Hammer's new spin-damage loop has corrected its previous low win rate; I would not weaken it based on this sample alone.
