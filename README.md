# Grimhollow

A Diablo II-style caster action-RPG that runs entirely in the browser. A sorceress wakes in a haunted forest outside a sunless crypt — learn the basics, cross the grave gate, break the dead, take what drops, and dive deeper.

Single-file, no build step, no dependencies — it's all `index.html`.

## Start

Choose a save slot from the Diablo II-style character select screen. The **Mage** is the only selectable class for now; other class cards are locked placeholders for future work. Each slot saves Mage progression in `localStorage`.

## Play

- **Left-click** — move; hold on a foe to cast starter **Rage Bolt**
- **1** — **Rage Bolt**, the basic staff projectile
- **2-6** — blank until abilities are unlocked through the talent tree
- **Spacebar** — dodge roll toward the cursor (costs **35 stamina**); a **Space — dodge (35)** hint glows above the skill bar when ready
- **Stamina bar** — pale blue rail (`#c8d8ff`) between the health and mana globes shows current / max stamina and ticks back up after dodge or **Blood Ward** (40 stamina + 12 mana)
- **Q** — drink a health potion
- **E** — drink a mana potion
- **I** — inventory & gear; inspect item cards, equip upgrades, or drop items
- **T** — talent tree; unlock Firebolt, Frost Nova, Lightning Arc, Flame Wave, Blood Ward, and upgrades
- **M** — mute / unmute audio
- Leveling grants talent and attribute points without pausing combat; a pulsing HUD icon appears when points are unspent (click it or press **T** for talents)

## What's in it

Click-to-move D2 combat with an authored forest tutorial start, a sparse skill bar that begins with Rage Bolt, talent-unlocked fire / frost / lightning / ward abilities, a save-slot character select, a first quest to slay the **Grave Brute Warden** at Depth 3, sprite-like canvas characters, procedurally generated crypts with authored gothic landmarks, distinct zombie / skeleton / demon / brute combat roles, elite affix monsters with bonus drops, a phased Warden boss with charges / slams / summons, rarity-colored loot across Diablo-like equipment slots, named unique relics that change Mage skill behavior, an inventory screen with weapon / offhand / helm / armor / gloves / boots / belt / amulet / two ring slots, refillable health and mana potions, a stamina pool for dodge and Blood Ward, XP and leveling with attribute allocation and talent points, bundled dark ARPG audio, D2-style health/mana globes with a stamina rail between them, and floor-clear portals that take you deeper.

## Combat And Visual Feel

The combat target is Diablo II mood with a faster dodge-roll rhythm gated by stamina. Dodge costs 35 stamina (regenerates at 20/s out of combat, 14/s while fighting or recently hit); Blood Ward costs 40 stamina and 12 mana. Zombies swarm and lunge, skeletons kite and line up bone shots, demons orbit and cast embers, brutes charge or slam, and the Warden seals an arena before shifting through boss phases. **Elite** foes in the crypt roll Diablo-style affixes (Molten, Vampiric, Fast, Frost, Arcane, Plague), hit harder, and drop bonus loot. The current tuning uses shorter cast recovery, quicker dodge recovery, lighter monster density, and small hit-stop on impacts to make combat feel more responsive.

Visual flourishes reinforce those beats: D2-style **four-direction facing** (N/E/S/W) for the Mage and monsters, frame-based idle/walk/cast/hurt animation, **type-specific death animations** (skeleton crumbles, demon dissolves, zombie collapses, brute falls), **gear-driven armor layers** (helm, robe/plate, gloves, boots, belt, weapon, offhand) with rarity-colored trim, an **inventory paper-doll** mirroring equipped gear, stronger procedural silhouettes, casting runes under the Mage, fire and ward lighting, deeper-floor mood shifts, boss arena sigils, charge/slam telegraphs, shockwaves, summon circles, monster death bursts, and rarity beams above magic loot.

The forest tutorial now has a readable path to the crypt, layered canopy shadows and moonlight, foreground parallax, placed trees / stones / signposts, fireflies, a gothic objective panel, tutorial enemy callouts with soft green undead silhouettes, starter potion refills, and a gate that asks the player to clear the nearby dead before entering. The Mage begins in plain robes; equipping loot immediately updates the on-canvas paper-doll look.

Dungeon landmarks now break up procedural floors with recognizable room identity: **Black Sarcophagus**, **Blood Altar**, **Martyr of the Gate**, **Bone Reliquary**, **Desecrated Fountain**, and a per-floor **Graveyard of Echoes** set piece can appear with labels, light, and small loot/orb rewards. Death sends you back to the nearest graveyard instead of a run summary — you keep level, XP, talents, and equipped gear, but lose a portion of backpack items.

The forest camp has a gentler graveyard respawn at the starting fire (10–18% backpack loss). Dungeon deaths cost 25–40% of bag items (random selection; equipped gear is never touched).

Special relic affixes can add Firebolt pierce, expand Frost Nova, add Flame Wave bolts, improve Blood Ward blocking, shorten dodge recovery, or increase potion capacity through belts. Named uniques such as **Ashwake Brand**, **Winterglass Reliquary**, **Cinder Choir**, and **Vow of Red Glass** are early build-defining drops.

## Audio

The current build includes real CC0 music and sound effects under `assets/audio/`, with procedural WebAudio fallback cues if an asset fails to load. The target is **Diablo II mood with faster combat response**: low camp/dungeon ambience, heavier boss pulse, sharp spell impacts, element-distinct hit sounds (fire, frost, lightning, rage), surface-aware footsteps (grass, dirt, stone, dungeon), a boss phase transition sting, a quick dodge whoosh, and restrained stone/metal UI clicks.

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
