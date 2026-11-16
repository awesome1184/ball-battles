# Ball Battles balance simulation

**Run date:** 2026-11-16  
**Game revision:** `f255df1` (before this results-only refresh)  
**Arena:** 560×560  
**Roster:** 11 balls, 55 unique pairings  
**Sample size:** 50 seeded fights per pairing, 25 starts from each side  
**Total:** 2,750 fights  
**Test cap:** 360 seconds per fight

## Method

Every ball was tested against every other ball using the current `simulateOneMatchup` battle engine, not a simplified damage model. Each pairing used 50 deterministic seeded runs. The starting side alternated so each weapon began on the left 25 times and on the right 25 times.

A fight that was still active at 360 seconds was recorded as a timeout/draw. There were **437 timeouts (15.9%)** and **2,313 decisive finishes**. Matrix win rates below are **wins divided by all 50 attempts**, so timeouts are not silently discarded or counted as losses. Average and median durations in the detailed results use decisive finishes only.

## Overall results

Each weapon participated in 500 fights, 50 against each of the other ten weapons.

| Rank | Ball | Wins / 500 | Win rate | Timeout draws / 500 |
|---:|---|---:|---:|---:|
| 1 | Scythe | 456 | 91.2% | 0 |
| 2 | Lance | 452 | 90.4% | 0 |
| 3 | Sword | 426 | 85.2% | 10 |
| 4 | Duplicator | 278 | 55.6% | 32 |
| 5 | Dagger | 222 | 44.4% | 93 |
| 6 | Axe | 178 | 35.6% | 81 |
| 7 | Chakram | 161 | 32.2% | 111 |
| 8 | Trident | 72 | 14.4% | 52 |
| 9 | Hammer | 42 | 8.4% | 187 |
| 10 | Spear | 22 | 4.4% | 147 |
| 11 | Bow | 4 | 0.8% | 161 |

## Matchup matrix

Percentages show the row weapon's wins out of all 50 fights against the column weapon. The remaining percentage consists of opponent wins and timeouts/draws.

| Ball | SWD | DAG | SPR | AXE | HAM | SCY | CHK | TRI | BOW | LNC | DUP |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 86 | 100 | 98 | 100 | 44 | 84 | 100 | 100 | 40 | 100 |
| Dagger | 4 | — | 62 | 80 | 38 | 0 | 72 | 94 | 74 | 0 | 20 |
| Spear | 0 | 0 | — | 0 | 0 | 0 | 0 | 40 | 4 | 0 | 0 |
| Axe | 0 | 2 | 78 | — | 54 | 0 | 12 | 100 | 60 | 0 | 50 |
| Hammer | 0 | 4 | 28 | 10 | — | 0 | 0 | 24 | 14 | 0 | 4 |
| Scythe | 56 | 100 | 100 | 100 | 100 | — | 100 | 100 | 100 | 56 | 100 |
| Chakram | 8 | 8 | 62 | 52 | 30 | 0 | — | 90 | 66 | 0 | 6 |
| Trident | 0 | 4 | 40 | 0 | 30 | 0 | 6 | — | 64 | 0 | 0 |
| Bow | 0 | 0 | 0 | 0 | 4 | 0 | 0 | 4 | — | 0 | 0 |
| Lance | 60 | 100 | 100 | 100 | 100 | 44 | 100 | 100 | 100 | — | 100 |
| Duplicator | 0 | 66 | 92 | 42 | 86 | 0 | 82 | 100 | 88 | 0 | — |

## Detailed pair results

Format: **A wins – B wins – timeouts**, followed by average/median decisive fight duration. A and B are in the order shown.

