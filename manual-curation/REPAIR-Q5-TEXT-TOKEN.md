# REPAIR-Q5-TEXT-TOKEN

## Scope

- Step id: `q5-text-token`
- Worlds reviewed: `date-a-live`, `madan-no-ou`
- Goal: review Q4 residual generic placeholder-token hits, avoid false positives, and convert real placeholder risks to `unresolved-reference` markers without changing canon content.

## Search Pattern

Reviewed curated files with a placeholder-token sweep for:

`placeholder|占位|todo|tbd|unknown|missing|dummy|sample|example|lorem|fixme|xxx|待定|暂缺|未定|模板|泛化`

## Changes

### `worlds/date-a-live/curated/relationship-graph.json`

- Converted two `resolutionStatus: "aggregate-placeholder"` values for Date A Bullet / 临界 aggregate minor-character group nodes to `resolutionStatus: "unresolved-reference"`.
- Expanded notes to clarify that the risk is unresolved individual-character resolution from an aggregate `characters-index` entry, not a canon change.

### `worlds/date-a-live/curated/knowledge-graph.json`

- Converted two `resolutionStatus: "aggregate-placeholder"` values for the same aggregate minor-character coverage nodes to `resolutionStatus: "unresolved-reference"`.
- Added/expanded notes stating that the aggregate entry remains unresolved at individual-character level.

### `worlds/madan-no-ou/curated/knowledge-graph.json`

- Reworded the explanatory note `不覆盖原 graphs/placeholder` to `不覆盖原始导入图谱草稿目录`.
- This was an explanatory QA note, not a canon placeholder, so no unresolved-reference marker was added.

## Non-risk Residual Matches

- `worlds/date-a-live/curated/README.md` still contains `状态栏模板`, but this file is outside the allowed mutation scope for this step and the phrase is explanatory source-quality context rather than a live placeholder.
- `worlds/madan-no-ou/curated/source-registry.json` contains the schema/property name `evidenceExamples`; this is structural metadata and not placeholder content.

## Validation

- Re-ran targeted placeholder-token sweeps over `worlds/date-a-live/curated` and `worlds/madan-no-ou/curated`.
- Confirmed in-scope placeholder-status hits were removed or converted to `unresolved-reference`.
- Parsed edited JSON files successfully with Node:
  - `worlds/date-a-live/curated/relationship-graph.json`
  - `worlds/date-a-live/curated/knowledge-graph.json`
  - `worlds/madan-no-ou/curated/knowledge-graph.json`

## Risk Notes

- Canon summaries, labels, node identities, and graph relationships were not changed.
- The remaining `unresolved-reference` markers are intentional risk markers for aggregate character entries that are not resolved to named individual characters.
