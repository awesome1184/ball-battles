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

- Daily deterministic weapon matchup with an animated canvas battle. Fights are knockout-only and do not end at a fixed time limit.
- Clean portrait arena with solid red/green/magenta balls, readable per-ball health, and redesigned, distinct pixel-art weapon silhouettes. The arena box is slightly smaller, and sprites are clipped to its boundaries.
- Bouncy physics inspired by the supplied Earclacks reference: floor, ceiling, and wall rebounds retain 100% of velocity, while ball-to-ball impacts use fully elastic normal impulses. Fighters do not home toward opponents; they move independently and collide naturally. Bow alone rotates 4× faster; all other weapons retain their own rotation speeds.
- Opposing pixel-art weapons physically clash as they rotate. Parries trigger a gold flash, sparks, brief stagger, knockback, and reverse the rotation direction of the involved weapons. Weapon guards can also catch arrows; Hammer attacks remain unparryable.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Every weapon begins each fight at 1 base damage before any purchased stat bonuses or per-hit growth. There is no automatic ball-to-ball pursuit; fighters move through momentum, gravity, and collisions. Trident's whirlpool is visual only and does not pull balls.
- Each weapon has its own fight-specific mechanic: Sword gains +1 damage per hit; Dagger gains 3.5% compounding attack speed; Spear starts with a short shaft, gains +0.5 damage per hit, and grows 8% longer per hit (compounding); Axe doubles its damage per hit, uses damage as its crit percentage, and deals 1 on normal hits or full stored damage on critical hits; Hammer gains +1 damage and +0.25 maximum spin per hit, resets to 1× spin after a hit, starts very slowly, and cannot be parried; Scythe adds one stack of 1 DPS poison per hit; Chakram gains 2.5% compounding spin speed; Trident gains +0.5 damage per hit and has a moving whirlpool visual; Bow adds one arrow to future volleys for each arrow hit (up to 64 per volley), firing each arrow in sequence from the bowstring; Lance deals 1 on normal hits, doubles its stored damage per hit, and periodically charges to a wall while invulnerable, dealing its full stored damage; Duplicator adds one clone every 4 team hits, up to 16 balls.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator. Duplicator has no weapon: its ball deals damage by body contact, while its team still gains one clone every 4 hits up to 16.
- Individual 50-coin contributions for base damage, scaling, weapon size, projectile rate, attack delay, and spin speed. The first contribution gives +5%, the next +2.5%, then +1.667% and so on, with harmonic diminishing returns; Scaling increases eligible per-hit growth.
- Practice fights let you choose the opposing weapon in Weapon Lab instead of selecting a random rival.
- Fight records and a local developer test panel.
- Sound toggle and 1× / 2× battle speed.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.