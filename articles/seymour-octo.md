# Seymour and octo

Seymour is an L1 larva reconstructed in CATMAID; octo is a second L1
larva in CAVE. octor includes a registration between the two, so neurons
can be compared directly.

## Using the registration

The registration file (`seymour_octo_reg.rds`, about 60 MB) is shared
separately. Point octor to it once, e.g. in `~/.Rprofile`:

``` r
options(octor.seymour_reg = "/path/to/seymour_octo_reg.rds")
```

Then:

``` r
library(octor)
library(catmaid)
conn <- catmaid_login(server = "...", token = "...")

nl <- read_seymour_neurons("annotation:^MBON$", conn = conn)
nl_octo <- seymour2octo(nl)            # skeletons and connectors

meshes <- octo_read_meshes(octo_find_ids("^MBON"))
rgl::plot3d(meshes, alpha = 0.3)
rgl::plot3d(nl_octo, col = "red")
```

[`seymour2octo()`](https://eichlerkathi.github.io/octor-docs/reference/seymour2octo.md)
and
[`octo2seymour()`](https://eichlerkathi.github.io/octor-docs/reference/seymour2octo.md)
work on neurons, neuronlists, meshes and point matrices. All coordinates
are in nm. Spelunker shows octo in 8 nm voxels; convert with
[`octo_nm2voxel()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nm2voxel.md)
and
[`octo_voxel2nm()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nm2voxel.md).

## Finding matching Seymour neurons

[`octo_nblast_seymour()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nblast_seymour.md)
moves Seymour neurons into octo space and compares them with octo
skeletons by NBLAST, which scores similarity of shape and position. For
each octo neuron it lists the best Seymour candidates:

``` r
sey <- read_seymour_neurons("annotation:^MBON$", conn = conn)
m <- octo_nblast_seymour(octo_find_ids("^MBON"), sey, top = 3)
m[m$rank == 1, c("octo_id", "cell_type", "seymour_name", "score")]
```

Scores go up to 1. With a registration error of a few µm, compare
against a sensible candidate set (same lineage or neuropil) rather than
all of Seymour, and check the top matches by eye before filling
`seymour_match_id`.

## How the registration was made

1.  **Landmarks:** 30 corresponding points (midline points of every VNC
    segment and mushroom body landmarks on both sides) give an affine
    transform. Octo is about 1.4 times larger than Seymour in x and y
    and 1.2 times in z; there is no mirroring.
2.  **Synapse clouds:** a smooth non-rigid warp then pulls Seymour’s
    presynaptic connectors onto octo’s synapse predictions
    (`synapses_v8`), coarse to fine, while the landmarks are kept in
    place.

| Method                       | Mean error on held-out landmarks |
|------------------------------|----------------------------------|
| Landmark affine only         | 5.2 µm                           |
| Affine + synapse clouds only | 4.6 µm                           |
| Landmarks + synapse clouds   | **3.6 µm**                       |

Errors were measured by 5-fold cross-validation over the landmarks.

The weakest region is the posterior VNC. Seymour’s connectors there are
sparse, and the only landmarks are on the midline. Adding lateral
landmarks there and in the brain outside the mushroom body is the
easiest way to improve it.

## Refitting

``` r
lm  <- read_seymour_octo_landmarks("seymour_octo_reg.csv")
syn <- octo_synapse_positions()                       # resumable download
con <- seymour_connectors("annotation:^all_somas$", conn = conn)

reg <- fit_seymour_octo_reg(
  lm,
  syn[, c("pre_pt_position_x", "pre_pt_position_y", "pre_pt_position_z")],
  con[, c("x", "y", "z")],
  cv_folds = 5)
reg
saveRDS(reg, "seymour_octo_reg.rds")
```

The landmark sheet needs the columns `include`, `seymour_loc` and
`octo_loc` (nm, `"x, y, z"`). Only rows with `include` set to `TRUE` are
used.
