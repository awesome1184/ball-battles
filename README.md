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

The live page follows the visual guide in `DESIGN.md`: a flat blue backdrop, cream paper panels, ink outlines and offset shadows, flat red/green corners, a ticket-style prediction slip, sentence-case copy, and pixel-art weapon previews from the Pixor CC0 weapon library, with local fallback sprites if the hosted images fail to load. The wordmark, matchup corners, and page headings use an embedded Pixelify Sans subset under the SIL Open Font License; the full license is in `licenses/`. Numbers remain in the system sans for readability. The battle engine remains in the standalone `index.html`; the `/ui` scaffold is a reference for the design and future extraction, not a replacement runtime.

## Earclacks-inspired fight presentation

The battle stage uses a square arena, compact matchup header with weapon icons, larger weapon-specific stat readouts, and distinct attack-hit indicators. Fighters now actively steer horizontally according to weapon-specific movement profiles; successful melee hits add a short forward lunge. Bow maintains a ranged gap, its limbs are oriented perpendicular to its firing axis, and arrows travel strictly along the bow's current rotation without auto-aim or target-leading. Other weapons close to different preferred distances. This is a movement and combat presentation change only; daily coins, predictions, upgrades, simulation tools, records, and the battle engine remain in place.

## Weapon art

The battle arena loads front-view pixel-art PNGs from [Pixor's free weapons library](https://pixor.art/library/weapons/), whose library assets are released under **CC0 1.0**. Used sprites: [sword](https://pixor.art/library/files/sword/sword.png), [dagger](https://pixor.art/library/files/dagger/dagger.png), [spear](https://pixor.art/library/files/spear/spear.png), [battle axe](https://pixor.art/library/files/axe/axe.png), [war hammer](https://pixor.art/library/files/hammer/hammer.png), [war scythe](https://pixor.art/library/files/war-scythe/war-scythe.png), [shuriken](https://pixor.art/library/files/shuriken/shuriken.png) (used for Chakram), [trident](https://pixor.art/library/files/trident/trident.png), [bow](https://pixor.art/library/files/bow/bow.png), and [lance](https://pixor.art/library/files/lance/lance.png). The existing hand-drawn sprites remain as an offline/load-failure fallback; Duplicator remains unarmed.


## Prototype features

- Daily deterministic weapon matchup with an animated canvas battle. Every fighter starts at exactly 100 HP, including Duplicator's main ball and its full-health clones. All fights use 1.5× weapon rotation. Matches have no time limit or overtime damage: a side wins only when every opposing ball has been eliminated.
- Square 600×600 battle arena with a compact matchup header, small weapon icons, flat circular fighter orbs in weapon-specific colors, fine black outlines, and centered high-contrast HP numbers. Weapon sprites prioritize instantly recognizable silhouettes over surface detail: bold shapes, flat fills, sharp outlines, and at most four opaque colors per sprite (outline, main color, shadow, highlight). Tiny bevels, extra material textures, and decorative fittings are removed. Lance is solid gold with a temporary blue shield only while charging; Duplicator is magenta with a small star marker on each clone.
- Gravity-driven arena physics with active, weapon-specific horizontal movement. Armed fighters close to a 96px preferred center gap so their 96px weapons can actually connect; Bow holds a 135px ranged gap, and unarmed Duplicator closes to 60px to land contact hits and build its swarm. Wall rebounds are deterministic and slightly damped instead of randomly deflecting velocity; floor impacts retain a small minimum hop, body collisions use 0.91 restitution, and a post-collision bounds pass keeps fighters inside the arena. Bow projectiles test every living opponent along their actual path, including Duplicator bodies, while still firing strictly along the bow's current rotation. Successful melee hits produce a brief lunge and a distinct weapon-colored slash, thrust, sweep, or impact cue. The Trident whirlpool pulls over a 165px radius. Hits cause a hidden, fixed 0.05-second impact-frame interruption while body movement continues. All weapons rotate 1.5× faster than the prior tuning; Bow retains its additional 4× rotation multiplier, and rotation is capped at 32 radians per second.
- Opposing pixel-art weapons physically clash as they rotate. Parries trigger a gold flash, sparks, brief stagger, and reverse the rotation direction of the involved weapons without pushing the balls. Weapon guards can also catch arrows; Hammer attacks remain unparryable.
- Per-hit weapon growth is temporary for that fight; a new fight starts from each weapon's base combat values.
- Damage growth is additive rather than multiplicative. Weapon-specific movement steers fighters toward their preferred engagement distance, while Bow backs away to preserve a ranged gap. Trident's whirlpool follows its rotating weapon head and actively pulls every nearby living ball toward it.
- Each weapon has its own fight-specific growth: Sword gains +1 damage per hit; Dagger gains 6% compounding attack speed and +0.08 damage per hit; Spear gains +0.5 damage and 8% length per hit; Axe gains +2 stored damage and +2 percentage points of critical chance per hit; Hammer gains +0.5 damage and +0.5 maximum spin per hit, resets to 1× spin after a hit, and remains unparryable but now physically clashes with other weapons; Scythe adds a poison stack worth 0.16 DPS per hit; Chakram gains 4.75% compounding spin speed and +0.18 damage per hit; Trident gains +0.65 damage per hit and has a larger, stronger whirlpool; Bow adds one arrow to future volleys per landed arrow (up to 64), with a faster volley cycle; Lance gains +2 charge damage per hit and makes more frequent, stronger wall charges. Successful hits cause a hidden, fixed 0.05-second impact-frame interruption. It does not scale with weapon or hit count.
- Daily coin claim, one prediction per daily matchup, and simulated community odds.
- Eleven weapon balls: Sword, Dagger, Spear, Axe, Hammer, Scythe, Chakram, Trident, Bow, Lance, and Duplicator. All ten armed weapons share a 96px base reach and the same artwork scale; weapon-size upgrades raise reach to a hard 102px cap (1.7× the 60px ball diameter), leaving roughly one ball diameter of visible weapon beyond the orb. Duplicator remains deliberately unarmed. Its main ball gains +0.2 damage per main-ball hit, and a full-health 100-HP clone spawns every 6 team hits (up to 6 balls). Clones deal 0.45 contact damage, spawn from the main ball, and can screen it from nearby attackers. If the main dies, the entire swarm is eliminated.
- Per-weapon, per-stat level pools for base damage, scaling, weapon size, projectile rate, attack speed, and spin speed. Each contribution adds 50 coins to that stat's progress bar; the next level costs 50 × (level + 1)² coins. Stat gains start at 1% or 2% per level, and the gain per new level increases linearly (for example, a 2% stat gains +2%, then +4%, then +6%). The prototype stores these pools locally; global cross-player sharing requires the Devvit backend.
- The daily path is: watch the current daily fight, receive the previous day's bet payout on the next daily visit with a one-time animated win/loss reveal, then upgrade the weapon you backed or open Simulate.
- Starting a new live fight, including a practice fight or matchup batch, immediately cancels the previous live fight without recording an unfinished result. The main fight button remains available during a live fight to restart it.
- Daily fight selection simulates batches of 500 deterministic candidates for the day's weapon pairing. A candidate qualifies only if it ends in a knockout within 120 seconds and reaches at least 2.00 excitement; the highest-scoring qualifying candidate wins, and the exact selected seed is replayed for the viewer. If a batch has no qualifying knockout, further 500-candidate batches are searched, with another batch available to start if the initial search limit is reached. The daily selection status shows the score, threshold, and damage activity. Large weapon-specific combat statistics sit immediately beneath the square arena, colored to match each fighter.
- Excitement scoring is weapon-neutral and uses five-second windows. Each window's intensity is `ln(1 + left-side HP damage) + ln(1 + right-side HP damage)`. The score is 65% of average window intensity plus 35% of the average of the three strongest windows, multiplied by `0.75 + 0.25 × active-window ratio`. This rewards sustained exchanges, gives equal credit to damage from either side, and compresses extreme damage bursts with a logarithm. Only actual HP damage contributes: there are no separate points for hit count, critical-hit labels, parries, clashes, arrow launches, clone spawns, Lance charges, winner identity, or remaining winner HP. Empty windows count against the average; movement and elapsed time alone score nothing.
- Live practice uses your trained favorite weapon against a randomly selected opponent. The Matchup Simulator lets you choose any two weapons and run 10, 25, 50, or 100 seeded fights using the actual battle engine. Starting sides alternate, results include win counts, draw/timeouts, and fight durations, and the test runs do not modify your save.
- Fight records include a clearly labeled historical matchup matrix from the previous 86px base-reach rules. It is retained for reference but is not presented as a current ranking; use the Matchup Simulator to generate fresh results under the 96px base / 102px maximum weapon rules.
- Synthesized battle audio uses WebAudio only, with no recordings, sound libraries, or external assets. Each weapon has its own filtered-noise impact and low thump; hit sounds brighten and rise in pitch as hit counts grow. Bow releases a short string twang and its arrows land with a separate thock. Weapon clashes and parries ring with detuned metallic tones, wall rebounds get soft speed-scaled ticks, ball collisions get low thuds, and knockouts finish with a deep thump and falling tone. The audio system caps polyphony at 8 voices, rate-limits each sound type, adds slight pitch variation, and is controlled by the existing sound toggle.

## Current prototype boundaries

Coins, upgrades, predictions, and records are stored in the current browser using localStorage. They do not sync between players or devices. The official daily matchup is generated from the date, so players load the same matchup and deterministic fight simulation, but the displayed community percentages are currently demo values rather than a live shared pool. There is no account system or server-side validation yet.
