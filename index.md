# octor

R tools for the **octo L1 larva connectome** in CAVE
(`zlatic_octo-2_datastack`), a SeaTable table of neuron seeds, and the
**Seymour** L1 larva in CATMAID.

- keep supervoxel and root IDs in SeaTable current, and flag neurons
  seeded more than once
- find neurons by cell type and read their meshes (simplified for fast
  plotting)
- query synapses, or download all synapse positions
- transform neurons between Seymour and octo (landmarks + synapse-cloud
  registration)

## Installation

octor lives in a private repository. To install it you need read access
(ask the repository owner to add you as a collaborator) and a GitHub
token:

``` r
install.packages(c("remotes", "usethis", "gitcreds"))
usethis::create_github_token()   # tick the "repo" scope, generate, copy the token
gitcreds::gitcreds_set()         # paste the token when asked
remotes::install_github("eichlerkathi/octor")
```

Use a **classic** token. Fine-grained tokens often cannot read private
repositories owned by another account.

## Setup

### 1. Python

octor talks to CAVE, SeaTable and CloudVolume through Python (via
reticulate). Install the Python packages once:

``` r
octor::octo_python_setup()
```

If you have the natverse package
[fafbseg](https://github.com/natverse/fafbseg) installed, this uses
[`fafbseg::simple_python()`](https://rdrr.io/pkg/fafbseg/man/simple_python.html),
so octor shares the natverse Python environment. Otherwise octor creates
its own environment and prints a `RETICULATE_PYTHON=...` line to add to
`~/.Renviron`.

Restart R afterwards.

### 2. CAVE token

``` r
library(octor)
octo_get_token()
```

This opens the token page of the octo CAVE server in your browser. Log
in, copy your token and paste it into the R console. octor checks that
the token works and saves it as `CAVE_TOKEN_BRAININBRAIN` in
`~/.Renviron`, so you only do this once. Tokens for other CAVE datasets
are not affected.

If you have no token yet, use `octo_get_token(new = TRUE)`.

### 3. SeaTable token

In SeaTable, open the base, then **? menu ? Advanced ? API Token** and
create a token with read-write permission. Add it to `~/.Renviron` (open
the file with
[`usethis::edit_r_environ()`](https://usethis.r-lib.org/reference/edit.html)):

    SEATABLE_API_TOKEN=<API token of the SeaTable base>

Restart R.

### 4. Check

``` r
library(octor)
octo_python_check()   # Python and packages
octo_find_ids("KC")   # SeaTable connection
```

### Troubleshooting

- **R uses the wrong Python:** reticulate picks its Python once per
  session. Set `RETICULATE_PYTHON=/path/to/python` in `~/.Renviron` and
  restart R.
- **Mesh or synapse results look like Python objects instead of R
  data:** update reticulate (`install.packages("reticulate")`); numpy 2
  needs reticulate 1.38 or newer.
- **Token rejected:** run
  [`octo_get_token()`](https://eichlerkathi.github.io/octor-docs/reference/octo_get_token.md)
  again; tokens can expire.

## Settings

Defaults are set as R options. To change one, e.g. in `~/.Rprofile`:

``` r
options(octor.seatable_table = "Seeds",
        octor.seatable_url   = "https://cloud.seatable.io",
        octor.seymour_reg    = "~/data/seymour_octo_reg.rds")
```

See
[`?octor`](https://eichlerkathi.github.io/octor-docs/reference/octor-package.md)
for all options.

## Usage

### SeaTable seeds

``` r
octo_update_ids()                 # supervoxels, root IDs, double-seed flags
seeds <- octo_seeds(trusted_only = TRUE)
```

The seed table needs these columns: `position` (Text, Spelunker voxel
coordinates), `supervoxel_id`, `root_id`, `root_id_previous`,
`dup_status` and `same_as` (Text), `root_changed_on` and
`ids_checked_on` (Date), `n_seeds` (Number) and `primary` (Checkbox).
Keep the ID columns as **Text**: Number columns corrupt 64-bit IDs.

Neurons with several seeds share a root ID. In each group, tick
`primary` on the row you trust. If no row is ticked, the row with the
most annotation filled in is picked. A SeaTable view filtered on
`n_seeds > 1` and grouped by `root_id` shows the groups together.

### Meshes

``` r
ids <- octo_find_ids("^MBON")             # regex on cell_type
nl  <- octo_read_meshes(ids)              # 10% of faces by default
nl[, c("cell_type", "soma_side")]
rgl::plot3d(nl)
```

### Synapses

``` r
syn <- octo_synapses(pre = ids)           # needs a materialized datastack
pos <- octo_synapse_positions()           # all positions, no root IDs, resumable
```

### Seymour → octo

``` r
library(catmaid)
conn <- catmaid_login(server = ..., token = ...)
nl <- read_seymour_neurons("annotation:^MBON$", conn = conn)
nl_octo <- seymour2octo(nl)               # skeletons + connectors, nm
```

The registration file (about 60 MB) is not in the package. Get it at:
<https://drive.google.com/file/d/1NJ-pJxH3CVPlpYD6es03B_MLNaUVh44h/view?usp=sharing>,
point `options(octor.seymour_reg = ...)` to it (a file path or a URL),
or fit your own:

``` r
lm  <- read_seymour_octo_landmarks("seymour_octo_reg.csv")
con <- seymour_connectors("annotation:^all_somas$", conn = conn)
reg <- fit_seymour_octo_reg(lm, pos[, c("pre_pt_position_x", "pre_pt_position_y",
                                        "pre_pt_position_z")],
                            con[, c("x", "y", "z")], cv_folds = 5)
saveRDS(reg, "seymour_octo_reg.rds")
```

With the current 30 landmarks, the cross-validated error is about 3.6
µm.
