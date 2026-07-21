# Coordinate generalisation in `fold_assignments.tsv`

## What changed

The `x` and `y` columns in `data/derived/primary/tables/fold_assignments.tsv`
and `data/derived/sensitivity/tables/fold_assignments.tsv` are generalised to
the **1 km OS National Grid square** (south-west corner of the square).

Earlier releases of this package carried these coordinates at their source
precision, which for some records was finer than 1 km. That was inadvertent.
Publishing precise locations of archaeological findspots, in particular
unexcavated burials, is contrary to the data-provider terms under which the
underlying records were obtained and to standard heritage practice, because
precise locations expose sites to unauthorised metal detecting.

The affected values have been rewritten throughout this repository's git
history, including all release tags, not merely superseded by a later commit.
Commit hashes therefore differ from those in any clone taken before
21 July 2026.

## Why the columns were generalised rather than removed

The `x`/`y` columns exist so that the spatial blocking of the cross-validation
folds can be independently verified. Spatial block assignment in this analysis
operates at scales far coarser than 1 km, so 1 km generalisation preserves that
check in full. Removing the columns entirely would have reduced what a reviewer
can verify, for no additional protection.

`site_id` and `fold` are unchanged. Every reported metric in the manuscript is
unaffected: no published statistic is computed from these two columns.

## Reproducibility impact

None for any packaged result. `scripts/repro_check_report.py` reproduces the
manuscript headline metrics from the derived tables, and does not read `x`/`y`.
Analysts performing a full rerun from licensed source data will use the source
coordinates directly, as documented in the README.
