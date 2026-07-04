# Grimhollow

A Diablo II-style caster action-RPG that runs entirely in the browser. A sorceress wakes at the last camp before a sunless crypt — cross the grave gate, break the dead, take what drops, and dive deeper.

Single-file, no build step, no dependencies — it's all `index.html`.

## Start

Choose a save slot from the Diablo II-style character select screen. The **Mage** is the only selectable class for now; other class cards are locked placeholders for future work. Each slot saves Mage progression in `localStorage`.

## Play

- **Left-click** — move; hold on a foe to cast **Firebolt**
- **1** — **Firebolt**, a fast single-target projectile
- **2** — **Frost Nova**, close-range crowd control
- **3** or **Spacebar** — dodge roll toward the cursor
- **4** — **Flame Wave**, a short cone of firebolts for packs
- **5** — **Blood Ward**, a temporary damage-reduction shield
- **6** — locked ultimate slot
- **I** — inventory & gear; inspect item cards, equip upgrades, or drop items
- **T** — talent tree; spend level-up points on connected spell and survival upgrades
- **M** — mute / unmute audio
- Leveling up pauses combat with an attribute screen for **Occult Power**, **Vitality**, **Willpower**, and **Agility**

## What's in it

Click-to-move D2 combat with a numbered skill bar, a save-slot character select, a safe gothic camp start, a first quest to slay the **Grave Brute Warden** at Depth 3, sprite-like canvas characters, procedurally generated crypts with authored gothic landmarks, distinct zombie / skeleton / demon / brute combat roles, a phased Warden boss with charges / slams / summons, rarity-colored loot with random affixes and named unique relics that change Mage skill behavior, a dedicated inventory screen with equipped relics / backpack grid / item details / equip and drop actions, XP and leveling with attribute allocation and talent points, a gothic talent tree for pyromancy / cryomancy / arcana / survival upgrades, bundled dark ARPG audio, D2-style health/mana globes, and floor-clear portals that take you deeper.

## Combat And Visual Feel

The combat target is Diablo II mood with a faster dodge-roll rhythm. Zombies swarm and lunge, skeletons kite and line up bone shots, demons orbit and cast embers, brutes charge or slam, and the Warden seals an arena before shifting through boss phases. The current tuning uses shorter cast recovery, quicker dodge recovery, lighter monster density, and small hit-stop on impacts to make combat feel more responsive.

Visual flourishes reinforce those beats: more detailed procedural sprites with stronger silhouettes, casting runes under the Mage, fire and ward lighting, deeper-floor mood shifts, boss arena sigils, charge/slam telegraphs, shockwaves, summon circles, monster death bursts, and rarity beams above magic loot.

Dungeon landmarks now break up procedural floors with recognizable room identity: **Black Sarcophagus**, **Blood Altar**, **Martyr of the Gate**, **Bone Reliquary**, and **Desecrated Fountain** set pieces can appear with labels, light, and small loot/orb rewards.

Special relic affixes can add Firebolt pierce, expand Frost Nova, add Flame Wave bolts, improve Blood Ward blocking, or shorten dodge recovery. Named uniques such as **Ashwake Brand**, **Winterglass Reliquary**, **Cinder Choir**, and **Vow of Red Glass** are early build-defining drops.

## Audio

The current build includes real CC0 music and sound effects under `assets/audio/`, with procedural WebAudio fallback cues if an asset fails to load. The target is **Diablo II mood with faster combat response**: low camp/dungeon ambience, heavier boss pulse, sharp spell impacts, a quick dodge whoosh, and restrained stone/metal UI clicks.

Bundled sources:

- [Great Labyrinth](https://opengameart.org/content/great-labyrinthorchestral-dungeon-music) and [Hard Dungeon](https://opengameart.org/content/hard-dungeon) by MintoDog — music loops.
- [80 CC0 RPG SFX](https://opengameart.org/content/80-cc0-rpg-sfx) by rubberduck — spell, monster, dodge, and loot SFX.
- [Interface Sounds](https://opengameart.org/content/interface-sounds) by Kenney — UI, error, level-up, and quest SFX.
- [Ice spells](https://opengameart.org/content/ice-spells) by bart — Frost Nova and death SFX.

See `assets/audio/ATTRIBUTION.md` for license notes.

## Run locally

Any static server works:

```bash
python -m http.server 5702
```

Then open http://localhost:5702.
