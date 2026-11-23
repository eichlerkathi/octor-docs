# Query synapses by root ID

Needs a materialized datastack. Without `version` the query is live, so
root IDs must be current (run
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
first).

## Usage

``` r
octo_synapses(pre = NULL, post = NULL, table = "synapses_v8", version = NULL)
```

## Arguments

- pre, post:

  root IDs (character) of pre- and/or postsynaptic neurons

- table:

  synapse table

- version:

  materialization version, `NULL` for a live query

## Value

data.frame; ID columns as character, positions split into `_x/_y/_z`
