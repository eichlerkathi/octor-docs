# Edit history of neurons

Lists the proofreading edits (merges and splits) that led to each root
ID: when, by whom, and which root IDs went in and came out.

## Usage

``` r
octo_edit_history(ids, details = FALSE, filtered = TRUE)
```

## Arguments

- ids:

  root IDs as character

- details:

  also fetch where each edit happened (`source_coords` and
  `sink_coords`: the points clicked for the merge or split, usually in
  Spelunker voxel coordinates). One extra request per 200 edits.

- filtered:

  only edits that affect the current state of the neuron (`TRUE`), or
  also edits on pieces that were later split off (`FALSE`)

## Value

data.frame with one row per edit, sorted by neuron and time; `timestamp`
is POSIXct (UTC). The attribute `latest` says which input IDs are
current.

## Details

The history of an outdated root ID ends where that ID was replaced. Run
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
first, or look up current IDs, to see the full history.

## Examples

``` r
if (FALSE) { # \dontrun{
h <- octo_edit_history(octo_find_ids("^MBON-a1"))
table(h$root_id, h$type)
h[h$type == "split", c("timestamp", "user_name", "before_root_ids")]
} # }
```
