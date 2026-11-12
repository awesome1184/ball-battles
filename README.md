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
- Gravity, wall/floor collisions, bouncing, and simple fighter movement.
- Lance damage ramp and Duplicator team replication: 1 → 2 → 4 → 8 → 16 balls during a fight.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Ten weapon types, including a ranged Bow, Lance, and Duplicator.
- Individual coin-funded upgrades for base damage, scaling, weapon size, projectile rate, attack delay, and spin speed.
- Gravity, jumping, floor bounce, wall collisions, and weapon hitboxes in the arena.
- Fight records and a local developer test panel.
- Sound toggle and 1× / 2× battle speed.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.