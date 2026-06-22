# REPAIR-GRAPH-HIGH

Date: 2026-06-22  
Scope: HIGH `relationship-edge-node` / `knowledge-edge-node` endpoint repairs for the delegated target worlds.

## Target worlds

`bocchi-the-rock`, `cheng-long-adventures`, `chunibyo`, `d-gray-man`, `dragon-ball`, `gate-jsdf`, `haganai`, `ikki-tousen`, `jojo`, `kekkaishi`, `madan-no-ou`, `persona-5`, `record-of-ragnarok`, `saijaku-muhai-bahamut`, `to-love-ru`, `xianjian-1`, `zero-no-tsukaima`.

## Method

- Did not rewrite edge meanings.
- Converted endpoint-only/string relationship nodes into object nodes where needed.
- Added or enriched minimal endpoint nodes with `id`, `type`, and `label`.
- Labels/types were taken from existing `characters-index.json` character ids/names, `world.json` organizations/locations/factions/power systems, or the immediate KG/edge context for concept/event/scope endpoints.
- Removed mechanical `referenced-placeholder` status where a node could be resolved to a character, faction, location, organization, power-system, concept, event, role, or scope.

## Files changed

Relationship graph files:

- `worlds/bocchi-the-rock/curated/relationship-graph.json`
- `worlds/chunibyo/curated/relationship-graph.json`
- `worlds/d-gray-man/curated/relationship-graph.json`
- `worlds/dragon-ball/curated/relationship-graph.json`
- `worlds/haganai/curated/relationship-graph.json`
- `worlds/ikki-tousen/curated/relationship-graph.json`
- `worlds/jojo/curated/relationship-graph.json`
- `worlds/kekkaishi/curated/relationship-graph.json`
- `worlds/madan-no-ou/curated/relationship-graph.json`
- `worlds/record-of-ragnarok/curated/relationship-graph.json`
- `worlds/saijaku-muhai-bahamut/curated/relationship-graph.json`
- `worlds/to-love-ru/curated/relationship-graph.json`
- `worlds/zero-no-tsukaima/curated/relationship-graph.json`

Knowledge graph files:

- `worlds/cheng-long-adventures/curated/knowledge-graph.json`
- `worlds/d-gray-man/curated/knowledge-graph.json`
- `worlds/gate-jsdf/curated/knowledge-graph.json`
- `worlds/ikki-tousen/curated/knowledge-graph.json`
- `worlds/kekkaishi/curated/knowledge-graph.json`
- `worlds/madan-no-ou/curated/knowledge-graph.json`
- `worlds/persona-5/curated/knowledge-graph.json`
- `worlds/xianjian-1/curated/knowledge-graph.json`
- `worlds/zero-no-tsukaima/curated/knowledge-graph.json`

## Notable repairs

- `bocchi-the-rock`: relationship endpoints for the band members, `kessoku-band`, and `starry` are now object nodes with character/organization/location labels.
- `chunibyo`: relationship endpoints for the core cast and `far-east-napping-society` are now object nodes.
- `d-gray-man`: added/resolved `alma-karma` in relationship graph and `allen-walker` in KG.
- `dragon-ball`: resolved `earth` as a location endpoint.
- `gate-jsdf`: resolved KG `tuka-luna-marceau` as a character endpoint.
- `haganai`: relationship endpoints for the core cast and `rinjinbu` are now object nodes.
- `ikki-tousen`: resolved KG endpoints `sonsaku-hakufu`, `ryubi-gentoku`, `sosou-moutoku` as character nodes.
- `jojo`: relationship endpoints for the listed Joestar / ally / antagonist characters are now object nodes.
- `kekkaishi`: resolved KG `ayakashi` as a species/concept node.
- `madan-no-ou`: resolved relationship endpoint `faron` and KG endpoint `roland` from existing character index evidence.
- `persona-5`: resolved KG concept endpoints `collective-public`, `rebellion`, and `free-will`.
- `record-of-ragnarok`: resolved relationship endpoints `humanity` and `gods` as faction nodes.
- `saijaku-muhai-bahamut`: relationship endpoints for character ids plus `academy`, `new-kingdom`, and `old-empire` are now object nodes.
- `to-love-ru`: relationship endpoints for the listed character ids are now object nodes.
- `xianjian-1`: resolved KG endpoints `仙灵岛事件` and `all-combat` as event/scope nodes.
- `zero-no-tsukaima`: relationship endpoints for cast/role/faction nodes are now object nodes; KG `louise-valliere` resolved as a character node.

## Validation

Ran JSON endpoint validation over the 17 target worlds and both graph types where present:

- Graph files validated: 34
- All graph JSON files parsed successfully.
- All `edges[].from` / `edges[].to` endpoints resolve to object `nodes[].id`.
- No non-object nodes remain in target graph `nodes` arrays.
- No duplicate node ids were found in target graph `nodes` arrays.

Validation summary by target graph:

| World | Graph | Nodes | Edges |
|---|---|---:|---:|
| bocchi-the-rock | relationship | 7 | 8 |
| bocchi-the-rock | knowledge | 8 | 7 |
| cheng-long-adventures | relationship | 12 | 10 |
| cheng-long-adventures | knowledge | 11 | 6 |
| chunibyo | relationship | 10 | 9 |
| chunibyo | knowledge | 7 | 6 |
| d-gray-man | relationship | 10 | 8 |
| d-gray-man | knowledge | 8 | 6 |
| dragon-ball | relationship | 9 | 7 |
| dragon-ball | knowledge | 9 | 6 |
| gate-jsdf | relationship | 9 | 9 |
| gate-jsdf | knowledge | 13 | 10 |
| haganai | relationship | 12 | 12 |
| haganai | knowledge | 8 | 7 |
| ikki-tousen | relationship | 8 | 6 |
| ikki-tousen | knowledge | 11 | 7 |
| jojo | relationship | 15 | 18 |
| jojo | knowledge | 11 | 9 |
| kekkaishi | relationship | 8 | 7 |
| kekkaishi | knowledge | 9 | 7 |
| madan-no-ou | relationship | 32 | 33 |
| madan-no-ou | knowledge | 33 | 28 |
| persona-5 | relationship | 17 | 12 |
| persona-5 | knowledge | 13 | 8 |
| record-of-ragnarok | relationship | 8 | 5 |
| record-of-ragnarok | knowledge | 6 | 4 |
| saijaku-muhai-bahamut | relationship | 16 | 15 |
| saijaku-muhai-bahamut | knowledge | 15 | 11 |
| to-love-ru | relationship | 14 | 14 |
| to-love-ru | knowledge | 11 | 6 |
| xianjian-1 | relationship | 16 | 14 |
| xianjian-1 | knowledge | 12 | 5 |
| zero-no-tsukaima | relationship | 19 | 15 |
| zero-no-tsukaima | knowledge | 12 | 9 |

A read-only repo-wide endpoint sweep over `worlds/*/curated/{relationship-graph,knowledge-graph}.json` also reported `world graph endpoint errors: 0` at this point.

## Residual risks

- Some newly materialized nodes are intentionally minimal and do not add new relationship prose.
- Concept/scope labels such as `all-combat` are based on local edge context rather than a richer curated lore entry.
- This pass only addresses graph endpoint integrity; source registry, character faction/location normalization, and KG coverage quality remain separate QA categories.
