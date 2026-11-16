# Ball Battles: 336px arena tournament

**Run date:** 2026-11-16  
**Ruleset:** final Bow/Hammer updates and Hammer parry behavior  
**Arena:** 336×336 (60% of the previous 560×560 width and height)  
**Roster:** 11 balls, 55 unique pairings  
**Sample:** 10 seeded fights per pairing, five starts from each side  
**Total:** 550 fights  
**Test cap:** 360 seconds per fight  
**Results:** 550 decisive finishes, 0 draws/timeouts

## Rules tested

- **Arena:** Square battle area reduced from 560×560 to 336×336 and kept centered on the canvas.
- **Bow:** Fires every 1.98 seconds at base cooldown (1.65 × 1.2). Starts each fight with 3 arrows per volley. Every landed arrow adds one arrow to future volleys. There is no upper volley cap.
- **Hammer:** Starts at spin speed 1. Current spin speed is its damage. It winds up at 1.0 spin-speed unit per second toward its maximum. Every successful hit increases maximum spin speed by 0.5, then resets current spin speed to 1 before winding up again. Hammer's own attacks cannot be parried. Hammer can parry other weapons, but its own rotation direction never reverses from a parry or weapon clash.
- **Lance:** Charges in the direction its weapon is pointing, starting at 16px/s and accelerating by 420px/s² to a 440px/s cap. Its weapon art is 1.28× size.
- **Typography:** The embedded Pixelify display font was removed. Interface text and canvas labels use a standard system sans-serif stack.

## Method

The tournament used the same `simulateOneMatchup` function as the game's Matchup Simulator, taken from the final `index.html` revision. Each unique unordered pair ran 10 deterministic seeded simulations. The starting side alternated, so each weapon started on the left five times and on the right five times in each pairing.

A fight still active at the simulator's 360-second cap would count as a draw. In this sample every one of the 550 fights ended before the cap. Results below are therefore wins out of 10, with no ties.

This is a deliberately small 10-run sample per pairing. It is useful for identifying large matchup imbalances and the effects of the new arena, but individual 10% or 20% differences can move substantially with a larger sample. The 336×336 arena also changes combat geometry materially, so these results should replace the older 560×560 tables rather than be directly averaged with them.

## Overall ranking

Each ball fought ten opponents ten times, for 100 fights per ball. Win rate is wins divided by 100.

| Rank | Ball | Wins / 100 | Win rate | Losses |
|---:|---|---:|---:|---:|
| 1 | Sword | 94 | 94% | 6 |
| 2 | Scythe | 87 | 87% | 13 |
| 3 | Lance | 76 | 76% | 24 |
| 4 | Duplicator | 72 | 72% | 28 |
| 5 | Hammer | 67 | 67% | 33 |
| 6 | Dagger | 51 | 51% | 49 |
| 7 | Chakram | 39 | 39% | 61 |
| 8 | Axe | 28 | 28% | 72 |
| 9 | Bow | 26 | 26% | 74 |
| 10 | Trident | 6 | 6% | 94 |
| 11 | Spear | 4 | 4% | 96 |

## Matchup matrix

Each cell is the row ball's wins out of 10 fights against the column ball, expressed as a percentage. Because there were no draws, the reciprocal cells sum to 100%.

| Ball | SWD | DAG | SPR | AXE | HAM | SCY | CHK | TRI | BOW | LNC | DUP |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 90 | 100 | 100 | 100 | 80 | 100 | 100 | 100 | 70 | 100 |
| Dagger | 10 | — | 100 | 100 | 0 | 0 | 100 | 100 | 100 | 0 | 0 |
| Spear | 0 | 0 | — | 0 | 0 | 0 | 0 | 40 | 0 | 0 | 0 |
| Axe | 0 | 0 | 100 | — | 0 | 0 | 20 | 100 | 40 | 0 | 20 |
| Hammer | 0 | 100 | 100 | 100 | — | 0 | 100 | 100 | 100 | 70 | 0 |
| Scythe | 20 | 100 | 100 | 100 | 100 | — | 100 | 100 | 100 | 70 | 80 |
| Chakram | 0 | 0 | 100 | 80 | 0 | 0 | — | 100 | 100 | 10 | 0 |
| Trident | 0 | 0 | 60 | 0 | 0 | 0 | 0 | — | 0 | 0 | 0 |
| Bow | 0 | 0 | 100 | 60 | 0 | 0 | 0 | 100 | — | 0 | 0 |
| Lance | 30 | 100 | 100 | 100 | 70 | 30 | 90 | 100 | 100 | — | 80 |
| Duplicator | 0 | 100 | 100 | 80 | 100 | 20 | 100 | 100 | 100 | 20 | — |

## All 55 pairings

Format: **A wins – B wins**, followed by average and median duration. A and B follow the order shown.

