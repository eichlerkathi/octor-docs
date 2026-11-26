# Working with the seed table

Annotations of octo neurons live in a SeaTable table, one row per
**seed**: a point inside a neuron, placed in Spelunker. Root IDs change
whenever a neuron is proofread, but a point inside the neuron stays
valid. So the table stores the position, and octor looks up the current
IDs from it.

## Setting up the table

Create these columns (names can be changed with the `cols` argument of
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)):

| Column | Type | Content |
|----|----|----|
| `position` | Text | Spelunker voxel coordinates, e.g. `11434, 13413, 2501` |
| `supervoxel_id` | Text | Filled by octor |
| `root_id` | Text | Filled by octor: the current neuron ID |
| `root_id_previous` | Text | Previous root ID, when it changed |
| `root_changed_on` | Date | When the root ID last changed |
| `ids_checked_on` | Date | Last update |
| `n_seeds` | Number | How many rows share this root ID |
| `dup_status` | Text | `unique`, `primary`, `secondary`, `CONFLICT ...`, `no segment` |
| `primary` | Checkbox | The row you trust and fill in |
| `same_as` | Text | For secondary rows: position of the primary row |
| `last_edited` | Date (with time) | Optional: when the neuron was last proofread |

[`octo_doctor()`](https://eichlerkathi.github.io/octor-docs/reference/octo_doctor.md)
checks that these columns exist and have the right types.

Keep all ID columns as **Text**. IDs are 64-bit integers, and Number
columns silently change their last digits.

Positions can be pasted straight from Neuroglancer: `1234, 5678, 910`,
`[1234 5678 910]` and tab-separated values all work.

## Updating IDs

``` r
library(octor)
octo_update_ids(dry_run = TRUE)   # see what would change
octo_update_ids()                 # write to SeaTable
```

The first run looks up a supervoxel for every seed. Seeds are looked up
in batches, with each segmentation chunk downloaded once for all seeds
in it, so thousands of seeds take minutes rather than hours. Later runs
only look up new seeds and refresh root IDs, which takes seconds.
Running it daily (cron job or scheduled task) keeps the table current.

## Neurons edited after annotation

With the optional `last_edited` column,
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
records when each neuron was last proofread. A SeaTable filter like
*`last_edited` is after `annotated_on`* (or after the row’s modification
date) lists neurons whose shape changed since someone annotated them,
and which should be checked again.

Outside the table,
[`octo_last_modified()`](https://eichlerkathi.github.io/octor-docs/reference/octo_last_modified.md)
gives the same for any root IDs, and
[`octo_edit_history()`](https://eichlerkathi.github.io/octor-docs/reference/octo_edit_history.md)
lists the individual merges and splits.

## Neurons seeded more than once

When several rows point to the same root ID, they are the same neuron.
In each group, one row is the **primary** row, the one you annotate; the
others are **secondary**:

- tick `primary` on the row you want to keep
- if no row is ticked, octor picks the row with the most annotation
  filled in (`cell_type`, `group`, `soma_side`, `reconstructor`,
  `annotator`, `seymour_match_id`), or the oldest row if they are equal
- `CONFLICT` means several rows are ticked. This usually happens when
  proofreading merged two neurons that were both annotated: merge the
  information into one row and untick the other
- if a merged neuron is split again, its rows become `unique` again

Useful SeaTable views:

- **Duplicates:** filter `n_seeds > 1`, group by `root_id`
- **To annotate:** filter `dup_status` is not `secondary`: one row per
  neuron

## Finding neurons

``` r
ids <- octo_find_ids("^MBON")                     # regex on cell_type
ids <- octo_find_ids("KC", exact = TRUE)          # exactly "KC"
ids <- octo_find_ids("^L$", column = "soma_side")
seeds <- octo_seeds(trusted_only = TRUE)          # whole table, one row per neuron
```

## Viewing in Spelunker

``` r
octo_scene(octo_find_ids("^MBON"), color_by = "cell_type", seeds = TRUE, open = TRUE)
```

This creates a short Spelunker link with the neurons selected, coloured
by cell type, and their seed points as annotations, so you can share a
set of neurons with one link.

## IDs from elsewhere

For root IDs that are not in the seed table (lists from colleagues, old
analyses),
[`octo_latestid()`](https://eichlerkathi.github.io/octor-docs/reference/octo_latestid.md)
finds the current IDs. When a neuron was split, it picks the piece that
kept most of the original:

``` r
octo_latestid(old_ids, details = TRUE)
octo_xyz2id("11434, 13413, 2501")      # neuron at a Spelunker position
```

[`octo_xyz2id()`](https://eichlerkathi.github.io/octor-docs/reference/octo_xyz2id.md)
also handles many points, e.g. all synapse positions. Use a checkpoint
file for long runs, so an interruption does not lose the work:

``` r
syn <- readRDS("synapses_v8_positions.rds")
pre <- syn[, c("pre_pt_position_x", "pre_pt_position_y", "pre_pt_position_z")]
syn$pre_root <- octo_xyz2id(pre, voxels = FALSE, checkpoint = "pre_ids.rds")
```

## Meshes

``` r
nl <- octo_read_meshes(ids)          # 10% of faces, fast to plot
nl[, c("cell_type", "soma_side")]
rgl::plot3d(nl)

nl_full <- octo_read_meshes(ids, simplify = 1)   # full resolution
```

Meshes are downloaded in parallel and kept in memory for the R session,
so plotting the same neurons again is instant. For overviews of many
neurons, skeletons are lighter still:

``` r
sk <- octo_skeletonize(ids)
nat::plot3d(sk)
```
