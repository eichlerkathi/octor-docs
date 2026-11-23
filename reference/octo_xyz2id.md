# Convert between positions, supervoxels and root IDs

`octo_xyz2id()` finds the neuron (root ID) or supervoxel at positions,
`octo_rootid()` the current root ID of supervoxels, and `octo_leaves()`
the supervoxels (or level-2 chunks) that make up a neuron.

## Usage

``` r
octo_xyz2id(xyz, voxels = TRUE, root = TRUE)

octo_rootid(svids)

octo_leaves(id, level = 1)
```

## Arguments

- xyz:

  positions: n x 3 matrix / data.frame, or text like `"1234, 5678, 910"`
  (see
  [`parse_position()`](https://eichlerkathi.github.io/octor-docs/reference/parse_position.md))

- voxels:

  `TRUE` if positions are Spelunker voxel coordinates, `FALSE` if they
  are nm

- root:

  return root IDs (`TRUE`) or supervoxel IDs (`FALSE`)

- svids:

  supervoxel IDs (character)

- id:

  one root ID (character)

- level:

  `1` for supervoxels, `2` for level-2 chunks (far fewer, faster)

## Value

character vector of IDs (`"0"` where a position hits no segment)

## Examples

``` r
if (FALSE) { # \dontrun{
octo_xyz2id("11434, 13413, 2501")
octo_xyz2id(cbind(91472, 107304, 20008), voxels = FALSE)
} # }
```
