# QA-CROSS-REFERENCES

Date: 2026-06-22  
Scope: `worlds/*/curated/` cross-file reference consistency.  
Mutation note: no `worlds/*/curated` files were modified; this report is the only file written.

## Method

Used a lenient Python-based read-only audit over every `worlds/*/curated` folder. The check covered:

- `characters-index.characters[].id` vs `relationship-graph.nodes[]` and relationship endpoints.
- `relationship-graph.edges[].from/to` vs `relationship-graph.nodes[].id`.
- `knowledge-graph.edges[].from/to` vs `knowledge-graph.nodes[].id`.
- `sourceRefs`, relationship `evidence`, and KG `source.ref` vs `source-registry.sources[].sourceId`.
- `source-registry.appliesTo[].targetId` vs `world.worldId` / folder id.
- Character `factions`, `locations`, `powerSystems` vs `world.json` arrays.
- `world.json` faction knownMembers vs character ids.
- Rough/heuristic KG coverage for world factions/locations/power systems.

Because structures vary by world, this is a QA疑点 report, not an auto-fix list. Group placeholders and intentionally sparse graphs are reported at lower severity.

## Overall result

- Worlds scanned: **63**.
- Worlds with at least one finding: **51**.
- Total findings from the lenient pass: **1406**.
- Severity counts: **HIGH 379**, **MED 707**, **LOW 238**, **INFO 82**.

Category counts observed:

| Category | Count | Meaning |
|---|---:|---|
| `character-location` | 377 | Character location value not found in `world.locations[].id`. |
| `character-faction` | 287 | Character faction value not found in `world.factions[].id`. |
| `relationship-edge-node` | 187 | Relationship graph edge endpoint missing from relationship nodes. |
| `source-ref` | 178 | Source reference missing from source-registry. |
| `world-kg-coverage` | 127 | Heuristic: world power/faction/location lacks obvious KG node. |
| `character-relationship-target` | 100 | `characters-index.relationships[]` target not found as character/node; often a group placeholder. |
| `relationship-coverage` | 65 | High/critical character absent from relationship graph. |
| `character-powerSystem` | 43 | Character power system value not found in `world.powerSystems[].id`. |
| `world-faction-member` | 28 | `world.factions[].knownMembers[]` entry absent from character index. |
| `knowledge-edge-node` | 14 | Knowledge graph edge endpoint missing from KG nodes. |

No JSON parse/root-shape failures were observed in the final high-priority pass.

## Worlds with most findings

| World | Findings | HIGH | MED | LOW | INFO |
|---|---:|---:|---:|---:|---:|
| `madan-no-ou` | 179 | 70 | 101 | 1 | 7 |
| `d-gray-man` | 55 | 2 | 42 | 11 | 0 |
| `toriko` | 55 | 0 | 54 | 1 | 0 |
| `toaru` | 50 | 50 | 0 | 0 | 0 |
| `cross-ange` | 48 | 0 | 45 | 3 | 0 |
| `kekkaishi` | 46 | 1 | 41 | 4 | 0 |
| `gate-jsdf` | 42 | 1 | 31 | 10 | 0 |
| `ikki-tousen` | 41 | 3 | 32 | 6 | 0 |
| `marvel-cinematic-universe` | 39 | 0 | 20 | 18 | 1 |
| `dantalian-no-shoka` | 38 | 0 | 24 | 5 | 9 |
| `jojo` | 38 | 36 | 0 | 0 | 2 |
| `type-moon-nasuverse` | 38 | 0 | 20 | 16 | 2 |
| `dragon-ball` | 36 | 1 | 27 | 8 | 0 |
| `naruto` | 36 | 0 | 20 | 14 | 2 |
| `honkai-impact-3rd` | 35 | 0 | 18 | 14 | 3 |
| `claymore` | 33 | 32 | 0 | 0 | 1 |
| `saijaku-muhai-bahamut` | 31 | 30 | 0 | 1 | 0 |
| `zero-no-tsukaima` | 31 | 31 | 0 | 0 | 0 |
| `to-love-ru` | 30 | 28 | 0 | 2 | 0 |
| `negima-uq-holder` | 29 | 0 | 23 | 6 | 0 |

## HIGH findings: broken graph/source references

These are the most actionable issues because they can break runtime traversal or provenance lookups.

### `bocchi-the-rock` — 16 HIGH

