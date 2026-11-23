# When were neurons last edited?

A root ID is created by the last edit of its neuron, so its creation
time is the time of the last merge or split (or of the initial
segmentation for neurons never edited).

## Usage

``` r
octo_last_modified(ids)
```

## Arguments

- ids:

  root IDs (character)

## Value

POSIXct (UTC), named by ID

## Examples

``` r
if (FALSE) { # \dontrun{
seeds <- octo_seeds(c("root_id", "cell_type"), trusted_only = TRUE)
seeds$last_edit <- octo_last_modified(seeds$root_id)
} # }
```
