# Stage 02 verification

- basins in split: 1083; analysis basins missing: 0
- one-sided (degenerate-split) basins: 8 [2837040, 7122470, 7138300, 7254710, 7255602, 7429898, 7822006, 7834070] — flagged `split_degenerate`, excluded from paired analyses (they classify as Indeterminate anyway)
- max |f_up_area(audit) - recomputed|: 0.000500
- median upstream area fraction: 0.517
- relief classes: {'low': 690, 'mixed': 232, 'high': 161}
- elevation-axis basins: 161; rule violations: 0 (high but not elevation), 0 (elevation but not high)
- threshold-sensitivity outputs present: True
  - A vs B (default): 1.3% cells relabelled; C vs B (default): 0.8% cells relabelled; any of A,C vs B: 2.1% cells relabelled

## Result: PASS

canonical cells written: 9624 (1083 basins)