# Ball Battles balance simulation: 50 fights per pairing

**Date:** 2026-11-16  
**Source game file blob used for the run:** `b05550722f09eb182e2b2feb5820dda236e6abdf`

## Test method

- Used the game's actual deterministic `simulateOneMatchup(leftId, rightId, runIndex)` runner and its `step(1/60)` simulation loop from `index.html`. This was not a simplified damage or matchup model.
- Tested all 11 weapons against every other weapon: 55 unique unordered pairings.
- Ran 50 seeded fights per pairing, 2,750 total fights.
- The engine alternated starting sides by run index, giving each weapon 25 starts on each side in every pairing.
- The engine's 360-second per-fight simulation cap remained in place.
- **All 2,750 fights ended decisively. There were zero draws and zero timeouts.**
- Each weapon appeared in 10 pairings × 50 fights = 500 fights.

## Geometry and balance used

All armed weapon lengths are measured outward from the edge of the 60px diameter fighter ball. Melee attack and parry segments begin at the ball surface and extend outward by the listed reach; loaded art, fallback pixel art, and weapon icons use the same surface attachment. The Trident's whirlpool remains centered on its weapon tip. Bow arrows launch from the forward side of the orb. Duplicator intentionally has no weapon.

Spear starts with 36px of reach from the ball edge and gains **+3.6px per successful hit** (an 80% reduction from the prior +18px), plus +0.5 damage per hit. Its sprite shaft is **1.5× wider visually**; its attack and parry hitbox width remains unchanged.

## Overall ranking

| Rank | Weapon | Wins | Win rate |
|---:|---|---:|---:|
| 1 | Sword | 445 / 500 | 89.0% |
| 2 | Trident | 426 / 500 | 85.2% |
| 3 | Axe | 397 / 500 | 79.4% |
| 4 | Scythe | 324 / 500 | 64.8% |
| 5 | Spear | 263 / 500 | 52.6% |
| 6 | Lance | 254 / 500 | 50.8% |
| 7 | Duplicator | 212 / 500 | 42.4% |
| 8 | Hammer | 188 / 500 | 37.6% |
| 9 | Dagger | 150 / 500 | 30.0% |
| 10 | Chakram | 86 / 500 | 17.2% |
| 11 | Bow | 5 / 500 | 1.0% |

## Matchup win-rate matrix

Each cell is the row weapon's percentage of wins against the column weapon, based on 50 fights. Values are in 2% increments. Columns and rows are ordered Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, Duplicator.

| Weapon | Sword | Dagger | Spear | Axe | Hammer | Scythe | Chakram | Trident | Bow | Lance | Duplicator |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 96 | 96 | 64 | 100 | 96 | 96 | 48 | 100 | 94 | 100 |
| Dagger | 4 | — | 42 | 24 | 2 | 0 | 92 | 2 | 100 | 28 | 6 |
| Spear | 4 | 58 | — | 32 | 72 | 32 | 68 | 20 | 94 | 48 | 98 |
| Axe | 36 | 76 | 68 | — | 96 | 96 | 88 | 58 | 100 | 76 | 100 |
| Hammer | 0 | 98 | 28 | 4 | — | 0 | 100 | 0 | 100 | 46 | 0 |
| Scythe | 4 | 100 | 68 | 4 | 100 | — | 98 | 4 | 100 | 74 | 96 |
| Chakram | 4 | 8 | 32 | 12 | 0 | 2 | — | 0 | 100 | 14 | 0 |
| Trident | 52 | 98 | 80 | 42 | 100 | 96 | 100 | — | 100 | 84 | 100 |
| Bow | 0 | 0 | 6 | 0 | 0 | 0 | 0 | 0 | — | 4 | 0 |
| Lance | 6 | 72 | 52 | 24 | 54 | 26 | 86 | 16 | 96 | — | 76 |
| Duplicator | 0 | 94 | 2 | 0 | 100 | 4 | 100 | 0 | 100 | 24 | — |

## Pair-by-pair results and durations

Wins are shown as **first-listed weapon wins – second-listed weapon wins**. Durations are fight-level averages and medians across all 50 runs in that pairing.

