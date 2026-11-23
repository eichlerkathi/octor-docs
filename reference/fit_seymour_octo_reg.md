# Fit a Seymour -\> octo registration

Affine fit from landmarks, then a coarse-to-fine non-rigid warp that
pulls the Seymour synapse cloud onto the octo synapse cloud while
keeping the landmarks in place.

## Usage

``` r
fit_seymour_octo_reg(
  landmarks,
  octo_xyz,
  seymour_xyz,
  holdout = NULL,
  cell = 2000,
  sigma = c(24000, 12000, 6000, 3000),
  iter = c(6, 6, 5, 4),
  trim = c(12000, 8000, 5000, 3000),
  landmark_weight = 1000,
  regularise = 5,
  cv_folds = 0
)
```

## Arguments

- landmarks:

  output of
  [`read_seymour_octo_landmarks()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_octo_landmarks.md)

- octo_xyz:

  octo synapse positions (n x 3, nm), e.g. presynaptic positions from
  [`octo_synapse_positions()`](https://eichlerkathi.github.io/octor-docs/reference/octo_synapse_positions.md)

- seymour_xyz:

  Seymour connector positions (n x 3, nm), e.g. from
  [`seymour_connectors()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_neurons.md)

- holdout:

  landmark rows not used for fitting, only to measure the error

- cell:

  downsampling grid (nm)

- sigma, iter, trim:

  smoothing width (nm), iterations and maximum matching distance (nm)
  per level

- landmark_weight:

  how many cloud points each landmark counts as

- regularise:

  pulls the warp towards zero where there are few points

- cv_folds:

  if \> 0, also estimate the error by k-fold cross-validation over
  landmarks (takes `cv_folds` times longer)

## Value

a `seymour_octo_reg` object; save with
[`saveRDS()`](https://rdrr.io/r/base/readRDS.html)

## Examples

``` r
if (FALSE) { # \dontrun{
lm  <- read_seymour_octo_landmarks("seymour_octo_reg.csv")
syn <- octo_synapse_positions()
con <- readRDS("seymour_connectors.rds")
reg <- fit_seymour_octo_reg(lm, syn[, c("pre_pt_position_x", "pre_pt_position_y",
                                        "pre_pt_position_z")], con[, c("x", "y", "z")])
saveRDS(reg, "seymour_octo_reg.rds")
} # }
```
