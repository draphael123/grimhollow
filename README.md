# Grimhollow

A Diablo II-style holy warrior action-RPG that runs entirely in the browser. A **Paladin** awakens in peaceful Grimhollow hamlet — hear the elders, cross the wood in three stages, and descend the sunless crypt when the dead grow restless.

Single-file, no build step, no dependencies — it's all `index.html`.

## Start

Choose a save slot from the Diablo II-style character select screen. The **Paladin** is the only selectable class for now; other class cards are locked placeholders. Each slot saves Paladin progression in `localStorage`.

**World flow:** Town (peaceful, NPCs, stash, no combat) → Forest 1 (tutorial path) → Forest 2 (first combat) → Forest 3 (crypt gate) → Dungeon depths.

## Play

### Desktop
- **Left-click** — move; talk to NPCs or stash; hold on a foe to cast **Smite**
- **1** — **Smite** (basic holy bolt)
- **2–6** — unlock through the talent tree
- **Spacebar** — dodge roll toward cursor (35 stamina)
- **Q** — health potion · **E** — mana potion (or talk / open stash when near NPCs in town)
- **I** — inventory · **T** — talents · town **stash** stores spare gear

### Mobile / touch
- Virtual **joystick** (bottom-left) for movement
- **Smite**, **Dodge**, contextual **Talk**, and **Inv** buttons (bottom-right)
- Tap skill bar icons and HP/MP flasks (44px+ targets)
- Auto-aim assist toward nearest foe when using Smite
- Landscape orientation recommended for ARPG feel

## What's in it

Click-to-move D2 combat with town → forest → crypt progression, Smite and talent-unlocked fire / frost / lightning / ward abilities, save slots, Grave Brute Warden quest at Depth 3, procedural crypts, elite affixes, rarity loot, inventory paper-doll, potions, stamina dodge, XP/talents/attributes, bundled dark ARPG audio, and mobile-friendly touch controls.

## Mobile (touch devices)

On phones and tablets, Grimhollow auto-detects touch input and switches to a mobile control layout:

- **Virtual joystick** (bottom-left) — hold and drag to move
- **Smite** (bottom-right) — hold to attack; auto-aims the nearest foe within range
- **Dodge** — roll toward aim direction (costs stamina)
- **Talk / Stash** — appears contextually when near NPCs or the town stash
- **INV / T** — inventory and talent tree shortcuts
- **Skill bar & potion flasks** — tap targets sized for fingers (44px+)
- **Safe-area insets** — controls respect notched screens; pinch-zoom disabled during play

Landscape orientation is recommended. Desktop keyboard and mouse controls remain fully supported.

## Run locally

```bash
python -m http.server 5702
```

Then open http://localhost:5702.

Production: https://grimhollow.vercel.app
