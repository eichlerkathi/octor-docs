# Find matching Seymour neurons for octo neurons

Moves Seymour neurons into octo space with the registration, then
compares them with octo skeletons by NBLAST (shape and position) and
lists the best matches for each octo neuron. Use the result to fill
`seymour_match_id` in the seed table.

## Usage

``` r
octo_nblast_seymour(
  octo,
  seymour,
  top = 5,
  reg = seymour_octo_reg(),
  resample = 1,
  k = 5
)
```

## Arguments

- octo:

  octo skeletons from
  [`octo_skeletonize()`](https://eichlerkathi.github.io/octor-docs/reference/octo_skeletonize.md),
  or root IDs

- seymour:

  Seymour neurons in Seymour space, e.g. from
  [`read_seymour_neurons()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_neurons.md)

- top:

  number of matches listed per octo neuron

- reg:

  registration, see
  [`seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/seymour_octo_reg.md)

- resample, k:

  dotprops settings (µm and neighbours)

## Value

data.frame with `octo_id`, octo annotations, `rank`, `seymour_id`,
`seymour_name`, `score` (mean of both directions), `score_fwd`,
`score_rev`. The full score matrix is in `attr(, "scores")`.

## Details

NBLAST scores range up to 1 (identical). The mean of both directions is
used for ranking. Keep the registration error (a few µm) in mind:
compare candidates that share a lineage or neuropil, and check matches
by eye.

## Examples

``` r
if (FALSE) { # \dontrun{
sey <- read_seymour_neurons("annotation:^MBON$", conn = conn)
m <- octo_nblast_seymour(octo_find_ids("^MBON"), sey)
m[m$rank == 1, c("octo_id", "cell_type", "seymour_name", "score")]
} # }
```
