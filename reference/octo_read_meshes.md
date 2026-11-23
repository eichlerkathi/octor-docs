# Read neuron meshes from CAVE

Fetches meshes by root ID into memory (nothing is saved to disk) and
attaches the SeaTable annotations for those IDs. Several meshes are
downloaded in parallel, and meshes already loaded in this R session are
reused (a root ID always refers to the same mesh; edits create new IDs).

## Usage

``` r
octo_read_meshes(
  ids,
  simplify = 0.1,
  threads = 8,
  cache = TRUE,
  timing = FALSE,
  annotate = TRUE,
  cols = c("position", "cell_type", "group", "soma_side", "seymour_match_id"),
  table = getOption("octor.seatable_table")
)

octo_clear_mesh_cache()
```

## Arguments

- ids:

  root IDs as character (numbers lose precision in R)

- simplify:

  reduce mesh resolution after download, for faster plotting: a fraction
  of faces to keep (default `0.1`, i.e. 10%), or a target number of
  faces per neuron (e.g. `50000`). `NULL` or `1` keeps full resolution.
  Uses the Python package fast-simplification (installed by
  [`octo_python_setup()`](https://eichlerkathi.github.io/octor-docs/reference/octo_python_setup.md)),
  or Rvcg if that is missing.

- threads:

  number of meshes downloaded at the same time

- cache:

  reuse meshes already downloaded in this R session. Clear with
  `octo_clear_mesh_cache()`.

- timing:

  print how much time went into downloading and simplifying

- annotate:

  add annotations from the SeaTable seed table

- cols:

  SeaTable columns to add

- table:

  SeaTable table name

## Value

a [nat::neuronlist](https://rdrr.io/pkg/nat/man/neuronlist.html) of
`mesh3d` objects in nm, named by root ID

## Examples

``` r
if (FALSE) { # \dontrun{
nl <- octo_read_meshes(octo_find_ids("^KC"))
nl[, "cell_type"]
rgl::plot3d(nl)
} # }
```
