# Skeletonize octo neurons

Turns meshes into skeletons with the wavefront method of the Python
package skeletor. Skeletons are much lighter to plot than meshes and can
be compared with other neurons by NBLAST (see
[`octo_nblast_seymour()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nblast_seymour.md)).

## Usage

``` r
octo_skeletonize(
  x,
  simplify = 0.1,
  prune = 1000,
  waves = 1,
  step_size = 1,
  remove_disconnected = 10,
  ...
)
```

## Arguments

- x:

  root IDs (character), or meshes from
  [`octo_read_meshes()`](https://eichlerkathi.github.io/octor-docs/reference/octo_read_meshes.md)

- simplify:

  mesh simplification before skeletonizing (only when `x` are IDs); 10%
  of faces is plenty for the skeleton shape

- prune:

  remove twigs shorter than this (nm); `0` keeps everything

- waves, step_size:

  skeletor wavefront settings: more waves give more robust skeletons,
  larger steps coarser ones

- remove_disconnected:

  drop mesh pieces with fewer faces than this

- ...:

  passed to
  [`octo_read_meshes()`](https://eichlerkathi.github.io/octor-docs/reference/octo_read_meshes.md)

## Value

a [nat::neuronlist](https://rdrr.io/pkg/nat/man/neuronlist.html) of
skeletons in nm, with the annotations of the input

## Examples

``` r
if (FALSE) { # \dontrun{
sk <- octo_skeletonize(octo_find_ids("^MBON"))
plot3d(sk)
} # }
```