| Pairing | Wins (A–B) | Average (s) | Median (s) |
|---|---:|---:|---:|
| Sword–Dagger | 48–2 | 60.21 | 57.42 |
| Sword–Spear | 48–2 | 45.33 | 44.42 |
| Sword–Axe | 32–18 | 44.14 | 41.52 |
| Sword–Hammer | 50–0 | 49.42 | 49.03 |
| Sword–Scythe | 48–2 | 45.19 | 45.44 |
| Sword–Chakram | 48–2 | 60.47 | 59.00 |
| Sword–Trident | 24–26 | 45.38 | 44.97 |
| Sword–Bow | 50–0 | 48.35 | 49.05 |
| Sword–Lance | 47–3 | 56.08 | 53.17 |
| Sword–Duplicator | 50–0 | 44.02 | 42.72 |
| Dagger–Spear | 21–29 | 92.55 | 97.78 |
| Dagger–Axe | 12–38 | 78.85 | 71.83 |
| Dagger–Hammer | 1–49 | 95.50 | 93.13 |
| Dagger–Scythe | 0–50 | 80.07 | 79.52 |
| Dagger–Chakram | 46–4 | 109.13 | 106.87 |
| Dagger–Trident | 1–49 | 63.09 | 58.28 |
| Dagger–Bow | 50–0 | 108.03 | 106.95 |
| Dagger–Lance | 14–36 | 102.61 | 103.07 |
| Dagger–Duplicator | 3–47 | 91.88 | 90.33 |
| Spear–Axe | 16–34 | 57.03 | 56.17 |
| Spear–Hammer | 36–14 | 79.69 | 82.57 |
| Spear–Scythe | 16–34 | 63.83 | 64.72 |
| Spear–Chakram | 34–16 | 102.68 | 96.24 |
| Spear–Trident | 10–40 | 53.47 | 53.70 |
| Spear–Bow | 47–3 | 94.87 | 88.97 |
| Spear–Lance | 24–26 | 83.57 | 85.01 |
| Spear–Duplicator | 49–1 | 70.08 | 69.08 |
| Axe–Hammer | 48–2 | 63.14 | 61.19 |
| Axe–Scythe | 48–2 | 49.74 | 50.60 |
| Axe–Chakram | 44–6 | 76.86 | 71.92 |
| Axe–Trident | 29–21 | 48.70 | 47.86 |
| Axe–Bow | 50–0 | 68.46 | 65.24 |
| Axe–Lance | 38–12 | 72.30 | 71.01 |
| Axe–Duplicator | 50–0 | 47.88 | 46.72 |
| Hammer–Scythe | 0–50 | 69.12 | 68.18 |
| Hammer–Chakram | 50–0 | 97.96 | 95.45 |
| Hammer–Trident | 0–50 | 55.86 | 54.62 |
| Hammer–Bow | 50–0 | 91.70 | 89.64 |
| Hammer–Lance | 23–27 | 85.86 | 89.76 |
| Hammer–Duplicator | 0–50 | 93.24 | 90.90 |
| Scythe–Chakram | 49–1 | 76.62 | 74.08 |
| Scythe–Trident | 2–48 | 47.52 | 48.18 |
| Scythe–Bow | 50–0 | 69.20 | 68.21 |
| Scythe–Lance | 37–13 | 78.57 | 77.27 |
| Scythe–Duplicator | 48–2 | 69.71 | 68.94 |
| Chakram–Trident | 0–50 | 58.57 | 54.22 |
| Chakram–Bow | 50–0 | 123.58 | 116.20 |
| Chakram–Lance | 7–43 | 108.03 | 108.74 |
| Chakram–Duplicator | 0–50 | 92.62 | 89.86 |
| Trident–Bow | 50–0 | 54.58 | 54.46 |
| Trident–Lance | 42–8 | 63.47 | 63.25 |
| Trident–Duplicator | 50–0 | 49.47 | 49.07 |
| Bow–Lance | 2–48 | 103.32 | 96.89 |
| Bow–Duplicator | 0–50 | 94.31 | 90.82 |
| Lance–Duplicator | 38–12 | 86.99 | 87.66 |

## Findings

- **Sword leads at 89.0%** and won 48/50 against Dagger, Spear, Scythe, and Chakram, 47/50 against Lance, and 50/50 against Hammer, Bow, and Duplicator. It split with Trident (24–26).
- **Trident is second at 85.2%**. It beat Spear 40–10, Scythe 48–2, and Lance 42–8. It lost 24–26 to Sword and 21–29 to Axe.
- **Axe is third at 79.4%**. It won 38–12 against Lance and 29–21 against Trident, and swept Bow and Duplicator 50–0.
- **Spear is now near the middle at 52.6%**. It beat Hammer 36–14, Chakram 34–16, and Duplicator 49–1, but lost to Trident 10–40, Axe 16–34, and Scythe 16–34. Its 80% slower reach growth prevents the former runaway scaling.
- **Bow remains the clear outlier at 1.0%**: five wins in 500 fights (three against Spear and two against Lance), and no wins in its other eight matchups. Faster arrows and the shorter cooldown are not enough to make it competitive in this arena.
- The field is still top-heavy: Sword, Trident, and Axe are above 79%; Spear and Lance are closest to even; Chakram is at 17.2%, and Bow at 1.0%.

**Overall fight duration:** average 73.14 seconds, median 68.80 seconds, longest 243.47 seconds. No fight reached the 360-second cap.
