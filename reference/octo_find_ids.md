# Find root IDs by searching a SeaTable column

Find root IDs by searching a SeaTable column

## Usage

``` r
octo_find_ids(
  pattern,
  column = "cell_type",
  exact = FALSE,
  ignore.case = TRUE,
  table = getOption("octor.seatable_table")
)
```

## Arguments

- pattern:

  regular expression (or exact value with `exact = TRUE`)

- column:

  column to search, `cell_type` by default

- exact:

  match the whole value (case-insensitive) instead of a regex

- ignore.case:

  passed to [`grepl()`](https://rdrr.io/r/base/grep.html)

- table:

  SeaTable table name

## Value

character vector of root IDs, one per neuron

## Examples

``` r
if (FALSE) { # \dontrun{
ids <- octo_find_ids("^MBON")
ids <- octo_find_ids("^L$", column = "soma_side")
nl <- octo_read_meshes(ids)
} # }
```
