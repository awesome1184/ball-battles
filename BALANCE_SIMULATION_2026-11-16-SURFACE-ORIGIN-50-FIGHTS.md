# Ball Battles balance simulation: revised balance, 50 fights per pairing

**Date:** 2026-11-16  
**Source game file blob used for the combat run:** `dc1245ca418061ba450ddaec26262058750a9c1c`

## Test method

- Used the game's actual deterministic `simulateOneMatchup(leftId, rightId, runIndex)` runner and its `step(1/60)` simulation loop from `index.html`. This was not a simplified damage or matchup model.
- Tested all 11 weapons against every other weapon: 55 unique unordered pairings.
- Ran 50 seeded fights per pairing, 2,750 total fights.
- The engine alternated starting sides by run index, giving each weapon 25 starts on each side in every pairing.
- The 360-second per-fight simulation cap remained in place.
- **2,748 fights ended decisively and 2 reached the 360-second cap.** There were no other draws.
- Each weapon appeared in 10 pairings × 50 fights = 500 fights.

## Geometry and balance used

All armed weapon lengths are measured outward from the edge of the 60px diameter fighter ball. Melee attack and parry segments begin at the ball surface and extend outward by the listed reach; loaded art, fallback pixel art, and weapon icons use the same surface attachment. The Trident's whirlpool remains centered on its weapon tip. Bow arrows launch from the forward side of the orb. Duplicator intentionally has no weapon.

- **Sword:** 1 base damage, +1 damage per successful hit, 72px starting reach, and 2.2 base rotation speed (before the shared 1.5× rotation multiplier).
- **Dagger:** +8% compounding spin speed per hit.
- **Spear:** 36px starting reach and +3.6px reach plus +0.5 damage per successful hit. Its shaft is 1.5× wider visually; its attack and parry hitbox width is unchanged.
- **Axe:** 3% starting critical chance and 3 critical damage; +1 percentage point of critical chance and +0.5 critical damage per hit. Non-critical hits deal exactly 1 damage.
- **Hammer:** starts at 1 spin speed, uses spin speed as damage, winds up at 1.25 spin-speed units per second, gains +0.5 maximum spin speed per hit, and resets to 1 after a hit. Hammer attacks remain unparryable; Hammer can parry other weapons without reversing its own rotation.
- **Scythe:** +0.09 poison damage per second per successful hit.
- **Chakram:** +4.75% compounding spin speed and +0.05 damage per successful hit.
- **Trident:** 300 starting pull strength, +20 pull strength and +0.5 damage per hit, with a fixed 165px whirlpool radius.
- **Bow:** 500px/s arrows, 1.485-second base volley cooldown, three starting arrows per volley, and +1 arrow for each landed arrow. All queued arrows in a volley share the angle captured when the volley begins.
- **Lance:** +2 charge damage per hit; charges along its weapon's pointing angle, starting at 16px/s and accelerating to 440px/s.
- **Duplicator:** creates one clone every six team hits, up to six balls.

## Overall ranking

| Rank | Weapon | Wins | Win rate |
|---:|---|---:|---:|
| 1 | Trident | 433 / 500 | 86.6% |
| 2 | Chakram | 417 / 500 | 83.4% |
| 3 | Sword | 404 / 500 | 80.8% |
| 4 | Scythe | 278 / 500 | 55.6% |
| 5 | Lance | 271 / 500 | 54.2% |
| 6 | Spear | 262 / 500 | 52.4% |
| 7 | Hammer | 227 / 500 | 45.4% |
| 8 | Duplicator | 184 / 500 | 36.8% |
| 9 | Dagger | 131 / 500 | 26.2% |
| 10 | Axe | 127 / 500 | 25.4% |
| 11 | Bow | 14 / 500 | 2.8% |

## Matchup win-rate matrix

Each cell is the row weapon's percentage of wins against the column weapon, based on 50 fights. Values are in 2% increments. Columns and rows are ordered Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, Duplicator.

| Weapon | Sword | Dagger | Spear | Axe | Hammer | Scythe | Chakram | Trident | Bow | Lance | Duplicator |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| Sword | — | 84 | 92 | 100 | 90 | 88 | 46 | 40 | 98 | 70 | 100 |
| Dagger | 16 | — | 44 | 64 | 0 | 14 | 2 | 2 | 94 | 24 | 2 |
| Spear | 8 | 56 | — | 96 | 52 | 44 | 6 | 22 | 94 | 48 | 98 |
| Axe | 0 | 36 | 4 | — | 4 | 38 | 2 | 2 | 88 | 18 | 62 |
| Hammer | 10 | 100 | 48 | 96 | — | 24 | 8 | 4 | 100 | 64 | 0 |
| Scythe | 12 | 86 | 56 | 62 | 76 | — | 16 | 0 | 100 | 56 | 92 |
| Chakram | 54 | 98 | 94 | 98 | 92 | 84 | — | 36 | 100 | 78 | 100 |
| Trident | 60 | 98 | 78 | 98 | 96 | 100 | 64 | — | 98 | 74 | 100 |
| Bow | 2 | 6 | 4 | 12 | 0 | 0 | 0 | 0 | — | 2 | 2 |
| Lance | 30 | 76 | 52 | 82 | 36 | 44 | 22 | 26 | 98 | — | 76 |
| Duplicator | 0 | 98 | 2 | 38 | 100 | 8 | 0 | 0 | 98 | 24 | — |

## Pair-by-pair results and durations

Wins are shown as **first-listed weapon wins – second-listed weapon wins**. Durations are fight-level averages and medians across all 50 runs in that pairing. The Spear–Bow and Trident–Bow pairings each had one 360-second timeout.

