# REPAIR-LOW-INFO-COVERAGE

Date: 2026-06-22

## Scope

Processed LOW/INFO coverage for the priority worlds requested by `low-info-coverage`:

- `worlds/date-a-live/curated/relationship-graph.json`
- `worlds/date-a-live/curated/knowledge-graph.json`
- `worlds/madan-no-ou/curated/relationship-graph.json`
- `worlds/madan-no-ou/curated/knowledge-graph.json`
- `worlds/dantalian-no-shoka/curated/relationship-graph.json`
- `worlds/dantalian-no-shoka/curated/knowledge-graph.json`
- `worlds/naruto/curated/relationship-graph.json`
- `worlds/naruto/curated/knowledge-graph.json`
- `worlds/marvel-cinematic-universe/curated/relationship-graph.json`
- `worlds/marvel-cinematic-universe/curated/knowledge-graph.json`
- `worlds/type-moon-nasuverse/curated/relationship-graph.json`
- `worlds/type-moon-nasuverse/curated/knowledge-graph.json`

No `characters-index.json` relationship notes were changed in this pass.

## Policy

- Added relationship graph nodes only for entities already present in curated `characters-index.json` or directly referenced by existing relationship strings.
- Added minimal KG nodes for existing curated characters to improve retrieval coverage.
- Did not expand unverified lore; added summaries from existing curated character summaries where available.
- Aggregate entries were modeled as `group`, not `character`.
- Relationship-string targets that are not in the local character index were marked `resolutionStatus: external-minimal` and noted as coverage-only nodes.

## Per-world actions

### `date-a-live`

- Added missing relationship/KG coverage for the existing aggregate entry `ch-date-a-bullet-minors` as `type: group` with `resolutionStatus: aggregate-placeholder`.
- Added minimal KG character nodes for existing indexed core characters missing from KG, including the main spirits, Ratatoskr/DEM-related characters, and Date A Bullet branch characters.
- Added a small relationship edge from `ch-higoromo-hibiki` to the aggregate Date A Bullet minors group to make the branch retrievable without inventing individual NPC identities.

### `madan-no-ou`

- Added relationship graph nodes for indexed characters missing from the graph: `badouin`, `guinevere`, `finilia-alshavin`, `eugene`, `greast`, `zacharias`, `liudie`, `augustus`.
- Added minimal KG nodes for indexed characters missing from KG, using existing character summaries only.
- Left unresolved MED items from the normalization pass untouched (`roland.powerSystems: 杜兰达尔`, `eugene.factions: 王室`).

### `dantalian-no-shoka`

- Added relationship graph nodes for indexed characters missing from the graph, covering episodic characters and minor case figures that were already in `characters-index.json`.
- Added minimal KG nodes for all indexed characters, because the KG previously lacked character-node coverage.
- Did not add speculative case relationships beyond existing curated identity coverage.

### `naruto`

- Added relationship graph nodes for indexed missing characters: `itachi-uchiha`, `pain`, `obito-uchiha`, `madara-uchiha`, `jiraiya`, `tsunade`.
- Added minimal external nodes for relationship-string targets not in the local character index: `kisame-hoshigaki`, `konan`, `rin-nohara`, `hashirama-senju`, `orochimaru`.
- Added two high-impact relationship edges supported by existing relationship strings: `itachi-uchiha -> sasuke-uchiha` and `pain -> naruto-uzumaki`.
- Added minimal KG nodes for all indexed characters.

### `marvel-cinematic-universe`

- Added relationship graph nodes for indexed missing characters: `thor-odinson`, `bruce-banner`, `natasha-romanoff`, `doctor-strange`, `peter-parker`.
- Added minimal external nodes for relationship-string targets not in the local character index: `pepper-potts`, `bucky-barnes`, `loki`, `clint-barton`, `wong`, `gamora`, `may-parker`.
- Added two high-impact relationship edges supported by existing relationship strings: `tony-stark -> peter-parker` and `thor-odinson -> avengers`.
- Added minimal KG nodes for all indexed characters.

### `type-moon-nasuverse`

- Added relationship graph nodes for indexed missing characters: `sakura-matou`, `illyasviel`, `gilgamesh`, `ritsuka-fujimaru`, `mash-kyrielight`, `kirei-kotomine`.
- Added minimal external nodes for relationship-string targets not in the local character index: `archer-emiya`, `zouken-matou`, `berserker-heracles`, `romani-archaman`, plus `holy-church` as `type: faction`.
- Added two high-impact relationship edges supported by existing relationship strings: `sakura-matou -> shirou-emiya` and `ritsuka-fujimaru -> mash-kyrielight`.
- Added minimal KG nodes for all indexed characters.

## Validation

Focused validation was run locally after edits:

```text
date-a-live: chars=24 relNodes=30 kgNodes=52 missingR=0 missingK=0 danglingRel=0
madan-no-ou: chars=34 relNodes=40 kgNodes=58 missingR=0 missingK=0 danglingRel=0
dantalian-no-shoka: chars=46 relNodes=51 kgNodes=68 missingR=0 missingK=0 danglingRel=0
naruto: chars=10 relNodes=17 kgNodes=14 missingR=0 missingK=0 danglingRel=0
marvel-cinematic-universe: chars=8 relNodes=17 kgNodes=12 missingR=0 missingK=0 danglingRel=0
type-moon-nasuverse: chars=9 relNodes=16 kgNodes=12 missingR=0 missingK=0 danglingRel=0
validation OK
```

Additional KG edge validation:

```text
date-a-live: kgDangling=0
madan-no-ou: kgDangling=0
dantalian-no-shoka: kgDangling=0
naruto: kgDangling=0
marvel-cinematic-universe: kgDangling=0
type-moon-nasuverse: kgDangling=0
```

## Remaining risks

- External-minimal relationship nodes are coverage stubs only; they should not be treated as fully curated indexed characters.
- `dantalian-no-shoka` now has broad minimal character KG coverage, but many case-specific relationships remain intentionally unexpanded pending stronger source review.
- This pass did not address global non-priority worlds or MED/source issues already assigned to other repair steps.
