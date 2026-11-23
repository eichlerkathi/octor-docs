# Flag neurons seeded more than once

Rows with the same root ID are the same neuron. In each such group
exactly one row should be the trusted ("primary") row; the others are
"secondary".

## Usage

``` r
octo_flag_duplicates(root, primary, ctime, pos, info = rep(0L, length(root)))
```

## Arguments

- root:

  root IDs (character)

- primary:

  logical, rows currently marked primary

- ctime:

  creation time (anything that sorts correctly, e.g. ISO strings)

- pos:

  label of each row, used in `same_as` (e.g. the position)

- info:

  number of filled annotation fields per row

## Value

data.frame with `n_seeds`, `status`, `primary`, `same_as`

## Details

- no row marked primary: the row with the most information (`info`)
  becomes primary, ties go to the oldest (`ctime`); status
  `"primary (auto)"`

- one row marked: status `"primary"`, the others `"secondary"`

- several marked: `"CONFLICT: n primaries"`, usually because
  proofreading merged two neurons that were both annotated

- root ID `"0"` or empty: `"no segment"`