| Pairing | A–B wins | Avg. duration | Median |
|---|---:|---:|---:|
| Sword – Dagger | 9–1 | 77.9s | 79.1s |
| Sword – Spear | 10–0 | 52.7s | 58.1s |
| Sword – Axe | 10–0 | 63.2s | 66.7s |
| Sword – Hammer | 10–0 | 59.2s | 58.7s |
| Sword – Scythe | 6–4 | 56.5s | 58.3s |
| Sword – Chakram | 10–0 | 59.9s | 61.3s |
| Sword – Trident | 10–0 | 62.4s | 64.8s |
| Sword – Bow | 10–0 | 53.7s | 52.5s |
| Sword – Lance | 7–3 | 62.5s | 67.0s |
| Sword – Duplicator | 10–0 | 49.8s | 52.7s |
| Dagger – Spear | 10–0 | 154.6s | 146.0s |
| Dagger – Axe | 10–0 | 145.8s | 137.0s |
| Dagger – Hammer | 0–10 | 101.9s | 101.6s |
| Dagger – Scythe | 0–10 | 80.5s | 84.1s |
| Dagger – Chakram | 10–0 | 131.8s | 126.5s |
| Dagger – Trident | 10–0 | 137.6s | 136.3s |
| Dagger – Bow | 10–0 | 136.6s | 133.9s |
| Dagger – Lance | 0–10 | 87.4s | 89.8s |
| Dagger – Duplicator | 0–10 | 92.4s | 91.9s |
| Spear – Axe | 0–10 | 162.2s | 147.5s |
| Spear – Hammer | 0–10 | 109.5s | 103.5s |
| Spear – Scythe | 0–10 | 84.2s | 82.2s |
| Spear – Chakram | 0–10 | 175.0s | 171.2s |
| Spear – Trident | 4–6 | 169.8s | 167.4s |
| Spear – Bow | 0–10 | 219.4s | 226.3s |
| Spear – Lance | 0–10 | 119.8s | 119.4s |
| Spear – Duplicator | 0–10 | 100.3s | 91.3s |
| Axe – Hammer | 0–10 | 107.1s | 102.4s |
| Axe – Scythe | 0–10 | 76.6s | 76.5s |
| Axe – Chakram | 2–8 | 149.2s | 135.0s |
| Axe – Trident | 10–0 | 108.8s | 111.0s |
| Axe – Bow | 4–6 | 199.1s | 192.5s |
| Axe – Lance | 0–10 | 103.0s | 101.3s |
| Axe – Duplicator | 2–8 | 96.6s | 91.1s |
| Hammer – Scythe | 0–10 | 79.8s | 79.7s |
| Hammer – Chakram | 10–0 | 103.9s | 101.1s |
| Hammer – Trident | 10–0 | 95.1s | 97.0s |
| Hammer – Bow | 10–0 | 103.4s | 100.4s |
| Hammer – Lance | 7–3 | 104.5s | 104.2s |
| Hammer – Duplicator | 0–10 | 90.2s | 91.2s |
| Scythe – Chakram | 10–0 | 84.9s | 80.4s |
| Scythe – Trident | 10–0 | 72.3s | 74.2s |
| Scythe – Bow | 10–0 | 76.0s | 73.7s |
| Scythe – Lance | 7–3 | 84.1s | 87.2s |
| Scythe – Duplicator | 8–2 | 82.1s | 84.3s |
| Chakram – Trident | 10–0 | 154.9s | 158.4s |
| Chakram – Bow | 10–0 | 141.2s | 131.6s |
| Chakram – Lance | 1–9 | 120.1s | 119.1s |
| Chakram – Duplicator | 0–10 | 92.8s | 92.6s |
| Trident – Bow | 0–10 | 149.1s | 151.5s |
| Trident – Lance | 0–10 | 103.6s | 100.7s |
| Trident – Duplicator | 0–10 | 61.4s | 61.3s |
| Bow – Lance | 0–10 | 97.0s | 101.6s |
| Bow – Duplicator | 0–10 | 90.8s | 90.9s |
| Lance – Duplicator | 8–2 | 83.1s | 80.3s |

## Balance observations

- **Sword is the clear leader** in this compact arena, winning 94 of 100 fights. It swept eight opponents and went 6–4 against Scythe and 7–3 against Lance. This may be a consequence of the shorter engagement distances and faster fight tempo; it deserves another test before being nerfed based only on ten attempts per pair.
- **Scythe remains excellent** at 87 wins. Its poison pressure stays effective even in the smaller arena.
- **Lance is strong but no longer near-untouchable**, at 76 wins. Sword, Scythe, and Hammer each took multiple wins from it.
- **Hammer is competitive at 67 wins.** Its accelerated 1.0-per-second wind-up made it particularly effective against Dagger, Spear, Axe, Chakram, Trident, and Bow. It still loses 0–10 to Scythe and Duplicator. Its special parry rule was active during this tournament: its attacks cannot be parried, it can parry other weapons, and its rotation direction does not reverse.
- **Bow has improved to 26 wins**, including 10–0 against Spear and Trident and 6–4 against Axe. It still lost 10–0 to Sword, Dagger, Hammer, Scythe, Chakram, Lance, and Duplicator. Its uncapped volleys can create more projectiles over time, but its low direct matchup success suggests projectile reliability and survivability still need attention.
- **Spear and Trident are now the bottom two**, with only 4 and 6 wins respectively. They are consistently overwhelmed in the compact geometry.
- **No fights timed out.** The smaller arena shortened every matchup enough to produce a decisive result within the test cap.

Because this is only ten runs per pairing, treat close results as provisional. A larger 50- or 100-run tournament on the final 336×336 rules would be the next step before making major numerical balance changes.
