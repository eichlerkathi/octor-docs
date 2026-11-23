# Read the seed table from SeaTable

Read the seed table from SeaTable

## Usage

``` r
octo_seeds(
  columns = NULL,
  trusted_only = FALSE,
  table = getOption("octor.seatable_table")
)
```

## Arguments

- columns:

  columns to read (missing ones are skipped with a message). `NULL`
  reads all columns.

- trusted_only:

  keep only one row per neuron: rows whose `dup_status` is not
  `secondary` or `no segment` (see
  [`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)).

- table:

  SeaTable table name

## Value

a data.frame with all values as text, plus the SeaTable row id `_id`
