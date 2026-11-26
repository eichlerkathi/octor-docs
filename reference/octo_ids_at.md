# Root IDs of neurons at another time

Shows what neurons were (or became) at a given time: for each root ID, a
sample of its supervoxels is looked up at `timestamp`. Supervoxels never
change, so this works for current and outdated IDs, and in both
directions in time. A neuron that was assembled by merges since then
maps to several earlier pieces; the largest is returned as `id_at`.

## Usage

``` r
octo_ids_at(ids, timestamp, sample = 200L, details = FALSE)
```

## Arguments

- ids:

  root IDs (character)

- timestamp:

  POSIXct, Date or text such as `"2026-11-01 14:00"` (read as UTC unless
  it has an offset)

- sample:

  supervoxels sampled per neuron

- details:

  return a data.frame with all pieces instead of a vector

## Value

character vector of root IDs at `timestamp` (`"0"` if the neuron's
supervoxels belonged to no neuron then), or a data.frame with `id`,
`id_at`, `fraction` (share of sampled supervoxels in `id_at`),
`n_pieces` and `pieces`

## Examples

``` r
if (FALSE) { # \dontrun{
octo_ids_at(octo_find_ids("^KC"), "2026-10-01")
octo_ids_at("720575940...", as.POSIXct("2026-11-20 09:00", tz = "Europe/Berlin"),
            details = TRUE)
} # }
```