| Pairing | Wins (A–B) | Average (s) | Median (s) |
|---|---:|---:|---:|
| Sword–Dagger | 42–8 | 67.71 | 62.67 |
| Sword–Spear | 46–4 | 54.94 | 53.56 |
| Sword–Axe | 50–0 | 54.63 | 56.43 |
| Sword–Hammer | 45–5 | 60.74 | 60.41 |
| Sword–Scythe | 44–6 | 55.64 | 55.67 |
| Sword–Chakram | 23–27 | 58.06 | 59.62 |
| Sword–Trident | 20–30 | 50.05 | 48.97 |
| Sword–Bow | 49–1 | 65.01 | 63.09 |
| Sword–Lance | 35–15 | 65.61 | 62.93 |
| Sword–Duplicator | 50–0 | 51.62 | 50.26 |
| Dagger–Spear | 22–28 | 94.82 | 99.03 |
| Dagger–Axe | 32–18 | 114.15 | 110.46 |
| Dagger–Hammer | 0–50 | 85.94 | 84.84 |
| Dagger–Scythe | 7–43 | 84.41 | 83.97 |
| Dagger–Chakram | 1–49 | 75.07 | 74.73 |
| Dagger–Trident | 1–49 | 64.65 | 63.65 |
| Dagger–Bow | 47–3 | 106.16 | 104.22 |
| Dagger–Lance | 12–38 | 108.22 | 112.70 |
| Dagger–Duplicator | 1–49 | 92.16 | 91.52 |
| Spear–Axe | 48–2 | 68.12 | 66.46 |
| Spear–Hammer | 26–24 | 75.64 | 74.94 |
| Spear–Scythe | 22–28 | 67.48 | 70.12 |
| Spear–Chakram | 3–47 | 66.04 | 65.59 |
| Spear–Trident | 11–39 | 52.69 | 51.78 |
| Spear–Bow | 47–2 (1 timeout) | 93.95 | 82.22 |
| Spear–Lance | 24–26 | 83.57 | 85.01 |
| Spear–Duplicator | 49–1 | 70.08 | 69.08 |
| Axe–Hammer | 2–48 | 78.74 | 78.06 |
| Axe–Scythe | 19–31 | 72.58 | 71.18 |
| Axe–Chakram | 1–49 | 68.94 | 68.47 |
| Axe–Trident | 1–49 | 57.21 | 55.47 |
| Axe–Bow | 44–6 | 112.94 | 106.68 |
| Axe–Lance | 9–41 | 98.62 | 101.27 |
| Axe–Duplicator | 31–19 | 85.87 | 83.47 |
| Hammer–Scythe | 12–38 | 73.47 | 73.55 |
| Hammer–Chakram | 4–46 | 68.26 | 69.63 |
| Hammer–Trident | 2–48 | 54.59 | 53.18 |
| Hammer–Bow | 50–0 | 81.85 | 79.13 |
| Hammer–Lance | 32–18 | 82.80 | 81.15 |
| Hammer–Duplicator | 0–50 | 96.85 | 93.57 |
| Scythe–Chakram | 8–42 | 66.14 | 66.35 |
| Scythe–Trident | 0–50 | 46.78 | 45.95 |
| Scythe–Bow | 50–0 | 75.35 | 74.12 |
| Scythe–Lance | 28–22 | 83.63 | 83.79 |
| Scythe–Duplicator | 46–4 | 76.77 | 76.75 |
| Chakram–Trident | 18–32 | 55.26 | 55.82 |
| Chakram–Bow | 50–0 | 64.69 | 65.68 |
| Chakram–Lance | 39–11 | 76.13 | 76.46 |
| Chakram–Duplicator | 50–0 | 53.13 | 50.06 |
| Trident–Bow | 49–0 (1 timeout) | 65.53 | 58.70 |
| Trident–Lance | 37–13 | 66.26 | 65.62 |
| Trident–Duplicator | 50–0 | 50.71 | 50.55 |
| Bow–Lance | 1–49 | 106.28 | 103.42 |
| Bow–Duplicator | 1–49 | 93.07 | 90.52 |
| Lance–Duplicator | 38–12 | 86.99 | 87.66 |

## Findings

- **Trident is the leader at 86.6%.** It beat Sword 30–20, Chakram 32–18, and swept Scythe and Duplicator. Its reduced pull values still produce a strong advantage.
- **Chakram is second at 83.4%.** The +0.05 damage-per-hit addition makes it competitive without the 93% runaway seen with the initial +0.15 test. It still won 49/50 against Dagger and Axe, and 47/50 against Spear; it swept Bow and Duplicator.
- **Sword is third at 80.8%.** The shorter 72px reach and 2.2 base rotation speed lowered its win rate from 89.0% on the prior run, despite its requested +1 damage-per-hit growth. It split nearly evenly with Chakram (23–27), but still swept Axe and Duplicator and won 49/50 against Bow.
- **The middle group is substantially closer:** Scythe 55.6%, Lance 54.2%, and Spear 52.4%.
- **Bow remains the clear outlier at 2.8%**, with 14 wins in 500 fights. Same-angle volleys raised it from the previous 1.0% run, but it remains far below the field. Its two timeouts were against Spear and Trident.
- Dagger and Axe remain weak at 26.2% and 25.4%; Hammer and Duplicator are also below even at 45.4% and 36.8%.

**Overall fight duration:** average 74.30 seconds, median 71.35 seconds, longest 360 seconds (the simulation cap).