| Pairing | A–B–Draws | Avg. decisive time | Median |
|---|---:|---:|---:|
| Sword – Dagger | 43–2–5 | 125.0s | 115.0s |
| Sword – Spear | 50–0–0 | 101.2s | 99.7s |
| Sword – Axe | 49–0–1 | 112.1s | 112.2s |
| Sword – Hammer | 50–0–0 | 104.9s | 103.3s |
| Sword – Scythe | 22–28–0 | 97.5s | 97.1s |
| Sword – Chakram | 42–4–4 | 123.8s | 118.5s |
| Sword – Trident | 50–0–0 | 121.0s | 117.9s |
| Sword – Bow | 50–0–0 | 104.5s | 104.3s |
| Sword – Lance | 20–30–0 | 133.6s | 130.6s |
| Sword – Duplicator | 50–0–0 | 80.0s | 80.0s |
| Dagger – Spear | 31–0–19 | 245.7s | 236.2s |
| Dagger – Axe | 40–1–9 | 248.2s | 232.7s |
| Dagger – Hammer | 19–2–29 | 291.0s | 313.7s |
| Dagger – Scythe | 0–50–0 | 118.0s | 115.6s |
| Dagger – Chakram | 36–4–10 | 224.2s | 216.4s |
| Dagger – Trident | 47–2–1 | 282.4s | 282.7s |
| Dagger – Bow | 37–0–13 | 252.2s | 232.9s |
| Dagger – Lance | 0–50–0 | 171.0s | 172.8s |
| Dagger – Duplicator | 10–33–7 | 157.1s | 147.0s |
| Spear – Axe | 0–39–11 | 248.2s | 233.4s |
| Spear – Hammer | 0–14–36 | 318.3s | 325.6s |
| Spear – Scythe | 0–50–0 | 107.9s | 108.7s |
| Spear – Chakram | 0–31–19 | 267.1s | 274.1s |
| Spear – Trident | 20–20–10 | 321.5s | 327.7s |
| Spear – Bow | 2–0–48 | 343.8s | 354.9s |
| Spear – Lance | 0–50–0 | 153.3s | 149.8s |
| Spear – Duplicator | 0–46–4 | 160.3s | 145.7s |
| Axe – Hammer | 27–5–18 | 250.4s | 246.5s |
| Axe – Scythe | 0–50–0 | 107.2s | 105.2s |
| Axe – Chakram | 6–26–18 | 244.3s | 231.6s |
| Axe – Trident | 50–0–0 | 234.3s | 238.9s |
| Axe – Bow | 30–0–20 | 273.6s | 283.8s |
| Axe – Lance | 0–50–0 | 156.7s | 165.9s |
| Axe – Duplicator | 25–21–4 | 157.2s | 145.7s |
| Hammer – Scythe | 0–50–0 | 111.5s | 111.1s |
| Hammer – Chakram | 0–15–35 | 289.2s | 289.0s |
| Hammer – Trident | 12–15–23 | 326.9s | 326.2s |
| Hammer – Bow | 7–2–41 | 324.7s | 325.1s |
| Hammer – Lance | 0–50–0 | 153.4s | 151.4s |
| Hammer – Duplicator | 2–43–5 | 159.8s | 141.9s |
| Scythe – Chakram | 50–0–0 | 112.7s | 110.6s |
| Scythe – Trident | 50–0–0 | 107.6s | 109.5s |
| Scythe – Bow | 50–0–0 | 111.7s | 110.4s |
| Scythe – Lance | 28–22–0 | 133.6s | 134.6s |
| Scythe – Duplicator | 50–0–0 | 103.5s | 101.8s |
| Chakram – Trident | 45–3–2 | 312.8s | 320.4s |
| Chakram – Bow | 33–0–17 | 256.6s | 250.1s |
| Chakram – Lance | 0–50–0 | 154.2s | 148.9s |
| Chakram – Duplicator | 3–41–6 | 157.2s | 147.0s |
| Trident – Bow | 32–2–16 | 316.3s | 324.9s |
| Trident – Lance | 0–50–0 | 146.6s | 143.8s |
| Trident – Duplicator | 0–50–0 | 104.4s | 105.2s |
| Bow – Lance | 0–50–0 | 155.0s | 148.7s |
| Bow – Duplicator | 0–44–6 | 171.0s | 151.0s |
| Lance – Duplicator | 50–0–0 | 112.9s | 113.2s |

## Balance conclusions

- **Scythe and Lance lead the field**, at 91.2% and 90.4% of all trials respectively. Scythe wins 50–0 against seven opponents, while Lance wins 50–0 against eight.
- **Sword is also extremely strong**, winning 85.2% of all trials. It loses only to Scythe and Lance in decisive matchups, with a close 22–28 result against Scythe.
- **Duplicator is the only other ball above 50%**, at 55.6%. Its clones make it a strong counter to several slower weapons, but it loses decisively to Sword, Scythe, and Lance.
- **Dagger is highly volatile**: 44.4% wins overall and 93 timeouts. Its spin-speed-only scaling can create long, unresolved fights; it beats several weapons consistently but loses every test against Scythe and Lance.
- **Spear, Hammer, and Bow are severely underpowered** in the current rules. Bow won just 4 of 500 tests, and Spear won 22. Their high timeout counts also point to a lack of reliable finishing power.
- **The 437 timeout draws are a balance issue in their own right.** In particular, Spear–Bow timed out 48/50 times, and Hammer–Bow 41/50 times. These matchups need more finishing pressure rather than treating stalemates as losses.
