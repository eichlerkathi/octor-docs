# Get seed table annotations for root IDs

Looks up the SeaTable annotations of neurons by root ID. The result has
one row per input ID, in the same order (duplicates kept), so it can be
added directly to another table, e.g. synapse counts.

## Usage

``` r
octo_annotations(
  ids,
  columns = c("cell_type", "group", "soma_side", "seymour_match_id"),
  all = FALSE,
  table = getOption("octor.seatable_table"),
  refresh = FALSE
)
```

## Arguments

- ids:

  root IDs (character)

- columns:

  seed table columns to return. `NULL` returns all columns.

- all:

  return all matching rows (with the SeaTable row id `_id`) instead of
  one row per input ID

- table:

  SeaTable table name

- refresh:

  read the table again instead of using the cached copy

## Value

data.frame with `root_id`, the requested columns (as text), and
`n_rows`: how many seed rows share this root ID (0 if not found)

## Details

When several rows share a root ID (a neuron seeded more than once), the
trusted row is used: `primary` / `primary (auto)` / `unique` first, then
conflicting rows, then `secondary` ones (see
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)).
Use `all = TRUE` to get every matching row instead.

IDs not found in the table get `NA`. That usually means the neuron has
no seed yet, or the ID is outdated: run
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
to refresh the table, or
[`octo_latestid()`](https://eichlerkathi.github.io/octor-docs/reference/octo_latestid.md)
to update your IDs.

## Examples

``` r
if (FALSE) { # \dontrun{
ann <- octo_annotations(pre_counts$rootid_pre, c("cell_type", "soma_side"))
pre_counts <- cbind(pre_counts, ann[, -1])

octo_annotations("720575940...", columns = NULL)            # everything
octo_annotations(ids, "cell_type", all = TRUE)              # all seed rows
} # }
```
