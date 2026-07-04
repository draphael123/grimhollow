# Grimhollow

A Diablo II-style caster action-RPG that runs entirely in the browser. A sorceress descends into a sunless crypt — wade into the dead, delete the pack, take what drops, and dive deeper.

Single-file, no build step, no dependencies — it's all `index.html`.

## Play

- **Left-click** — move; hold on a foe to cast **Firebolt**
- **Right-click** — **Frost Nova** (freezes & shatters the crowd)
- **Spacebar** — dodge roll toward the cursor (brief invulnerability)
- **I** — inventory & gear; click a bag item to equip

## What's in it

Click-to-move D2 combat with a dodge roll, procedurally generated crypts that scale with depth, three monster types with pathing / attack telegraphs / flinch / freeze, rarity-colored loot with random affixes that visibly change your damage, XP and leveling, D2-style health/mana globes, and floor-clear portals that take you deeper.

## Run locally

Any static server works:

```bash
python -m http.server 5702
```

Then open http://localhost:5702.
