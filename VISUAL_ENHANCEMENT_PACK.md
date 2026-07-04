# Grimhollow Visual Enhancement Pack

**Goal:** Raise perceived visual quality from ~8.5 to ~9.0 while preserving the single-file HTML architecture, mobile touch layout, and current combat/loot systems.

**Scope:** Art replacement and UI polish — no gameplay rewrites. Builds on the Phase 1 combat-feel pass (Smite rework, denser packs, loot ceremony, crit floaters).

**Out of scope (this pack):** New zones, class rewrites, netcode, engine migration.

---

## 1. Pack Overview

| Phase | Focus | Target lift |
|-------|--------|-------------|
| **A — Hero & HUD** | Paladin sheets, skill icons, mobile buttons | +0.25 |
| **B — Monsters** | Zombie, skeleton, demon, brute roster | +0.20 |
| **C — Environments** | Town, forest stages, dungeon tiles, landmarks | +0.25 |
| **D — VFX & Audio-visual** | Spell sprites, hit FX, elite auras, loot beams | +0.15 |
| **E — UI Polish** | Char select, inventory paper-doll, talent tree chrome | +0.15 |

**Delivery model:** PNG sprite sheets + JSON frame manifests (or inline atlas metadata). Keep procedural fallbacks in `index.html` until each asset class is swapped.

**Success criteria:**
- No regression on 375px mobile width
- 60 FPS on mid-tier laptop with full dungeon pack
- All assets under `assets/` with documented naming (see §9)

---

## 2. Character Art

### Paladin 4-direction sheets
| State | Frames/dir | Notes |
|-------|------------|-------|
| Idle | 5 | Subtle breathing, sword at rest |
| Walk | 8 | Greaves + cape sway; match `WALK_KEYFRAMES` bob |
| Cast | 4 | Holy flash on frame 2; Smite melee vs bolt variants |
| Hurt | 2 | Plate clank tilt |
| Death | 3 | Collapse + shield drop |

**Directions:** N, E, S, W (or 8-dir if budget allows; renderer currently uses `facing` ±1).

**Gear overlays (draw order):**
1. Body base
2. Armor tint by slot equipped
3. Weapon (Training Sword → unique silhouettes)
4. Shield / offhand
5. Helm (optional hide hair)

**Palette:** `#d9b45a` holy gold accent, `#8a8470` plate mid, `#2a2418` shadow.

**Files:**
```
assets/sprites/paladin/idle_{n,e,s,w}.png
assets/sprites/paladin/walk_{n,e,s,w}.png
assets/sprites/paladin/cast_{n,e,s,w}.png
assets/sprites/paladin/hurt_{n,e,s,w}.png
assets/sprites/paladin/death_{n,e,s,w}.png
assets/sprites/paladin/gear_weapon.png
assets/sprites/paladin/gear_shield.png
```

---

## 3. Monster Art — Priority Roster

| Monster | Priority | Frames | Elite variant |
|---------|----------|--------|---------------|
| **Zombie / Lost Dead** | P0 | idle 4, walk 6, attack 3, death 3 | Green aura tint |
| **Skeleton archer** | P0 | idle 4, walk 6, draw 2, death 4 (collapse) | Frost affix blue |
| **Demon** | P1 | idle 4, walk 6, cast 4, death 3 | Molten death FX hook |
| **Brute / Warden** | P1 | idle 3, walk 4, windup 3, slam 2, death 4 | Boss scale 1.4× |

**Size guides (world px, `r` radius):**
- Zombie `r≈14` → sheet ~48×48 cell
- Skeleton `r≈13` → 44×44
- Demon `r≈16` → 52×52
- Brute `r≈22` (Warden 30) → 64×64 / 80×80

**Pack composition tie-in:** Frontline zombies face camera; skeletons offset back — silhouettes must read at 50% scale.

```
assets/sprites/monsters/zombie_sheet.png
assets/sprites/monsters/skeleton_sheet.png
assets/sprites/monsters/demon_sheet.png
assets/sprites/monsters/brute_sheet.png
assets/sprites/monsters/elite_aura.png   # additive ring, 64×64
```

---

## 4. Environment

### Town (Grimhollow Hamlet)
- Cobble + grass transition tiles 32×32
- Stash building, NPC porch, well prop as PNG overlays
- Warm torch `drawLight` anchors — replace procedural candles with sprite

### Forest stages (1–3)
| Stage | Mood | Unique landmarks |
|-------|------|------------------|
| 1 | Safe path, green | Trail markers, fallen log |
| 2 | Mist, first combat | Broken wagon, corpse prop |
| 3 | Dusk, crypt gate | Gate arch PNG, 4–5 spawn clearings |

### Dungeon tilesets
- Wall, floor, door, pillar — 32×32 seamless
- Depth tint overlays (depth 1 warm stone → depth 3+ violet)
- Landmarks: reliquary, blood altar, sarcophagus as 64×64 props

```
assets/tiles/town_floor.png
assets/tiles/town_wall.png
assets/tiles/forest_floor_{1,2,3}.png
assets/tiles/dungeon_floor.png
assets/tiles/dungeon_wall.png
assets/props/crypt_gate.png
assets/props/reliquary.png
```

---

## 5. UI/UX

### Character select (D2 polish)
- Full-bleed background illustration (hamlet at dusk)
- Paladin figure: use idle south sheet at 2×
- Slot cards: embossed frame, level/depth metadata
- Hover: gold border pulse matching `#d9b45a`

