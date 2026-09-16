# Upstream-downstream partition of 1,083 snow-affected Northern Hemisphere basins

This repository publishes the basin partition behind the manuscript *Asymmetric snow variations from headwater to
downstream in Northern Hemisphere basins* (Nature Communications, NCOMMS-26-023352, in revision): the upstream and
downstream label of every HydroBASINS Level-08 sub-basin, the per-basin audit figures, and the tables that document how
each partition was built and checked.

## How the partition is built

Each of the 1,083 snow-affected Level-07 basins is split **within itself**, in two stages, from its Level-08 sub-basins
(HydroBASINS / BasinATLAS v10; 9,624 cells in total):

1. **Relief-adaptive pre-label.** The pre-label sets only the target upstream area fraction. Where the internal relief
   (area-weighted 90th minus 10th percentile of sub-basin elevation) is at least the threshold *T* = 600 m, cells at or
   above the area-weighted median elevation are pre-labelled upstream (161 basins). Otherwise the Pfafstetter digit
   order is used, digits 6-9 upstream and 1-4 downstream (906 basins); where the digits are one-sided, the distance to
   the terminal sink decides (16 basins).
2. **Connectivity-constrained cut.** The main stem is traced from the outlet along the tributary with the larger
   upstream area, and the partition is the single stem edge whose upstream share of basin area is closest to the target.
   The upstream unit is therefore one contiguous headwater subtree and the downstream unit always contains the outlet.

The analysis is repeated for relief thresholds of 300, 400, 500, 600, 700 and 800 m; 96.4 % of Level-08 cells keep the
same label across all six (87.1 % of basins are unchanged).

## Audit and exclusions (canonical run, T = 600 m)

| Outcome | Basins |
| --- | --- |
| Network-valid partition | 1,009 |
| More than one outlet | 62 |
| One-sided (all cells on one side) | 8 |
| Network-valid but visually inverted | 4 |

A partition is network-valid when the basin has one outlet, one acyclic Level-08 routing component, two non-empty and
internally connected labels, exactly one upstream-to-downstream cut edge and no downstream-to-upstream edge. All 1,083
basins were also inspected one by one against an ETOPO 2022 hillshade, which found the four inverted cases. The 74
excluded basins stay in every basin-averaged analysis and are dropped only from paired upstream-downstream statistics.

## Files

- `plots/` - one figure per basin, grouped by audit status (`valid_T600`, `invalid_multi_outlet`, `invalid_one_sided`).
  Figures are downscaled to 1600 px wide and saved as 64-colour indexed PNG; the originals are 2312 px wide.
  The four visually inverted basins are network-valid, so their figures sit in `valid_T600`;
  `index.html` points there for them (the working copy of the audit page linked to a folder that does not exist).
- `index.html` - offline browser for the figures: filter by status, relief class, threshold sensitivity, and step
  through the basins. Open it locally, or serve the repository with GitHub Pages.
- `data/Lev08_split.csv` - the label of every Level-08 cell (the partition itself).
- `data/basin_split_summary.csv` - one row per basin: axis used, upstream area fraction, cell counts.
- `data/basin_split_audit.csv` - the full audit table, all six thresholds plus the two alternative rules.
- `data/manual_review.csv` - the review sheet used for the visual audit.
- `data/invalid_basin_ids_T600.csv` - the excluded basins.
- `data/threshold_sensitivity.csv`, `data/threshold_sensitivity_by_relief.csv`, `data/threshold_sensitivity.md` -
  relabelling statistics across thresholds.
- `data/verification.md` - the bit-exact reproduction check against the submitted version.

## Figure legend

- Blue and orange polygons: the final upstream and downstream labels.
- Grey arrows: the within-basin `NEXT_DOWN` routing between Level-08 cells.
- Red arrow: the upstream-to-downstream cut edge.
- Filled purple star: the primary outlet; open purple triangle: any further outlet.
- Purple outline: a cell whose label changes between thresholds.
- Small panels: the same basin at the other relief thresholds. Bottom table: the Level-08 cells with area, elevation,
  distance to sink and their label under each threshold.
- Basin geometry is drawn in a local projected coordinate system; arrows show routing topology, not river centre-lines.

## Source data and licence

Derived from HydroBASINS and BasinATLAS v10 (HydroSHEDS, www.hydrosheds.org) and ERA5-Land (Copernicus Climate Change
Service). The labels, tables and figures in this repository are released under CC BY 4.0; please respect the licences of
the upstream data sets when you redistribute them. Cite the manuscript above, and HydroSHEDS for the underlying basins.
