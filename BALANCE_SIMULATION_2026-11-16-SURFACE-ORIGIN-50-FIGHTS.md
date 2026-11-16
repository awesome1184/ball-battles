# Ball Battles balance simulation: 50 fights per pairing

**Date:** 2026-11-16  
**Source game file blob used for the run:** `9687e253c993c3abff824eab530b9aa48c468c27`

## Test method

- Used the game's actual deterministic `simulateOneMatchup(leftId, rightId, runIndex)` runner and its `step(1/60)` simulation loop from `index.html`. This was not a simplified damage or matchup model.
- Tested all 11 weapons against every other weapon: 55 unique unordered pairings.
- Ran 50 seeded fights per pairing, 2,750 total fights.
- The engine alternated starting sides by run index, giving each weapon 25 starts on each side in every pairing.
- The engine's 360-second per-fight simulation cap remained in place.
- **All 2,750 fights ended decisively. There were zero draws and zero timeouts.**
- Each weapon appeared in 10 pairings × 50 fights = 500 fights.

## Geometry and balance used

All armed weapon lengths are now measured outward from the edge of the 60px diameter fighter ball. Melee attack and parry segments begin at the ball surface and extend outward by the listed reach; loaded art, fallback pixel art, and weapon icons use the same surface attachment. The Trident's whirlpool remains centered at its weapon tip. Bow arrows still launch from the forward side of the orb. Duplicator intentionally has no weapon.

Spear's reach is 36px from the ball edge and gains **+3.6px per successful hit** (down 80% from the previous +18px), plus +0.5 damage per hit. Its shaft is 1.5× wider in the sprite and hitbox.

## Overall ranking

| Rank | Weapon | Wins | Win rate |
|---:|---|---:|---:|
| 1 | Sword | 446 / 500 | 89.2% |
| 2 | Trident | 427 / 500 | 85.4% |
| 3 | Axe | 397 / 500 | 79.4% |
| 4 | Scythe | 323 / 500 | 64.6% |
| 5 | Spear | 280 / 500 | 56.0% |
| 6 | Lance | 256 / 500 | 51.2% |
| 7 | Duplicator | 211 / 500 | 42.2% |
| 8 | Hammer | 185 / 500 | 37.0% |
| 9 | Dagger | 142 / 500 | 28.4% |
| 10 | Chakram | 80 / 500 | 16.0% |
| 11 | Bow | 3 / 500 | 0.6% |

## Matchup win-rate matrix

Each cell is the row weapon's percentage of wins against the column weapon, based on 50 fights. Values are in 2% increments. Columns and rows are ordered Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, Duplicator.

| Weapon | Sword | Dagger | Spear | Axe | Hammer | Scythe | Chakram | Trident | Bow | Lance | Duplicator |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 96 | 98 | 64 | 100 | 96 | 96 | 48 | 100 | 94 | 100 |
| Dagger | 4 | — | 26 | 24 | 2 | 0 | 92 | 2 | 100 | 28 | 6 |
| Spear | 2 | 74 | — | 32 | 78 | 34 | 80 | 18 | 98 | 44 | 100 |
| Axe | 36 | 76 | 68 | — | 96 | 96 | 88 | 58 | 100 | 76 | 100 |
| Hammer | 0 | 98 | 22 | 4 | — | 0 | 100 | 0 | 100 | 46 | 0 |
| Scythe | 4 | 100 | 66 | 4 | 100 | — | 98 | 4 | 100 | 74 | 96 |
| Chakram | 4 | 8 | 20 | 12 | 0 | 2 | — | 0 | 100 | 14 | 0 |
| Trident | 52 | 98 | 82 | 42 | 100 | 96 | 100 | — | 100 | 84 | 100 |
| Bow | 0 | 0 | 2 | 0 | 0 | 0 | 0 | 0 | — | 4 | 0 |
| Lance | 6 | 72 | 56 | 24 | 54 | 26 | 86 | 16 | 96 | — | 76 |
| Duplicator | 0 | 94 | 0 | 0 | 100 | 4 | 100 | 0 | 100 | 24 | — |

## Pair-by-pair results and durations

Wins are shown as **first-listed weapon wins – second-listed weapon wins**. Durations are fight-level averages and medians across all 50 runs in that pairing.

| Pairing | Wins (A–B) | Average (s) | Median (s) |
|---|---:|---:|---:|
| Sword–Dagger | 48–2 | 60.21 | 57.42 |
| Sword–Spear | 49–1 | 45.21 | 45.66 |
| Sword–Axe | 32–18 | 44.14 | 41.52 |
| Sword–Hammer | 50–0 | 49.42 | 49.03 |
| Sword–Scythe | 48–2 | 45.19 | 45.44 |
| Sword–Chakram | 48–2 | 60.47 | 59.00 |
| Sword–Trident | 24–26 | 45.38 | 44.97 |
| Sword–Bow | 50–0 | 48.35 | 49.05 |
| Sword–Lance | 47–3 | 56.08 | 53.17 |
| Sword–Duplicator | 50–0 | 44.02 | 42.72 |
| Dagger–Spear | 13–37 | 89.24 | 84.34 |
| Dagger–Axe | 12–38 | 78.85 | 71.83 |
| Dagger–Hammer | 1–49 | 95.50 | 93.13 |
| Dagger–Scythe | 0–50 | 80.07 | 79.52 |
| Dagger–Chakram | 46–4 | 109.13 | 106.87 |
| Dagger–Trident | 1–49 | 63.09 | 58.28 |
| Dagger–Bow | 50–0 | 108.03 | 106.95 |
| Dagger–Lance | 14–36 | 102.61 | 103.07 |
| Dagger–Duplicator | 3–47 | 91.88 | 90.33 |
| Spear–Axe | 16–34 | 56.78 | 57.38 |
| Spear–Hammer | 39–11 | 75.93 | 75.18 |
| Spear–Scythe | 17–33 | 65.61 | 65.86 |
| Spear–Chakram | 40–10 | 83.82 | 76.27 |
| Spear–Trident | 9–41 | 52.83 | 51.23 |
| Spear–Bow | 49–1 | 89.97 | 83.70 |
| Spear–Lance | 22–28 | 80.95 | 78.97 |
| Spear–Duplicator | 50–0 | 63.93 | 61.05 |
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

- **Sword leads at 89.2%** and won 49/50 against Spear, 48/50 against Dagger, Scythe, and Chakram, and 47/50 against Lance. It split almost evenly with Trident (24–26).
- **Trident remains very strong at 85.4%**, winning 41/50 against Spear, 48/50 against Scythe, and 42/50 against Lance. It lost 24–26 to Sword and 21–29 to Axe.
- **Axe is third at 79.4%** after its critical damage progression change. It won 38/50 against Lance and 29/50 against Trident, and swept Bow and Duplicator 50–0.
- **Spear lands near the middle at 56.0%**. The much slower +3.6px reach growth removed its runaway advantage; it still beat Hammer 39–11, Chakram 40–10, and Duplicator 50–0, but lost 9–41 to Trident.
- **Bow is the outlier at 0.6%**: just 3 wins in 500 fights. It won 2/50 against Lance and 1/50 against Spear, and lost all 50 fights against six opponents. The faster arrow speed and shorter cooldown did not compensate for its weaknesses in this arena.
- The results still show a top-heavy field: Sword, Trident, and Axe are above 79%, while Chakram and Bow are below 16%. Spear and Lance are the closest to the 50% mark.

**Overall fight duration:** average 72.44 seconds, median 68.17 seconds, longest 197.62 seconds. No fight reached the 360-second cap.