All are `relationship-edge-node`: relationship edges reference ids not present in `relationship-graph.nodes`, including `ijichi-nijika`, `kessoku-band`, `gotoh-hitori`, `kita-ikuyo`, `yamada-ryo`, `ijichi-seika`, `starry`.

### `cheng-long-adventures` — 1 HIGH

- `knowledge-edge-node`: KG edge points to missing node `demon-magic`.

### `chunibyo` — 18 HIGH

All are `relationship-edge-node`: missing relationship nodes include `takanashi-rikka`, `togashi-yuuta`, `dekomori-sanae`, `nibutani-shinka`, `tsuyuri-kumin`, `far-east-napping-society`, `takanashi-touka`, `shichimiya-satone`, `isshiki-makoto`, `tsukumo-nanase`.

### `claymore` — 32 HIGH

All are `source-ref`: many `characters-index.characters[].sourceRefs` use values such as `characters.json entryIndex 8`, `characters.json entryIndex 4`, `characters.json entryIndex 0`, which are not registered `sourceId` values in `source-registry.json`. This looks systemic: either register these source ids or replace them with canonical `src-*` ids.

### `d-gray-man` — 2 HIGH

- `relationship-edge-node`: edge endpoint `alma-karma` missing from relationship nodes.
- `knowledge-edge-node`: KG edge endpoint `allen-walker` missing from KG nodes.

### `dragon-ball` — 1 HIGH

- `relationship-edge-node`: edge endpoint `earth` missing from relationship nodes.

### `gate-jsdf` — 1 HIGH

- `knowledge-edge-node`: KG edge endpoint `tuka-luna-marceau` missing from KG nodes.

### `haganai` — 24 HIGH

All are `relationship-edge-node`: missing relationship nodes include `hasegawa-kodaka`, `mikazuki-yozora`, `kashiwazaki-sena`, `hasegawa-kobato`, `takayama-maria`, `takayama-kate`, `rinjinbu`, `kusunoki-yukimura`, `shiguma-rika`, `hasegawa-hayato`, `kashiwazaki-pegasus`.

### `ikki-tousen` — 3 HIGH

- `knowledge-edge-node`: KG edges point to missing nodes `sonsaku-hakufu`, `ryubi-gentoku`, `sosou-moutoku`.

### `jojo` — 36 HIGH

All are `relationship-edge-node`: relationship edges reference many character ids missing from relationship nodes, including `george-joestar-i`, `jonathan-joestar`, `dio-brando`, `william-zeppelin`, `joseph-joestar`, `caesar-zeppeli`, `lisa-lisa`, `kars`, `holly-kujo`, `jotaro-kujo`, `muhammad-avdol`, `noriaki-kakyoin`, `jean-pierre-polnareff`, `iggy`, `enya`.

### `kekkaishi` — 1 HIGH

- `knowledge-edge-node`: KG edge endpoint `ayakashi` missing from KG nodes.

### `madan-no-ou` — 70 HIGH

- `relationship-edge-node`: `rel-regin-faron` points to missing `faron`.
- `knowledge-edge-node`: `edge-durandal-roland` points to missing `roland`.
- `source-ref`: most HIGH findings are `characters-index.characters[].sourceRefs` values like `src-madan-no-ou-001#entry-0`, `#entry-15`, `#entry-44..`, etc., absent from `source-registry.sources[].sourceId`. This is systemic fragment-id/provenance mismatch.

### `persona-5` — 3 HIGH

- `knowledge-edge-node`: KG edge endpoints missing: `collective-public`, `rebellion`, `free-will`.

### `record-of-ragnarok` — 2 HIGH

- `relationship-edge-node`: edge endpoints `humanity`, `gods` missing from relationship nodes.

### `saijaku-muhai-bahamut` — 30 HIGH

All are `relationship-edge-node`: edges reference missing nodes including `lux-arcadia`, `airi-arcadia`, `fugil-arcadia`, `lieselotte-atisimarta`, `philuffy-aingram`, `krulcifer-einfolk`, `celistia-ralgris`, `triad-sharis`, `triad-tillfur`, `triad-noct`, `reiri-aingram`, `academy`, `new-kingdom`, `old-empire`, `balzeride-kreutzer`, `barzeride`.

### `testament-sister-new-devil` — 28 HIGH

All are `source-ref`: `characters-index.characters[].sourceRefs` use human-readable comments such as `characters.json comment 东城刃更`, `characters.json comment 成濑澪`, etc., not registered source ids.

