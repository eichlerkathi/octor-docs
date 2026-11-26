# Add rows to the seed table

Appends the rows of a data.frame to the SeaTable seed table. Only
columns that exist in the table are written (matched by exact name);
others are skipped with a message, and empty values (`NA`) are left
blank. Rows whose position is already in the table are skipped, so
running this twice does not create duplicate seeds.

## Usage

``` r
octo_add_seeds(
  df,
  xyz = NULL,
  voxels = TRUE,
  skip_existing = TRUE,
  dry_run = FALSE,
  table = getOption("octor.seatable_table")
)
```

## Arguments

- df:

  data.frame of new rows

- xyz:

  optional names of three columns with coordinates, e.g.
  `c("x", "y", "z")`, used to fill the `position` column as `"x, y, z"`
  in Spelunker voxels

- voxels:

  with `xyz`: `TRUE` if the coordinates are already Spelunker voxels,
  `FALSE` if they are nm (they are then divided by the voxel size)

- skip_existing:

  skip rows whose position already exists in the table (or appears
  earlier in `df`)

- dry_run:

  only report what would be added

- table:

  SeaTable table name

## Value

invisibly, the rows (as written) that were added, or would be added

## Details

Afterwards run
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
to fill in supervoxel and root IDs (and flag neurons that now have
several seeds).

## Examples

``` r
if (FALSE) { # \dontrun{
new <- data.frame(position = c("11434, 13413, 2501", "9812, 13639, 15827"),
                  cell_type = c("KC", "MBON"), annotator = "Kathi")
octo_add_seeds(new, dry_run = TRUE)
octo_add_seeds(new)
octo_update_ids()

# from a table with nm coordinates, e.g. one position per neuron
octo_add_seeds(pre_counts[pre_counts$n_synapses >= 20, ],
               xyz = c("x", "y", "z"), voxels = FALSE)
} # }
```
