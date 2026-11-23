# Update outdated root IDs

Finds the current root ID for each input, also for IDs that are not in
the seed table (for those,
[`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
is the better route because it works from the seed position). When a
neuron was split, the piece holding most of a random sample of the old
neuron's level-2 chunks is chosen.

## Usage

``` r
octo_latestid(ids, sample = 100L, details = FALSE)
```

## Arguments

- ids:

  root IDs (character)

- sample:

  number of level-2 chunks sampled for split neurons

- details:

  return a data.frame (`old_id`, `new_id`, `n_candidates`, `overlap`)
  instead of a vector

## Value

character vector of current IDs, or a data.frame

## Examples

``` r
if (FALSE) { # \dontrun{
octo_latestid(c("720575940...", "720575940..."))
octo_latestid(old_ids, details = TRUE)   # check overlap for split neurons
} # }
```
