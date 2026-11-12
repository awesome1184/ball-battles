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

- Daily deterministic weapon matchup with an animated canvas battle.
- Clean portrait arena with solid red/green/magenta balls, readable per-ball health, and spinning weapon sprites.
- Gravity, wall/floor collisions, and continuous physical rebounds without scheduled jumps.
- Weapon clashes can trigger parries: a defender blocks the incoming strike, flashes gold, and briefly staggers the attacker. Weapon guards can also catch arrows.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Every weapon has its own per-hit growth rule: Sword damage +1; Dagger attack speed +3.5% (compounding); Spear damage +0.5 and reach +0.5; Axe damage +0.75; Hammer damage +1; Scythe damage +0.5 and reach +0.25; Chakram spin speed +2.5% (compounding); Trident damage +0.5 and attack speed +1.5%; Bow arrow damage +0.5 and projectile speed +6; Lance damage +0.8 and reach +0.35; Duplicator adds one clone every 4 team hits, up to 16.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator.
- Individual 50-coin contributions for base damage, scaling, weapon size, projectile rate, attack delay, and spin speed. Each contribution gives a tiny permanent gain with harmonic diminishing returns; Scaling increases the size of that weapon's per-hit growth.
- Fight records and a local developer test panel.
- Sound toggle and 1× / 2× battle speed.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.