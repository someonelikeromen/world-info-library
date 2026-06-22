# REPAIR-Q5-RELATIONSHIP-LOW

## Scope

- Step id: `q5-relationship-low`
- Worlds reviewed: `rozen-maiden`, `sekirei`, `dungeon-fighter-online`, `tokyo-ghoul`, `marvel-cinematic-universe`, `gate-jsdf`, `honkai-impact-3rd`, `date-a-live`, `type-moon-nasuverse`, `danmachi`
- Files changed are limited to the delegated curated character indexes, relationship graphs, and this report.

## Actions Taken

- Converted string relationship targets in the scoped `characters-index.json` files into structured relationship objects with `target`, `targetType`, `relation`, and `resolutionStatus` where the target could be resolved.
- Preserved multi-target relationship labels as `targets` arrays when a single target would be misleading, e.g. `matsu/kazehana` in `sekirei`.
- Marked organization, collective, location, and concept relationship targets as non-character targets using `group`, `location`, or `concept` rather than pretending they are characters.
- Added minimal relationship graph nodes for confirmed missing important character targets and non-character targets used by structured relationships.
- Left only unverifiable conceptual relationship labels as `resolutionStatus: unresolved` rather than inventing a target.

## Per-World Results

| World | Structured relationship targets | Remaining unresolved | Notes |
| --- | ---: | ---: | --- |
| `rozen-maiden` | 26 | 0 | Added minimal nodes for missing mediums/related creators and doll collective targets. |
| `sekirei` | 22 | 0 | Resolved indexed targets, added `takami`, `shiina`, and `disciplinary-squad`; kept `matsu/kazehana` as multi-target. |
| `dungeon-fighter-online` | 9 | 0 | Added `michael`, `adventurers`, `heaven`, and `ghostblade-line` as character/group/location/concept nodes. |
| `tokyo-ghoul` | 13 | 0 | Added nodes for `ayato-kirishima`, `eto-yoshimura`, `kureo-mado`, and `v-organization`. |
| `marvel-cinematic-universe` | 17 | 0 | Existing graph already covered structured targets after conversion. |
| `gate-jsdf` | 22 | 0 | Added confirmed character nodes such as `kato-el-altestan`, `molt-sol-augustus`, `delilah`, plus `hodoryu` location and indexed `giselle`. |
| `honkai-impact-3rd` | 17 | 0 | Added confirmed relationship targets including `seele-vollerei`, `kallen-kaslana`, and `mei-dr`. |
| `date-a-live` | 70 | 4 | Normalized organization targets to `group`; retained four conceptual labels as unresolved because no unique character/group/location/concept target is safe. |
| `type-moon-nasuverse` | 19 | 0 | Resolved alias target `saber` to canonical `saber-artoria`; graph coverage already includes related nodes. |
| `danmachi` | 14 | 0 | Added confirmed nodes for `loki`, `hephaestus`, `syr-flova`, and `ottar`. |

## Remaining Unresolved

Only `date-a-live` retains unresolved relationship entries. They are broad/conceptual labels rather than unique relationship targets:

- `ch-honjo-nia`: no unique target for the label about distrust of three-dimensional humans.
- `ch-hoshimiya-mukuro`: no unique target for the label about exclusivity/possessiveness in close relationships.
- `ch-yamai-kaguya`: no unique target for the label about competitive sisterly pride.
- `ch-takamiya-shinji`: no unique target for the label about obsession with a team/group concept.

These were intentionally kept unresolved to avoid fabricating characters or over-specific links.

## Validation

A scoped JSON/reference validation script was run after edits across the ten worlds. Results:

- All edited JSON files parse successfully.
- No remaining string-form relationships were found in the scoped worlds.
- No structured relationship target points to a missing relationship graph node.
- All structured `targetType` values are within `character`, `group`, `location`, or `concept`.
- Remaining unresolved count in the scoped worlds is 4, all in `date-a-live` and documented above.
