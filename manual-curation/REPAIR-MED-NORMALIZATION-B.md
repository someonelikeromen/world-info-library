# REPAIR-MED-NORMALIZATION-B

## Scope

Target worlds handled in this MED normalization pass:

- `worlds/honkai-impact-3rd/curated/world.json`
- `worlds/honkai-impact-3rd/curated/characters-index.json`
- `worlds/naruto/curated/world.json`
- `worlds/naruto/curated/characters-index.json`
- `worlds/marvel-cinematic-universe/curated/world.json`
- `worlds/marvel-cinematic-universe/curated/characters-index.json`
- `worlds/cross-ange/curated/world.json`
- `worlds/cross-ange/curated/characters-index.json`
- `worlds/gundam-seed/curated/world.json`
- `worlds/gundam-seed/curated/characters-index.json`
- `worlds/toriko/curated/world.json`
- `worlds/toriko/curated/characters-index.json`

No `curation-notes.md` files were changed in this pass; per-character `normalizationNotes` were used where residual semantics needed to be preserved.

## Actions

### General

- Converted string-only `world.locations` into canonical id objects for the six target worlds where the display name was already clearly present in the curated file.
- Converted string-only or display-name-heavy `world.factions` into canonical id objects for `cross-ange`, `gundam-seed`, and `toriko`; added missing obvious faction ids in `honkai-impact-3rd`, `naruto`, and `marvel-cinematic-universe`.
- Updated character references in `characters-index.json` for the main MED categories:
  - `character-location`
  - `character-faction`
  - `character-powerSystem`
  - supporting `world-faction-member` / `territories` refs where directly obvious
- Preserved original display strings through object `aliases` and per-character `normalizationNotes`.
- Regenerated `characters-index.json:indices.byFaction`, `indices.byPowerSystem`, `indices.byVisibility`, `indices.byId`, and `indices.byName` for the six target worlds after normalization.

### World-specific notes

- `honkai-impact-3rd`
  - Added canonical location ids such as `st-freya-academy`, `schicksal-hq`, `anti-entropy-base`, `sea-of-quanta`, `elysian-realm`, `shenzhou`, `world-serpent-base`.
  - Added canonical faction ids `st-freya`, `former-era`.
  - Added `martial-arts` as a technique-class powerSystem for Fu Hua-related martial technique tagging instead of leaving it dangling.

- `naruto`
  - Added canonical location ids for the major villages and special/narrative locations, including `konohagakure`, `mount-myoboku`, `amegakure`, `otogakure-related-base`, `kamui-dimension`, `historical-battlefields`.
  - Added obvious factions `uchiha-clan`, `amegakure`, `mount-myoboku`.
  - Added `senjutsu` powerSystem for character references to仙术/自然能量.

- `marvel-cinematic-universe`
  - Added canonical location ids such as `new-york`, `avengers-compound`, `wakanda`, `asgard`, `kamar-taj`, `quantum-realm`, `titan`, `new-york-sanctum`, `earth`, `cosmos`, `united-states`.
  - Added obvious factions `asgard`, `black-order`, `masters-of-mystic-arts`, `stark-industries`.
  - Added `asgardian-divinity` powerSystem.
  - Did not fabricate `avengers-adjacent` as a faction; removed it from `factions` and preserved it in `normalizationNotes` as a relationship/adjacency tag.

- `cross-ange`
  - Normalized all target character location/faction references to canonical ids, including `misurugi-empire`, `arzenal`, `dragons-aura`, `anti-embryo-camp`, `diamond-rose-knights`, `embryo-camp`.
  - Added `old-human-tech` powerSystem for Tusk / 上古之民 references.

- `gundam-seed`
  - Normalized warship, country, alliance, ZAFT/PLANT, and battlefield references, including `archangel`, `plant`, `orb`, `space-battlefields`, `earth-alliance`, `zaft-plant`, `three-ships-alliance`, `archangel-crew`, `klein-faction`.
  - Normalized `coordinator-related` to `coordinator`.
  - Did not fabricate `command` or `politics` as power systems; removed them from `powerSystems` and preserved semantics in `normalizationNotes`.

- `toriko`
  - Normalized locations such as `human-world`, `gourmet-world`, `hotel-gourmet`, `cooking-festival-stage`, `gourmet-society-base`, `igo-headquarters`, `neo-base`.
  - Normalized factions such as `igo`, `gourmet-corps`, `neo`, `gourmet-knights-chef-network`, `four-heavenly-kings`, `independent-gourmet-ecosystem`, `toriko-camp`.
  - Mapped `料理竞赛场` to `gourmet-colosseum-market`.

## Validation

Local validation performed after edits:

1. JSON parse check for all target `world.json` and `characters-index.json` files.
2. Cross-reference scan for every character `locations`, `factions`, and `powerSystems` value against the corresponding `world.locations[].id`, `world.factions[].id`, and `world.powerSystems[].id`.

Validation result:

```text
honkai-impact-3rd {}
naruto {}
marvel-cinematic-universe {}
cross-ange {}
gundam-seed {}
toriko {}
json parse ok for target world/characters files
```

## Remaining issues / not handled here

- This pass only handled the delegated MED normalization for the six target worlds.
- Empty `source-registry.json:sources`, empty `conflictLog`, LOW/INFO relationship graph coverage, and KG coverage were not modified because they are outside this step's mutation scope.
- Some broad narrative/location ids (`historical-battlefields`, `cosmos`, `world-serpent-base`) remain intentionally coarse-grained and may be refined in later manual curation if stricter canon granularity is required.
