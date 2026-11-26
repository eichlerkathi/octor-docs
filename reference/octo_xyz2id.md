# Convert between positions, supervoxels and root IDs

`octo_xyz2id()` finds the neuron (root ID) or supervoxel at positions,
`octo_rootid()` the root ID of supervoxels, and `octo_leaves()` the
supervoxels (or level-2 chunks) that make up a neuron. With `timestamp`,
root IDs are looked up as they were at that time instead of now (see
also
[`octo_ids_at()`](https://eichlerkathi.github.io/octor-docs/reference/octo_ids_at.md)).

## Usage

``` r
octo_xyz2id(xyz, voxels = TRUE, root = TRUE, timestamp = NULL)

octo_rootid(svids, timestamp = NULL)

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

- timestamp:

  look up root IDs at this time instead of now: POSIXct, Date or text
  such as `"2026-11-01 14:00"` (read as UTC unless it has an offset,
  e.g. `"2026-11-01T15:00:00+01:00"`)

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
octo_xyz2id("11434, 13413, 2501", timestamp = "2026-10-01")   # as it was then
} # }
```
