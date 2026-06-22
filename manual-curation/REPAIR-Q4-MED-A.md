# REPAIR-Q4-MED-A

Date: 2026-06-22

## Scope

Processed MED normalization for the first high-priority world group in `manual-curation/QA-AFTER-REPAIR-R3.md`:

- `worlds/kekkaishi/curated/`
- `worlds/ikki-tousen/curated/`
- `worlds/type-moon-nasuverse/curated/`
- `worlds/negima-uq-holder/curated/`
- `worlds/danmachi/curated/`
- `worlds/kenichi/curated/`

Allowed files modified:

- `world.json`
- `characters-index.json`
- `curation-notes.md`
- this report

Focus categories:

- character-location
- character-faction
- world-faction-member
- character-powerSystem

## Normalization policy

- Obvious display-name references were changed to canonical ids from each world's registry.
- Original display labels were preserved under character `metadata.originalReferenceLabels` and `normalizationNotes`.
- Ambiguous values were not forced into fake canon ids; any unresolved cases were left unchanged only if they could not be safely mapped.
- For world registries that were still string-only, entries were converted into `{ id, name }` registry objects so character references could resolve against canonical ids.

## Per-world changes

### `kekkaishi`

Files:

- `worlds/kekkaishi/curated/world.json`
- `worlds/kekkaishi/curated/characters-index.json`
- `worlds/kekkaishi/curated/curation-notes.md`

Actions:

- Converted string-only `world.json.factions` and `world.json.locations` into `{id, name}` registry objects.
- Normalized character factions and locations to canonical ids such as `sumimura-family`, `yukimura-family`, `yakou`, `rikai`, `kokuboro`, `karasumori-school`, `karasumori-land`, `yakou-base`, and `spirit-land`.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

### `ikki-tousen`

Files:

- `worlds/ikki-tousen/curated/world.json`
- `worlds/ikki-tousen/curated/characters-index.json`
- `worlds/ikki-tousen/curated/curation-notes.md`

Actions:

- Converted string-only `world.json.factions` and `world.json.locations` into `{id, name}` registry objects.
- Normalized character factions and locations to canonical ids such as `nanyo-academy`, `seito-academy`, `xuchang-academy`, `luoyang-high`, `kansai-faction`, `yamato-himiko-line`, `kanto-high-schools`, `kyoto-kansai`, and `toushi-tournament-venue`.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

### `type-moon-nasuverse`

Files:

- `worlds/type-moon-nasuverse/curated/world.json`
- `worlds/type-moon-nasuverse/curated/characters-index.json`
- `worlds/type-moon-nasuverse/curated/curation-notes.md`

Actions:

- Converted world factions and locations into `{id, name}` registry objects.
- Added `church-technique` to `world.powerSystems` so `kirei-kotomine` could resolve its power-system label canonically.
- Normalized character faction/location fields to canonical ids such as `fuyuki-masters`, `fuyuki-servants`, `tohsaka-family`, `matou-family`, `einzbern-family`, `holy-church`, `fuyuki-city`, `clock-tower`, `chaldea-base`, `einzbern-castle`, `singularity`, and `fuyuki-church`.
- Added `waver-velvet` and `romani-archaman` to align `world.factions[].knownMembers` with actual character-index ids.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

### `negima-uq-holder`

Files:

- `worlds/negima-uq-holder/curated/world.json`
- `worlds/negima-uq-holder/curated/characters-index.json`
- `worlds/negima-uq-holder/curated/curation-notes.md`

Actions:

- Converted world factions and locations into `{id, name}` registry objects.
- Added `anti-magic` to `world.powerSystems` to resolve the character-level `anti-magic` label.
- Normalized character faction/location fields to canonical ids such as `mahora-gakuen-city`, `magic-association-world`, `white-wing`, `uq-holder`, `kyoto-magic-side`, `kyoto-magic-base`, `magic-world-mars`, `orbital-elevator-future-city`, and `uq-holder-haven`.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

### `danmachi`

Files:

- `worlds/danmachi/curated/world.json`
- `worlds/danmachi/curated/characters-index.json`
- `worlds/danmachi/curated/curation-notes.md`

Actions:

- Converted world factions and locations into `{id, name}` registry objects.
- Normalized character factions and locations to canonical ids such as `hestia-familia`, `loki-familia`, `freya-familia`, `benevolent-mistress-inn`, `orario`, `babel-tower`, `dungeon`, and `hearth-stone`.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

### `kenichi`

Files:

- `worlds/kenichi/curated/world.json`
- `worlds/kenichi/curated/characters-index.json`
- `worlds/kenichi/curated/curation-notes.md`

Actions:

- Converted world factions and locations into `{id, name}` registry objects.
- Added `strategy` to `world.powerSystems` so the existing `nijima-haruo` power label could resolve canonically.
- Normalized character factions and locations to canonical ids such as `ryozanpaku`, `shin-white-union`, `dark`, `ikkyo-kyuken`, `huangliang-high-school`, and `ryozanpaku-dojo`.
- Preserved original labels in `metadata.originalReferenceLabels` and `normalizationNotes`.

## Validation

Validation performed with a local Node.js script over all 6 target worlds:

- Parsed each target `world.json` and `characters-index.json` successfully.
- Rebuilt registry lookups from `world.factions[].id`, `world.locations[].id`, and `world.powerSystems[].id`.
- Checked every character `factions`, `locations`, and `powerSystems` entry against those registries.
- Verified each `world.factions[].knownMembers` value resolves to an existing `characters-index.json` id.
- Confirmed each target `curation-notes.md` contains a single `2026-06-22 MED 规范化补记` block.

Observed validation summary:

```text
kekkaishi             unresolved refs: 0; unknown knownMembers: 0
ikki-tousen           unresolved refs: 0; unknown knownMembers: 0
type-moon-nasuverse   unresolved refs: 0; unknown knownMembers: 0
negima-uq-holder      unresolved refs: 0; unknown knownMembers: 0
danmachi              unresolved refs: 0; unknown knownMembers: 0
kenichi               unresolved refs: 0; unknown knownMembers: 0
```

## Remaining risks

- I did not force any ambiguous label into a fabricated canon id; unresolved items were left alone only if they could not be safely mapped.
- This repair step targets MED normalization only; it does not claim to clear remaining LOW/INFO quality signals outside the requested scope.
