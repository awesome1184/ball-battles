# Ball Battles

A dependency-free browser game prototype. The entire game currently lives in index.html; there is no build step, package install, or backend.

## Run in Codespaces

Open this repository in a Codespace, then run:

    python3 -m http.server 8000 --bind 0.0.0.0

Open the forwarded port 8000 in the Ports panel. The game is served from the repository root.

## Publish with GitHub Pages

1. Open Settings → Pages for this repository.
2. Under Build and deployment, choose Deploy from a branch.
3. Select branch main and folder /(root), then save.
4. Once GitHub Pages finishes publishing, open:

https://awesome1184.github.io/ball-battles/

No GitHub Actions workflow is required for this setup.

## Prototype features

- Daily deterministic weapon matchup with an animated canvas battle. All fights use 1.5× faster weapon rotation and 1.6× base health. Matches have no time limit or overtime damage: a side wins only when every opposing ball has been eliminated.
- Clean portrait arena with solid red/green/magenta balls, readable per-ball health, and redesigned, distinct pixel-art weapon silhouettes. Weapon artwork is clipped to the outside of each ball so every weapon visibly meets the orb's surface; arena sprites are also clipped to the arena boundaries.
- Bouncy, energy-preserving physics inspired by the supplied Earclacks reference: floor, ceiling, and wall rebounds preserve momentum, with no floor friction. Ball-to-ball impacts use fully elastic normal impulses. Every fighter receives independent, irregular horizontal momentum impulses, with strong lateral travel, wall-aware escape, and a recovery burst when it gets trapped in a small horizontal area. Fighters do not home toward opponents; they move independently and collide naturally. Duplicator clones get their own roaming direction. Lance charges retain their dedicated high-speed wall-rebound behavior. All weapons rotate 1.5× faster than the previous tuning; Bow retains its additional 4× rotation multiplier.
- Opposing pixel-art weapons physically clash as they rotate. Parries trigger a gold flash, sparks, brief stagger, knockback, and reverse the rotation direction of the involved weapons. Weapon guards can also catch arrows; Hammer attacks remain unparryable.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Every weapon begins each fight at 1 base damage before any purchased stat bonuses or per-hit growth. There is no automatic ball-to-ball pursuit; fighters move through momentum, gravity, and collisions. Trident's whirlpool follows its rotating weapon head and actively pulls every nearby living ball toward it.
- Each weapon has its own fight-specific mechanic: Sword gains +1 damage per hit; Dagger gains 6% compounding attack speed; Spear starts with a short shaft, gains +0.5 damage per hit, and grows 8% longer per hit (compounding); Axe grows its stored damage by 1.95× per hit, uses damage as its crit percentage, and deals 1 on normal hits or full stored damage on critical hits; Hammer gains +0.65 damage and +0.15 maximum spin per hit, resets to 1× spin after a hit, starts very slowly, and cannot be parried; Scythe adds a poison stack worth 0.275 DPS per hit; Chakram gains 4.75% compounding spin speed; Trident gains +0.5 damage per hit and pulls nearby balls toward its moving whirlpool; Bow adds one arrow to future volleys for each arrow hit (up to 64 per volley), firing each arrow in sequence from the bowstring; Lance deals 1 on normal hits, doubles its stored damage per hit, and periodically charges to a wall while invulnerable, dealing its full stored damage; Duplicator's main ball creates one full-health clone every 8 team hits, up to 6 balls total. The main ball has reduced health, enemies prioritize it, clones deal very low contact damage, and the whole swarm is eliminated immediately if the main ball dies.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator. Duplicator has no weapon; the main ball's body deals damage by direct contact, and clones spawn at the main ball's full maximum health.
- Per-weapon, per-stat level pools for base damage, scaling, weapon size, projectile rate, attack speed, and spin speed. Each contribution adds 50 coins to that stat's progress bar; the next level costs 50 × (level + 1)² coins. Stat gains start at 1% or 2% per level, and the gain per new level increases linearly (for example, a 2% stat gains +2%, then +4%, then +6%). The prototype stores these pools locally; global cross-player sharing requires the Devvit backend.
- The daily path is: watch the current daily fight, receive the previous day's bet payout on the next daily visit with a one-time animated win/loss reveal, then upgrade the weapon you backed or open Simulations.
- Simulations use your trained favorite weapon against a randomly selected opponent. Opponents cannot be chosen; simulations use the same battle engine, hide daily betting controls, and are recorded separately from daily showdowns.
- Fight records, a matchup win-rate matrix (2,750 neutral simulations: 50 per pairing, 25 from each starting side), and a local developer test panel. The displayed matchup matrix is an archived pre-roaming balance snapshot. Its win-rate estimates need to be recalculated before they can be used to assess the new movement system.
- Sound toggle and 1× / 2× battle speed.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.
