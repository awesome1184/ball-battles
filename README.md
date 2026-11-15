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

## Visual direction

The live page follows the visual guide in `DESIGN.md`: a flat blue backdrop, cream paper panels, ink outlines and offset shadows, flat red/green corners, a ticket-style prediction slip, sentence-case copy, and pixel-art weapon previews drawn from the battle sprites. The wordmark, matchup corners, and page headings use an embedded Pixelify Sans subset under the SIL Open Font License; the full license is in `licenses/`. Numbers remain in the system sans for readability. The battle engine remains in the standalone `index.html`; the `/ui` scaffold is a reference for the design and future extraction, not a replacement runtime.

## Prototype features

- Daily deterministic weapon matchup with an animated canvas battle. Every fighter starts at exactly 100 HP, including Duplicator's main ball and its full-health clones. All fights use 1.5× weapon rotation. Matches have no time limit or overtime damage: a side wins only when every opposing ball has been eliminated.
- Clean portrait arena with solid red/green/magenta balls, readable per-ball health, and ten distinct pixel-art weapon sprites. Each sprite receives silhouette, material, bevel/shadow, highlight, and detail passes; artwork is clipped so each weapon meets the orb cleanly and stays inside the arena.
- Gravity-driven arena physics: fighters receive a seeded random launch velocity and then move without steering or horizontal acceleration. Floor, ceiling, and wall rebounds preserve full speed. Ball collisions use elastic normal impulses with mass proportional to radius. A hidden stall rescue adds a small sideways nudge only after horizontal speed stays below 40 px/s for 2 seconds. The Trident whirlpool pulls harder over a 165px radius; Lance charges recur every 2.8 seconds after the initial charge. Hits pause the target's weapon rotation and attacks for a short, weapon-specific stagger while body movement continues. All weapons rotate 1.5× faster than the prior tuning; Bow retains its additional 4× rotation multiplier, and rotation is capped at 32 radians per second.
- Opposing pixel-art weapons physically clash as they rotate. Parries trigger a gold flash, sparks, brief stagger, and reverse the rotation direction of the involved weapons without pushing the balls. Weapon guards can also catch arrows; Hammer attacks remain unparryable.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Damage growth is additive rather than multiplicative. Fighters move freely under gravity and elastic collisions; there is no roaming controller or ongoing horizontal steering. A hidden rescue only adds a small sideways nudge after horizontal speed remains below 40 px/s for 2 seconds. Trident's whirlpool follows its rotating weapon head and actively pulls every nearby living ball toward it.
- Each weapon has its own fight-specific growth: Sword gains +1 damage per hit; Dagger gains 6% compounding attack speed and +0.08 damage per hit; Spear gains +0.5 damage and 8% length per hit; Axe gains +2 stored damage and +2 percentage points of critical chance per hit; Hammer gains +0.65 damage and +0.15 maximum spin per hit, resets to 1× spin after a hit, and remains unparryable but now physically clashes with other weapons; Scythe adds a poison stack worth 0.16 DPS per hit; Chakram gains 4.75% compounding spin speed and +0.18 damage per hit; Trident gains +0.65 damage per hit and has a larger, stronger whirlpool; Bow adds one arrow to future volleys per landed arrow (up to 64), with a faster volley cycle; Lance gains +2 charge damage per hit and makes more frequent, stronger wall charges. Successful hits also interrupt the target for a short weapon-specific stun that grows with the attacker's successful hits, with per-weapon caps and a brief re-stun guard.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator. All ten armed weapons share a 72px base reach and the same artwork scale; weapon-size upgrades raise reach to a hard 90px cap, exactly 1.5× the 60px ball diameter. Duplicator remains deliberately unarmed. Its main ball gains +0.2 damage per main-ball hit, and a full-health 100-HP clone spawns every 6 team hits (up to 6 balls). Clones deal 0.45 contact damage, spawn from the main ball, and can screen it from nearby attackers. If the main dies, the entire swarm is eliminated.
- Per-weapon, per-stat level pools for base damage, scaling, weapon size, projectile rate, attack speed, and spin speed. Each contribution adds 50 coins to that stat's progress bar; the next level costs 50 × (level + 1)² coins. Stat gains start at 1% or 2% per level, and the gain per new level increases linearly (for example, a 2% stat gains +2%, then +4%, then +6%). The prototype stores these pools locally; global cross-player sharing requires the Devvit backend.
- The daily path is: watch the current daily fight, receive the previous day's bet payout on the next daily visit with a one-time animated win/loss reveal, then upgrade the weapon you backed or open Simulate.
- Live practice uses your trained favorite weapon against a randomly selected opponent. The Matchup Simulator lets you choose any two weapons and run 10, 25, 50, or 100 seeded fights using the actual battle engine. Starting sides alternate, results include win counts, draw/timeouts, and fight durations, and the test runs do not modify your save.
- Fight records include a clearly labeled historical matchup matrix from the previous 86px base-reach rules. It is retained for reference but is not presented as a current ranking; use the Matchup Simulator to generate fresh results under the 72px base / 90px maximum weapon rules.
- Synthesized battle audio uses WebAudio only, with no recordings, sound libraries, or external assets. Each weapon has its own filtered-noise impact and low thump; hit sounds brighten and rise in pitch as hit counts grow. Bow releases a short string twang and its arrows land with a separate thock. Weapon clashes and parries ring with detuned metallic tones, wall rebounds get soft speed-scaled ticks, ball collisions get low thuds, and knockouts finish with a deep thump and falling tone. The audio system caps polyphony at 8 voices, rate-limits each sound type, adds slight pitch variation, and is controlled by the existing sound toggle. Battle speed remains switchable between 1× and 2×.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.
