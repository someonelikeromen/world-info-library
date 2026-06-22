# REPAIR-SOURCE-REFS

Date: 2026-06-22  
Scope: `worlds/{madan-no-ou,toaru,testament-sister-new-devil,claymore}/curated/source-registry.json` and `characters-index.json` only.

## Goal

Repair HIGH `source-ref` QA issues without inventing new canon sources.

Strategy used:

- Prefer registering fragment/comment/entryIndex sourceRefs as traceable aliases of an existing parent source.
- Do not rewrite character content or fabricate new source facts.
- Add notes / registryNotes so the merge decision is explicit.

## Worlds repaired

### `madan-no-ou`

Observed issue:

- `characters-index.json` used fragment refs like `src-madan-no-ou-001#entry-0`, `#entry-15`, `#entry-44..` that were not registered in `source-registry.json`.

Repair applied:

- Kept the canonical parent source `src-madan-no-ou-001`.
- Registered the fragment ids as derived aliases in `source-registry.json`.
- Marked them as fragment-level provenance only.

Notes:

- `#entry-*` ids are treated as entry slices of the same worldbook, not separate canon sources.
- No new world facts were introduced.

### `toaru`

Observed issue:

- `characters-index.json` used `characters.json comment ...` refs that were not registered.

Repair applied:

- Registered the imported root source `src-toaru-001` in curated registry.
- Added one alias entry per comment-based sourceRef.
- Each alias points back to `src-toaru-001` with a comment selector.

Notes:

- These aliases preserve traceability from character rows to the original imported character-sheet comments.
- No new canon claims were added.

### `testament-sister-new-devil`

Observed issue:

- `characters-index.json` used `characters.json comment ...` refs that were not registered.

Repair applied:

- Registered the imported root source `src-testament-sister-new-devil-001` in curated registry.
- Added alias entries for each comment-based sourceRef.
- Recorded the merge decision in `registryNotes`.

Notes:

- `拉姆萨斯/威尔贝特` was kept as a merged alias mapping to the same parent source trail.

### `claymore`

Observed issue:

- `characters-index.json` used `characters.json entryIndex 0/4/8` refs that were not registered.

Repair applied:

- Registered the imported root source `src-claymore-001` in curated registry.
- Added alias entries for the entryIndex refs.
- Recorded that these are entry-slice aliases only.

Notes:

- This world uses a very small set of entry indices; all are now traceable to the imported parent source.

## Validation

Performed a mechanical consistency check after editing:

- JSON parse check: passed for the four edited worlds.
- `characters-index.sourceRefs` coverage against `source-registry.sources[].sourceId`: no missing refs in the four edited worlds.
- Registry now contains parent source plus derived alias entries for all known HIGH source-ref patterns in scope.

Validation summary:

- `madan-no-ou`: missing refs = 0
- `toaru`: missing refs = 0
- `testament-sister-new-devil`: missing refs = 0
- `claymore`: missing refs = 0

## Residual risk

- The alias entries are provenance shims, not newly verified source records.
- Some comments / entry slices may still need human curation if later workflows require richer metadata than `parentSourceId` + selector.
- I did not modify other curated files, so unrelated HIGH issues from graph nodes remain for later passes.
