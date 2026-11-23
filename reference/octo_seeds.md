# Read the seed table from SeaTable

The table is kept in memory for a few minutes, so repeated calls (e.g.
from
[`octo_find_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_find_ids.md)
or
[`octo_scene()`](https://eichlerkathi.github.io/octor-docs/reference/octo_scene.md))
do not download it again. Set the time with
`options(octor.seed_cache_seconds = 300)`; `0` turns caching off.
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
clears the cache after writing.

## Usage

``` r
octo_seeds(
  columns = NULL,
  trusted_only = FALSE,
  table = getOption("octor.seatable_table"),
  refresh = FALSE
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

- refresh:

  read the table again even if it is cached

## Value

a data.frame with all values as text, plus the SeaTable row id `_id`
