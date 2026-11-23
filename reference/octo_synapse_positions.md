# Download all synapse positions from the annotation service

Works without materialization: returns positions only (no root IDs).
Downloads in resumable chunks (CSV files in `outdir`); run again after
an interruption to continue.

## Usage

``` r
octo_synapse_positions(
  table = "synapses_v8",
  start = 1L,
  stop = NULL,
  outdir = paste0(table, "_chunks"),
  chunk = 100000L,
  valid_only = TRUE
)
```

## Arguments

- table:

  annotation table

- start, stop:

  range of annotation IDs (default: all)

- outdir:

  folder for the chunk files

- chunk:

  annotation IDs per chunk file

- valid_only:

  drop rows with `valid == FALSE`

## Value

data.table with `id`, `score`, `valid` and position columns (nm)
