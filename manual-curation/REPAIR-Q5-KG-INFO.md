# Q5 KG INFO Repair

Scope: non-blocking Q5 KG INFO convergence for worlds with high residual INFO after Q4.

## Objective

For the target worlds, ensure every `world.json` entity listed under `factions`, `locations`, and `powerSystems` is either represented by a minimal KG node or has an explicit non-graphing rationale. This pass graphized all in-scope residual entities, so no non-graphing exceptions were needed.

## Files Mutated

- `worlds/type-moon-nasuverse/curated/knowledge-graph.json`
- `worlds/date-a-live/curated/knowledge-graph.json`
- `worlds/danmachi/curated/knowledge-graph.json`
- `worlds/negima-uq-holder/curated/knowledge-graph.json`
- `worlds/ikki-tousen/curated/knowledge-graph.json`
- `worlds/kekkaishi/curated/knowledge-graph.json`
- `worlds/kenichi/curated/knowledge-graph.json`
- `worlds/gundam-seed/curated/knowledge-graph.json`
- `worlds/persona-5/curated/knowledge-graph.json`
- `worlds/rozen-maiden/curated/knowledge-graph.json`
- `worlds/sekirei/curated/knowledge-graph.json`
- `manual-curation/REPAIR-Q5-KG-INFO.md`

No `world.json`, `characters-index.json`, `relationship-graph.json`, raw/import files, or out-of-scope worlds were changed.

## Repair Actions

Added minimal KG nodes for missing `world.json` factions, locations, and power systems. Each added node uses the existing world entity id when available, carries a minimal `label` and `summary`, and is marked with:

- `resolutionStatus`: `q5-world-entity-minimal`
- `notes`: `Q5 KG INFO: Added from curated world.json factions/locations/powerSystems for minimal graph coverage.`

For legacy KG edge compatibility, every in-scope edge that had `from`/`to` but lacked `source`/`target` received mirrored `source` and `target` fields. The original `from`/`to` fields were preserved.

Each modified KG also received `metadata.q5KgInfoRepair` with added-node count and scope notes.

## Added Node Counts

| World | Added minimal KG nodes |
| --- | ---: |
| `type-moon-nasuverse` | 20 |
| `date-a-live` | 14 |
| `danmachi` | 10 |
| `negima-uq-holder` | 10 |
| `ikki-tousen` | 7 |
| `kekkaishi` | 8 |
| `kenichi` | 10 |
| `gundam-seed` | 11 |
| `persona-5` | 11 |
| `rozen-maiden` | 6 |
| `sekirei` | 6 |
| **Total** | **113** |

## Non-Graphing Decisions

None. All in-scope `world.json` entries under `factions`, `locations`, and `powerSystems` now have KG node coverage by id or label.

## Validation

A local Python QA pass loaded all 11 target `world.json` and `knowledge-graph.json` files and checked:

- no duplicate `nodes[].id`
- every `world.json` faction/location/powerSystem is covered by KG id or label
- every KG edge resolves to existing nodes using `source`/`target` with fallback to `from`/`to`

Result: all 11 target worlds passed with `dups 0`, `missing 0`, and `broken 0`.

## Risks / Notes

- This is intentionally minimal KG coverage, not lore expansion. Added summaries are sourced from existing `world.json` fields where present, or a generic coverage note for string-only faction entries.
- Some KGs use older rich fields such as `title`, `visibility`, `strength`, `from`, and `to`; this pass preserved them and only added compatible minimal fields.
- Shared IDs in `world.json` across categories, such as combined place/faction concepts, were represented as a single KG node with a combined type when encountered during this pass.
