# Ball Battles balance simulation: 48px Spear

**Run date:** 2026-11-16  
**Game code blob:** `286f62aca27c4ee64cb8f4d8075356132ff94e96` (the combat code tested in this run)  
**Arena:** 336×336  
**Method:** the game's actual `simulateOneMatchup(leftId, rightId, runIndex)` engine; deterministic seeded runs; starting sides alternated.

## Configuration tested

- **Spear:** starts at 48px reach, half the regular weapons' 96px starting reach. Each hit adds 50% of that starting length (+24px) and +0.5 damage. Hit-based length growth is uncapped.
- **Trident:** whirlpool radius remains fixed at 165px. Each hit adds +0.5 damage and +35 pull strength.
- Each fighter starts with 100 HP. No persistent training upgrades are applied in the tournament.

## Tournament totals

- 11 weapons, 55 unique pairings, 10 fights per pairing.
- **550 fights completed.**
- **0 draws and 0 timeouts** (the simulator's 360-second cap was not reached).
- Each pairing used five starts from each side.

## Overall ranking

| Rank | Weapon | Wins / 100 | Losses | Win rate |
|---:|---|---:|---:|---:|
| 1 | Spear | 89 | 11 | 89% |
| 2 | Trident | 84 | 16 | 84% |
| 3 | Sword | 83 | 17 | 83% |
| 4 | Scythe | 68 | 32 | 68% |
| 5 | Lance | 60 | 40 | 60% |
| 6 | Duplicator | 52 | 48 | 52% |
| 7 | Hammer | 47 | 53 | 47% |
| 8 | Dagger | 31 | 69 | 31% |
| 9 | Chakram | 22 | 78 | 22% |
| 10 | Axe | 8 | 92 | 8% |
| 11 | Bow | 6 | 94 | 6% |

Each weapon fought 10 opponents 10 times each, for 100 fights per weapon.

## Matchup win-rate matrix

Each cell is the row weapon's win percentage against the column weapon, based on 10 fights. A dash marks the diagonal.

| Weapon | Sword | Dagger | Spear | Axe | Hammer | Scythe | Chakram | Trident | Bow | Lance | Duplicator |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 90% | 30% | 100% | 100% | 80% | 100% | 60% | 100% | 70% | 100% |
| Dagger | 10% | — | 0% | 100% | 0% | 0% | 100% | 0% | 100% | 0% | 0% |
| Spear | 70% | 100% | — | 100% | 100% | 100% | 70% | 60% | 100% | 90% | 100% |
| Axe | 0% | 0% | 0% | — | 0% | 0% | 20% | 0% | 40% | 0% | 20% |
| Hammer | 0% | 100% | 0% | 100% | — | 0% | 100% | 0% | 100% | 70% | 0% |
| Scythe | 20% | 100% | 0% | 100% | 100% | — | 100% | 10% | 100% | 70% | 80% |
| Chakram | 0% | 0% | 30% | 80% | 0% | 0% | — | 0% | 100% | 10% | 0% |
| Trident | 40% | 100% | 40% | 100% | 100% | 90% | 100% | — | 100% | 70% | 100% |
| Bow | 0% | 0% | 0% | 60% | 0% | 0% | 0% | 0% | — | 0% | 0% |
| Lance | 30% | 100% | 10% | 100% | 30% | 30% | 90% | 30% | 100% | — | 80% |
| Duplicator | 0% | 100% | 0% | 80% | 100% | 20% | 100% | 0% | 100% | 20% | — |

## Individual matchup results

The win column is shown from the first weapon's perspective. Durations include all 10 fights in the pairing.

| Matchup | Wins | Average fight | Median fight |
|---|---:|---:|---:|
| Sword vs Dagger | 9–1 | 77.92s | 79.12s |
| Sword vs Spear | 3–7 | 48.94s | 48.42s |
| Sword vs Axe | 10–0 | 63.18s | 66.67s |
| Sword vs Hammer | 10–0 | 59.16s | 58.72s |
| Sword vs Scythe | 8–2 | 56.53s | 58.33s |
| Sword vs Chakram | 10–0 | 59.86s | 61.35s |
| Sword vs Trident | 6–4 | 57.58s | 58.38s |
| Sword vs Bow | 10–0 | 53.65s | 52.48s |
| Sword vs Lance | 7–3 | 62.48s | 66.97s |
| Sword vs Duplicator | 10–0 | 49.82s | 52.70s |
| Dagger vs Spear | 0–10 | 79.09s | 75.68s |
| Dagger vs Axe | 10–0 | 145.75s | 136.98s |
| Dagger vs Hammer | 0–10 | 101.87s | 101.63s |
| Dagger vs Scythe | 0–10 | 80.48s | 84.07s |
| Dagger vs Chakram | 10–0 | 131.79s | 126.52s |
| Dagger vs Trident | 0–10 | 71.16s | 70.48s |
| Dagger vs Bow | 10–0 | 136.58s | 133.92s |
| Dagger vs Lance | 0–10 | 87.42s | 89.85s |
| Dagger vs Duplicator | 0–10 | 92.42s | 91.88s |
| Spear vs Axe | 10–0 | 57.02s | 57.70s |
| Spear vs Hammer | 10–0 | 58.57s | 63.17s |
| Spear vs Scythe | 10–0 | 56.18s | 62.10s |
| Spear vs Chakram | 7–3 | 95.22s | 100.05s |
| Spear vs Trident | 6–4 | 53.50s | 52.32s |
| Spear vs Bow | 10–0 | 66.70s | 69.50s |
| Spear vs Lance | 9–1 | 70.37s | 77.53s |
| Spear vs Duplicator | 10–0 | 51.92s | 51.33s |
| Axe vs Hammer | 0–10 | 107.11s | 102.38s |
| Axe vs Scythe | 0–10 | 76.62s | 76.55s |
| Axe vs Chakram | 2–8 | 149.24s | 135.02s |
| Axe vs Trident | 0–10 | 69.86s | 74.13s |
| Axe vs Bow | 4–6 | 199.12s | 192.50s |
| Axe vs Lance | 0–10 | 103.00s | 101.33s |
| Axe vs Duplicator | 2–8 | 96.56s | 91.15s |
| Hammer vs Scythe | 0–10 | 79.83s | 79.70s |
| Hammer vs Chakram | 10–0 | 103.91s | 101.15s |
| Hammer vs Trident | 0–10 | 62.83s | 65.78s |
| Hammer vs Bow | 10–0 | 103.35s | 100.38s |
| Hammer vs Lance | 7–3 | 104.46s | 104.23s |
| Hammer vs Duplicator | 0–10 | 90.23s | 91.18s |
| Scythe vs Chakram | 10–0 | 84.88s | 80.45s |
| Scythe vs Trident | 1–9 | 59.97s | 59.73s |
| Scythe vs Bow | 10–0 | 75.98s | 73.75s |
| Scythe vs Lance | 7–3 | 84.14s | 87.23s |
| Scythe vs Duplicator | 8–2 | 82.15s | 84.28s |
| Chakram vs Trident | 0–10 | 65.60s | 59.38s |
| Chakram vs Bow | 10–0 | 141.25s | 131.57s |
| Chakram vs Lance | 1–9 | 120.09s | 119.12s |
| Chakram vs Duplicator | 0–10 | 92.84s | 92.60s |
| Trident vs Bow | 10–0 | 64.10s | 63.40s |
| Trident vs Lance | 7–3 | 77.32s | 79.77s |
| Trident vs Duplicator | 10–0 | 54.19s | 55.87s |
| Bow vs Lance | 0–10 | 96.98s | 101.60s |
| Bow vs Duplicator | 0–10 | 90.84s | 90.87s |
| Lance vs Duplicator | 8–2 | 83.07s | 80.27s |

## Readout

Spear leads at **89%**, despite starting at only 48px. Its +24px reach and +0.5 damage gains per hit make it extremely strong once it lands early hits. It won 10–0 against six opponents and 9–1 against Lance, but lost 3–7 to Sword, 3–7 to Chakram, and 4–6 to Trident.

Trident finished second at **84%**. Its fixed-radius whirlpool plus +35 pull strength and +0.5 damage per hit proved very effective. It beat Dagger, Axe, Hammer, Chakram, Bow, and Duplicator 10–0, while losing 4–6 to Sword and Spear, 1–9 to Scythe, and 3–7 to Lance.

Sword remained close behind at **83%**. The sharpest balance warning is the concentration of wins at the top: Spear and Trident both beat most of the field consistently. Bow (6%), Axe (8%), and Chakram (22%) had particularly low results in this sample.

The previous 336×336 baseline used the prior Spear and Trident growth rules with the same 10-fight-per-pair format. This result is directly comparable in methodology, but 10 fights per pairing is still a small sample. Treat the percentages as directional balance evidence rather than precise long-run probabilities.