### Inventory
- Paper-doll silhouette with slot hotspots
- Rarity frame borders per `RARITIES` colors
- Compare tooltip on hover (desktop) / long-press (mobile)

### Skill icons (64×64)
| Slot | Icon |
|------|------|
| 1 Smite | Crossed sword + holy burst |
| 2 Firebolt | Ember bolt |
| 3 Frost Nova | Ice ring |
| 4 Lightning | Forked arc |
| 5 Flame Wave | Fan of fire |
| 6 Blood Ward | Crimson hex |

### Mobile HUD
- Smite button: holy gold gradient, separate CD ring from Firebolt
- Joystick: stone texture cap
- Potion orbs: match ground loot colors

```
assets/ui/frame_panel.png
assets/ui/skill_smite.png
assets/ui/skill_firebolt.png
...
assets/ui/mobile_attack.png
```

---

## 6. VFX

| Effect | Spec | Replaces |
|--------|------|----------|
| **Holybolt** | 8-frame streak, gold core | Procedural circle + cross |
| **Holystrike** | Radial burst 12 frames | `addFx('burst')` gold |
| **Firebolt / Flame** | Orange trail particles | Current gradient trails |
| **Frost Nova** | Expanding ring sprite sheet | `kind:'nova'` arc stroke |
| **Lightning** | Branch overlay PNG | Line + spark |
| **Hit impact** | 6-frame flash per element | `drawImpactFx` |
| **Elite auras** | Looping 8-frame rim | `drawMonsterSprite` tint |
| **Loot beam** | Vertical column per rarity | `drawGroundLoot` gradient |
| **Crit floater** | Optional starburst behind text | Yellow `!` suffix |

**Atlas:** `assets/vfx/combat_fx.png` — 512×512, 64×64 cells.

---

## 7. Audio-Visual Sync

Pairs with Phase 1 combat changes:

| Game event | Visual | Audio |
|------------|--------|-------|
| Smite melee | Holystrike burst + spark shower | `smite` (holy tone) |
| Smite bolt | Holybolt cross-trail | `smite` |
| Crit hit | Yellow `!` floater + scale pop | Pitch-up `hitRage` layer |
| Kill blow | `SLAIN` pop + hit-stop | `kill` + brief music duck |
| Loot drop magic+ | Label floater + beam | `lootMagic` |
| Loot drop rare+ | Stronger beam + star motes | `lootRare` / `lootEpic` |
| Pack engage | Front zombie + back skeleton silhouettes | Footstep + dungeon music layer |
| Elite death | Molten burst palette | `bossPhase` undertone |

**Optional:** Record 0.1s music sidechain dip on kill blow for D2-style punch.

---

## 8. Sprint Breakdown

| Sprint | Work | Est. | Depends on |
|--------|------|------|------------|
| **S1** | Asset pipeline + Paladin idle/walk/cast (4-dir) | 1.5 wk | — |
| **S2** | Zombie + skeleton sheets, pack silhouette test | 1 wk | S1 loader |
| **S3** | Dungeon + forest floor/wall tiles, crypt gate | 1.5 wk | — |
| **S4** | Skill icons, HUD frames, mobile buttons | 1 wk | S1 |
| **S5** | Holy/combat VFX atlases, loot beams, crit FX | 1 wk | S1, S2 |
| **S6** | Demon, brute, Warden boss, town props, char select BG | 1.5 wk | S2, S3 |

**Total:** ~7.5 weeks solo artist-dev; ~4 weeks with parallel artist + code integration.

**Integration checkpoints:** End of each sprint — deploy preview to Vercel, smoke test desktop + mobile.

---

## 9. Asset Specs

### Dimensions
| Category | Size | Format |
|----------|------|--------|
| Tiles | 32×32 | PNG-24 + alpha |
| Props | 64×64 – 128×128 | PNG |
| Character cells | 48×48 – 64×64 | PNG |
| UI icons | 64×64 | PNG |
| VFX frames | 64×64 | PNG additive-friendly |
| Backgrounds | 1280×720 | WebP or PNG |

### Palette discipline
- Backgrounds: desaturate 15% vs characters
- Holy: `#d9b45a`, `#ffe08a`, `#fff8d0`
- Fire: `#ff8a3a` → `#ff4a22`
- Frost: `#7fd8ff` → `#5a9aff`
- Blood/ward: `#ff6060`
- UI chrome: `#8a6426` border, `rgba(8,9,14,0.98)` fill

### File naming convention
```
assets/{category}/{entity}_{variant}_{state}.png
assets/{category}/{entity}_sheet.png   # spritesheet alternative
```
- Lowercase, underscore separators
- No spaces; version suffix only if iterating (`_v2`)

### Loader contract (for `preloadSprites`)
```json
{
  "paladin_walk_e": { "sheet": "assets/sprites/paladin/walk_e.png", "fw": 48, "fh": 48, "frames": 8, "fps": 11 }
}
```

---

## Top 3 Priorities (start here)

1. **Paladin 4-dir walk + cast sheets** — Most screen time; immediately upgrades every scene.
2. **Zombie + skeleton monster sheets** — Forest tutorial and dungeon packs are 80% of combat screen.
3. **Holy VFX atlas (Smite bolt + melee burst)** — Locks in the new combat identity from Phase 1.

---

*Document version: 1.0 — post combat-feel deploy*
