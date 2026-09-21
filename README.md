# Upstream-downstream partition of 1,083 snow-affected Northern Hemisphere basins

The basin partition of "Asymmetric snow variations from headwater to downstream in Northern Hemisphere basins"
(Nature Communications, NCOMMS-26-023352): the upstream or downstream label of every HydroBASINS Level-08 sub-basin,
the audit of every partition, and one map per basin. The algorithm is described in the Methods and in Supplementary
Text S2 of the paper.

## Run

Open `code/split_basins.ipynb` and run all cells (numpy and pandas, a few seconds). It reads `data/Lev08_cells.csv`,
writes its tables to `split_output/` and checks them against the published tables in `data/`.

Open `index.html` to browse the maps by audit status, relief class and basin.

## Contents

- `data/Lev08_cells.csv` - input: the 9,624 Level-08 sub-basins of the 1,083 basins with their HydroBASINS / BasinATLAS
  v10 attributes. The row order is part of the input.
- `data/Lev08_split.csv` - the partition: the label of every Level-08 sub-basin.
- `data/Lev08_split_thresholds.csv` - the labels under the six relief thresholds (`s_T300` to `s_T800`; `s_T600` is the
  partition) and under the two alternative rules (`s_ELEVDEF`, `s_AREA50`).
- `data/basin_split_summary.csv` - one row per basin: rule used, upstream area fraction, relief class.
- `data/basin_split_audit.csv` - the audit of every basin under all thresholds and rules. Of the 1,083 basins, 1,009
  have a valid partition (`valid_T600`); 62 have more than one outlet, 8 are one-sided and 4 are visually inverted.
- `data/catchments_4767.csv` - the 4,767 minimally disturbed gauged catchments the basins were selected from.
  `record_source` names the source list whose record was kept, and `in_both_compilations` flags the 621 catchments
  listed in both, so some attributes are empty for the records of one list.
- `plots/` - one map per basin, grouped by audit status: the partition under the six thresholds over an ETOPO 2022
  hillshade with the HydroRIVERS network (blue upstream, red downstream, black outline for the outlet sub-basin; a
  black dot marks a label that differs from the 600 m partition).
- `Workflow.tiff` - the workflow of the partition (Supplementary Fig. S6 of the paper).

The notebooks that redraw Figs. 1-4 and the Source Data are in https://github.com/SrayPen/snowmismatch_reproduction.

## License

CC BY 4.0 (`LICENSE`). Derived from HydroBASINS, BasinATLAS v10 and HydroRIVERS (HydroSHEDS), ETOPO 2022 (NOAA NCEI)
and ERA5-Land (Copernicus Climate Change Service), which keep their own licenses.
