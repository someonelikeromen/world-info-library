# QA-CROSS-REFERENCES-AFTER-REPAIR

Date: 2026-06-22  
Scope: `worlds/*/curated/` cross-file reference consistency after the repair pass.  
Mutation note: no `worlds/*/curated` files were modified in this step; this report is the only file written.

## Method

Re-ran a read-only cross-reference sweep over all `worlds/*/curated` folders, checking:

- `relationship-graph.edges[].from/to` against `relationship-graph.nodes[].id`
- `knowledge-graph.edges[].from/to` against `knowledge-graph.nodes[].id`
- `characters-index.characters[].sourceRefs`, `sourceId`, `sourceTrace`, and graph/source reference fields against `source-registry.sources[].sourceId`
- character `factions`, `locations`, `powerSystems` against world-level ids
- character `relationships[]` targets against character and relationship-graph ids
- world faction member references against `characters-index.characters[].id`
- a light heuristic for obvious KG coverage gaps
- a quick sanity check that the special-world gate fields added in the prior repair still exist for `acg-character-database`, `blue-archive`, and `monster-hunter`

## Comparison with the pre-repair report

Baseline from `manual-curation/QA-CROSS-REFERENCES.md`:

- Worlds scanned: 63
- Findings: 1406
- Severity: HIGH 379 / MED 707 / LOW 238 / INFO 82

After repair rerun:

- Worlds scanned: 63
- Findings: 876
- Severity: **HIGH 0 / MED 438 / LOW 295 / INFO 143**

### Main conclusion

- **HIGH is now zero in this rerun.**
- The previously reported broken graph/source-reference issues are no longer showing as HIGH.
- Remaining findings are mostly normalization / coverage / heuristic quality issues rather than hard broken endpoints.

## Residual findings by category

| Category | Count | Severity | Notes |
|---|---:|---|---|
| `character-relationship-target` | 231 | LOW | Relationship labels still point to groups, placeholders, or non-indexed targets in some worlds. |
| `character-location` | 217 | MED | Character location values often do not match world ids exactly; many look like display labels. |
| `character-faction` | 150 | MED | Same slug-vs-display-name mismatch pattern as locations. |
| `world-kg-coverage` | 143 | INFO | Heuristic signal only; indicates missing obvious KG node coverage for some world entities. |
| `relationship-coverage` | 64 | LOW | High/core characters still absent from relationship graphs in some worlds. |
| `character-powerSystem` | 43 | MED | Power-system ids are inconsistently normalized. |
| `world-faction-member` | 28 | MED | Some faction `knownMembers` entries do not resolve to indexed characters. |

## Worlds with the largest residual load

| World | Findings | MED | LOW | INFO |
|---|---:|---:|---:|---:|
| `madan-no-ou` | 178 | 101 | 69 | 8 |
| `date-a-live` | 78 | 0 | 63 | 15 |
| `dantalian-no-shoka` | 38 | 24 | 2 | 12 |
| `naruto` | 34 | 20 | 11 | 3 |
| `gate-jsdf` | 33 | 22 | 9 | 2 |
| `honkai-impact-3rd` | 33 | 21 | 8 | 4 |
| `marvel-cinematic-universe` | 32 | 17 | 12 | 3 |
| `d-gray-man` | 31 | 21 | 9 | 1 |
| `dragon-ball` | 29 | 21 | 6 | 2 |
| `type-moon-nasuverse` | 29 | 13 | 12 | 4 |
| `cross-ange` | 20 | 16 | 2 | 2 |
| `negima-uq-holder` | 20 | 14 | 5 | 1 |
| `kimetsu-no-yaiba` | 19 | 9 | 7 | 3 |
| `sekirei` | 19 | 2 | 11 | 6 |
| `danmachi` | 18 | 8 | 7 | 3 |
| `tokyo-ghoul` | 16 | 5 | 9 | 2 |
| `gundam-seed` | 15 | 15 | 0 | 0 |
| `toriko` | 14 | 13 | 0 | 1 |

## Still needs human review

1. **Id normalization policy**
   - The largest remaining class is `character-location` / `character-faction`.
   - Many entries appear to use localized labels rather than strict world ids.
   - Decide whether these fields are runtime foreign keys or display labels.

2. **Relationship placeholder policy**
   - `character-relationship-target` is still common.
   - Some targets may be intentional group labels or secondary names, but they are not consistently resolvable.

3. **Relationship graph completeness**
   - `relationship-coverage` still flags worlds where important characters are not represented in the relationship graph.
   - This is a retrieval-quality issue, not a broken-reference issue.

4. **KG coverage heuristic**
   - `world-kg-coverage` remains informational only.
   - It should be treated as a prompt for manual enrichment, not as a hard failure.

## Validation status

- JSON parse check over `worlds/*/curated/*.json`: **315 files, 0 parse errors**
- Special-world gate presence check:
  - `acg-character-database`: `runtimeUseGate`, `specialWorldGate`, `referenceLibraryType` present where expected
  - `blue-archive`: `runtimeUseGate`, `notCompleteCanonRoster` present where expected
  - `monster-hunter`: `runtimeUseGate`, `notCompleteCanonRoster` present where expected
- No HIGH cross-reference findings remained in the rerun.

## Final assessment

- **P0/P1-style graph/source breakage is effectively cleared in this pass.**
- Remaining issues are mostly MED/LOW/INFO and should be treated as follow-up normalization and coverage work.
- Largest manual follow-up candidate is `madan-no-ou`, followed by `date-a-live` and the other medium-load worlds listed above.
