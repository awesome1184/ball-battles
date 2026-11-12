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

- Daily deterministic weapon matchup with an animated canvas battle. All fights use 1.5× faster weapon rotation, 1.6× base health, escalating arena overtime from 40 seconds, and a 50-second maximum with remaining-health tiebreaks.
- Clean portrait arena with solid red/green/magenta balls, readable per-ball health, and redesigned, distinct pixel-art weapon silhouettes. Weapon artwork is clipped to the outside of each ball so every weapon visibly meets the orb's surface; arena sprites are also clipped to the arena boundaries.
- Bouncy, energy-preserving physics inspired by the supplied Earclacks reference: floor, ceiling, and wall rebounds retain 100% of velocity, with no floor friction or velocity clipping. Ball-to-ball impacts use fully elastic normal impulses. Fighters do not home toward opponents; they move independently and collide naturally. Fighters start with stronger horizontal launch speed, and Duplicator clones also receive stronger horizontal motion. Lance charges rebound from walls without losing horizontal momentum. All weapons rotate 1.5× faster than the previous tuning; Bow retains its additional 4× rotation multiplier.
- Opposing pixel-art weapons physically clash as they rotate. Parries trigger a gold flash, sparks, brief stagger, knockback, and reverse the rotation direction of the involved weapons. Weapon guards can also catch arrows; Hammer attacks remain unparryable.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Every weapon begins each fight at 1 base damage before any purchased stat bonuses or per-hit growth. There is no automatic ball-to-ball pursuit; fighters move through momentum, gravity, and collisions. Trident's whirlpool follows its rotating weapon head and actively pulls every nearby living ball toward it.
- Each weapon has its own fight-specific mechanic: Sword gains +1 damage per hit; Dagger gains 3.5% compounding attack speed; Spear starts with a short shaft, gains +0.5 damage per hit, and grows 8% longer per hit (compounding); Axe doubles its damage per hit, uses damage as its crit percentage, and deals 1 on normal hits or full stored damage on critical hits; Hammer gains +1 damage and +0.25 maximum spin per hit, resets to 1× spin after a hit, starts very slowly, and cannot be parried; Scythe adds one stack of 1 DPS poison per hit; Chakram gains 2.5% compounding spin speed; Trident gains +0.5 damage per hit and pulls nearby balls toward its moving whirlpool; Bow adds one arrow to future volleys for each arrow hit (up to 64 per volley), firing each arrow in sequence from the bowstring; Lance deals 1 on normal hits, doubles its stored damage per hit, and periodically charges to a wall while invulnerable, dealing its full stored damage; Duplicator has a marked main ball that deals damage by body contact, then creates one full-health clone every 4 team hits (up to 16 balls). Clones deal reduced damage, and if the main ball dies, the entire swarm is immediately eliminated.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator. Duplicator has no weapon; the main ball's body deals damage by direct contact, and clones spawn at the main ball's full maximum health.
- Per-weapon, per-stat level pools for base damage, scaling, weapon size, projectile rate, attack speed, and spin speed. Each contribution adds 50 coins to that stat's progress bar; the next level costs 50 × (level + 1)² coins. Stat gains start at 1% or 2% per level, and the gain per new level increases linearly (for example, a 2% stat gains +2%, then +4%, then +6%). The prototype stores these pools locally; global cross-player sharing requires the Devvit backend.
- The daily path is: watch the current daily fight, receive the previous day's bet payout on the next daily visit with a one-time animated win/loss reveal, then upgrade the weapon you backed or open Simulations.
- Simulations use your trained favorite weapon against a randomly selected opponent. Opponents cannot be chosen; simulations use the same battle engine, hide daily betting controls, and are recorded separately from daily showdowns.
- Fight records, a matchup win-rate matrix (50 neutral simulations per pairing, 25 from each starting side), and a local developer test panel. Current baseline simulation rankings put Scythe first (90.8% average) and Dagger last (1.6% average); the matrix is a balance estimate, not live player data.
- Sound toggle and 1× / 2× battle speed.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.
