# REPAIR-MED-NORMALIZATION-A

Date: 2026-06-22

## Scope

Processed MED normalization for high-load world group A:

- `worlds/madan-no-ou/curated/`
- `worlds/dantalian-no-shoka/curated/`
- `worlds/gate-jsdf/curated/`
- `worlds/d-gray-man/curated/`
- `worlds/dragon-ball/curated/`

Allowed files modified:

- `world.json`
- `characters-index.json`
- `curation-notes.md`
- this report

Focus categories: character-location, character-faction, character-powerSystem, world-faction-member/index consistency.

## Normalization policy

- Obvious display-name references were changed to canonical ids from each world's `world.json` registries.
- Original display labels were preserved under character `metadata.originalReferenceLabels`.
- Character-level `normalizationNotes` were added where normalization was performed or where a reference was intentionally left unresolved.
- When the role of a missing registry entry was clear and non-controversial, a minimal `normalization-stub` node was added to `world.json` with a note that it needs later enrichment.
- Ambiguous cases were not forced into fake canon ids.

## Per-world changes

### `madan-no-ou`

Files:

- `worlds/madan-no-ou/curated/world.json`
- `worlds/madan-no-ou/curated/characters-index.json`
- `worlds/madan-no-ou/curated/curation-notes.md`

Actions:

- Added safe registry nodes for recurring character references missing from `world.json`, including duchy seats/regions such as `sheresuta`, `leitmeritz-seat`, `olmutz-seat`, `polesia-seat`, `legnica-seat`, `lebus-seat`, `osterode-seat`, `brest-seat`, `ode`, `reims`, `nemetacum`, `muozinel-region`, `asvarre-region`, `sachstein-region`.
- Added faction/affiliation nodes such as `silver-meteor-army`, `lourie-family`, `alshavin-family`, `brune-royal-house`, `zhcted-royal-house`, `vorn-family`, `lutetia`, `nemetacum-duchy`, `demons`, `ancient-divine`, and `alsace-domain`.
- Added ability/power normalization nodes for recurring non-registry labels: `archery-martial-arts`, `dragon-gear-resonance`, `demon-abilities`, `demon-related-late`, `dragon-gear-related`.
- Converted character display-name references to canonical ids where safe.
- Rebuilt `characters-index.json.indices` from normalized character records.

Intentional unresolved references:

- `roland.powerSystems`: `杜兰达尔` remains unresolved because repository evidence identifies it as an artifact/item (`knowledge-graph.json` has `durandal` type `artifact`), not a `powerSystem`; it is already present in Roland's `items`.
- `eugene.factions`: `王室` remains unresolved because the source summary says the exact royal house needs later verification; mapping it to either Brune or Zhcted would be fabricated.

### `dantalian-no-shoka`

Files:

- `worlds/dantalian-no-shoka/curated/world.json`
- `worlds/dantalian-no-shoka/curated/curation-notes.md`

Actions:

- Character location fields were already id-like.
- Added missing location registry nodes referenced by characters, including `battlefront-airbase`, `glanholm-station`, `gourmet-banquet`, `doll-warehouse-city`, `calabos-estate`, `lentz-villa`, `hildenbrand-house`, `sustin-concert-hall`, `fiona-lab`, `ghost-train`, `red-brick-mansion`, `olrick-mansion`, `wesley-old-house`, `roscetti-shop`, and `asquith-mansion`.
- Did not expand unverified canon beyond minimal event-location stubs.

Result: no remaining character-location/faction/powerSystem references outside `world.json` registries.

### `gate-jsdf`

Files:

- `worlds/gate-jsdf/curated/world.json`
- `worlds/gate-jsdf/curated/characters-index.json`
- `worlds/gate-jsdf/curated/curation-notes.md`

Actions:

- Converted string-only `world.json.factions` and `world.json.locations` into `{id, name}` registry objects.
- Added needed safe registry entries: `special-region`, `apostles`, `kato-students`.
- Added non-supernatural power normalization nodes `political-authority` and `martial-training` for original `political`/`martial` character labels.
- Normalized character `locations`, `factions`, and `powerSystems` to ids.
- Rebuilt `characters-index.json.indices`.

Result: no remaining character-location/faction/powerSystem references outside `world.json` registries.

### `d-gray-man`

Files:

- `worlds/d-gray-man/curated/world.json`
- `worlds/d-gray-man/curated/characters-index.json`
- `worlds/d-gray-man/curated/curation-notes.md`

Actions:

- Converted string-only `world.json.factions` and `world.json.locations` into `{id, name}` registry objects.
- Added needed safe registry entries: `bookman-lineage`, `secret-lines`, plus role/location scope nodes such as `europe`, `battlefields`, `order-periphery`, `villages-and-towns`, `earl-battlefields`, `illusion-space`, `order-secret-facilities`, and `past-ark`.
- Normalized character `locations` and `factions` to ids.
- Rebuilt `characters-index.json.indices`.

Result: no remaining character-location/faction/powerSystem references outside `world.json` registries.

### `dragon-ball`

Files:

- `worlds/dragon-ball/curated/world.json`
- `worlds/dragon-ball/curated/characters-index.json`
- `worlds/dragon-ball/curated/curation-notes.md`

Actions:

- Converted string-only `world.json.factions` and `world.json.locations` into `{id, name}` registry objects.
- Added needed safe registry entries: `capsule-corporation`, `satan-friendly-buu-branch`, `west-city`, `universe`, `kami-lookout`, `king-kai-planet`, `kaioshin-realm`.
- Added power normalization nodes for original id-like labels: `namekian-biology`, `capsule-technology`, `alien-biology`, `magic`.
- Normalized character `locations`, `factions`, and `powerSystems` to ids.
- Rebuilt `characters-index.json.indices`.

Result: no remaining character-location/faction/powerSystem references outside `world.json` registries.

## Validation

Validation performed with a local Node.js script over the 5 target worlds:

- Parsed each target `world.json` and `characters-index.json` successfully.
- Built registries from `world.locations[].id`, `world.factions[].id`, and `world.powerSystems[].id`.
- Checked every character `locations`, `factions`, and `powerSystems` entry against those registries.
- Checked rebuilt `indices.byFaction` and `indices.byPowerSystem` for stale keys.

Observed validation summary:

```text
madan-no-ou        unresolved refs: 2; stale index groups: 2 (same unresolved labels)
dantalian-no-shoka unresolved refs: 0; stale index groups: 0
gate-jsdf          unresolved refs: 0; stale index groups: 0
d-gray-man         unresolved refs: 0; stale index groups: 0
dragon-ball        unresolved refs: 0; stale index groups: 0
```

Remaining unresolved details:

```json
[
  {"world":"madan-no-ou","character":"roland","category":"powerSystems","value":"杜兰达尔","reason":"artifact/item, not safe to map as powerSystem"},
  {"world":"madan-no-ou","character":"eugene","category":"factions","value":"王室","reason":"exact royal house not safely established"}
]
```

## Remaining risks / not handled here

- This step did not claim to clear empty `source-registry.json:sources`, empty `conflictLog`, LOW/INFO graph quality, or global KG coverage; those are outside this MED normalization subtask.
- Some newly added `normalization-stub` nodes are intentionally minimal and should be enriched later from source volumes if deeper canon precision is required.
- `madan-no-ou` still has two intentional MED residuals because forcing them would create false canon.