### `to-love-ru` — 28 HIGH

All are `relationship-edge-node`: missing nodes include `rito-yuuki`, `lala-deviluke`, `haruna-sairenji`, `mikan-yuuki`, `nana-deviluke`, `momo-deviluke`, `sastin`, `gidalucione-deviluke`, `yami`, `mea-kurosaki`, `nemesis`, `yui-kotegawa`, `run-ren`, `ryoko-mikado`.

### `toaru` — 50 HIGH

All are `source-ref`: `characters-index.characters[].sourceRefs` use values like `characters.json comment 上条当麻`, `characters.json comment 茵蒂克丝`, `characters.json comment 御坂美琴`, etc., not registered `sourceId` values. This is systemic source-id mismatch.

### `xianjian-1` — 2 HIGH

- `knowledge-edge-node`: KG edge endpoints missing: `仙灵岛事件`, `all-combat`.

### `zero-no-tsukaima` — 31 HIGH

- Mostly `relationship-edge-node`: missing endpoints include `louise-valliere`, `user-familiar`, `tabitha`, `kirche`, `guiche`, `montmorency`, `henrietta`, `wales-tudor`, `agnes`, `joseph-gallia`, `sheffield`, `josette`, `osman`, `eleonore-valliere`, `cattleya-valliere`, `siesta`, `julio-cesare`, `romalia`.
- Also `knowledge-edge-node`: endpoint `louise-valliere` missing from KG nodes.

## MED / LOW / INFO pattern notes

### 1. Localized display names vs slug ids

Most MED findings are not necessarily lore errors. They commonly show that character fields store localized names or broad labels, while `world.json` stores slug ids. Examples:

- `black-bullet`: characters use factions/locations such as `天童民间警备公司`, `民警`, `东京区域`, while world arrays likely use different ids.
- `campione`: character factions/locations include `弑神者`, `日本相关势力`, `赤铜黑十字`, `日本`, `欧洲`, etc., not matching `world.json` ids.
- `cross-ange`: many character faction/location fields use Chinese display names (`米斯尔奇皇国`, `阿尔泽纳尔`, `反恩布利欧阵营`, `原始地球`) rather than world ids.
- `d-gray-man`, `dragon-ball`, `gate-jsdf`, `gundam-seed`, `hidan-no-aria`, etc. show the same slug-vs-display-name mismatch.

Recommendation: decide whether runtime fields must be ids. If yes, normalize these arrays to world ids and keep display names in `name`/`aliases`. If no, add explicit alias/mapping support and do not treat these fields as strict foreign keys.

### 2. Relationship placeholders / secondary characters

LOW `character-relationship-target` findings often refer to groups or secondary characters that may intentionally be unindexed, e.g. `students`, `loki`, `trunks`, `bookman`, `seele`, `adventurers`. If these are intended runtime graph targets, add group nodes or character stubs; otherwise document that `characters-index.relationships[]` can contain non-resolving labels.

### 3. High/critical character coverage gaps

LOW `relationship-coverage` findings indicate high/critical characters absent from `relationship-graph.nodes`. Examples include `absolute-duo` (`sakuya`), `cross-ange` (`aura`), `d-gray-man` (`komui-lee`, `alma-karma`), `danmachi` (`liliruca-arde`, `welf-crozzo`, `ryu-lion`), `evangelion` (`asuka-langley-soryu`, `misato-katsuragi`). This may be acceptable for intentionally sparse graphs, but it reduces relationship retrieval quality.

### 4. KG coverage is heuristic

`world-kg-coverage` only compares ids/titles/aliases as strings. A missing obvious KG node for a power/faction/location is a retrieval-quality signal, not proof of broken data. It is most useful for core power systems (e.g. when `world.powerSystems[].id` has no matching KG node).

## Recommended triage order

1. Fix `relationship-edge-node` and `knowledge-edge-node` HIGH issues first: add missing nodes or correct endpoint ids.
2. Fix systemic `source-ref` HIGH issues by registering referenced ids or replacing ad-hoc comments/fragments with canonical `sourceId` values.
3. Choose an id convention for character `factions`, `locations`, and `powerSystems`; avoid mixing slug ids and localized display labels in runtime-critical fields.
4. Review high/critical character omissions from relationship graphs for worlds expected to support relationship-heavy RP retrieval.
5. If group placeholders are intentional, add group nodes or document them explicitly so QA/runtime can distinguish them from broken references.
