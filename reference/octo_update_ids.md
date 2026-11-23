# Update supervoxel and root IDs in the SeaTable seed table

Looks up the supervoxel at each seed position (only where missing,
unless `refresh_supervoxels = TRUE`), gets its current root ID, records
root ID changes and flags neurons seeded more than once (see
[`octo_flag_duplicates()`](https://eichlerkathi.github.io/octor-docs/reference/octo_flag_duplicates.md)).
Read-only on the CAVE side.

## Usage

``` r
octo_update_ids(
  table = getOption("octor.seatable_table"),
  coord_res = getOption("octor.voxel_size"),
  info_cols = c("cell_type", "group", "soma_side", "reconstructor", "annotator",
    "seymour_match_id"),
  refresh_supervoxels = FALSE,
  dry_run = FALSE,
  cols = NULL
)
```

## Arguments

- table:

  SeaTable table name

- coord_res:

  voxel size (nm) of the positions

- info_cols:

  columns whose filled-in values decide which row becomes primary when
  none is marked

- refresh_supervoxels:

  look up supervoxels again for all rows

- dry_run:

  compute everything but do not write to SeaTable

- cols:

  named character vector to rename the expected columns, e.g.
  `c(position = "xyz")`

## Value

invisibly, a data.frame with the new values per row

## Details

Expected columns (names can be changed via `cols`): `position` (text,
Spelunker voxel coordinates), `supervoxel_id`, `root_id`,
`root_id_previous`, `dup_status`, `same_as` (text), `root_changed_on`,
`ids_checked_on` (date), `n_seeds` (number), `primary` (checkbox). Keep
the ID columns as Text: Number columns corrupt 64-bit IDs.

## Examples

``` r
if (FALSE) { # \dontrun{
res <- octo_update_ids(dry_run = TRUE)
table(res$dup_status)
octo_update_ids()
} # }
```
