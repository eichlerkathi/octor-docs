# Open neurons in Spelunker

Builds a Spelunker (Neuroglancer) link showing the given neurons on the
octo EM, optionally coloured by a column of the seed table and with the
seed points as annotations. The link is shortened through the CAVE state
service; if that fails, a long link containing the whole state is
returned.

## Usage

``` r
octo_scene(
  ids = character(),
  color_by = NULL,
  colors = NULL,
  seeds = FALSE,
  position = NULL,
  layout = "xy-3d",
  shorten = TRUE,
  open = FALSE,
  table = getOption("octor.seatable_table")
)
```

## Arguments

- ids:

  root IDs (character); may be empty for a blank scene

- color_by:

  seed table column to colour neurons by, e.g. `"cell_type"`

- colors:

  colours instead of `color_by`: one colour, or a vector named by root
  ID or by values of `color_by`

- seeds:

  add the seed points of these neurons as an annotation layer

- position:

  centre of the view in Spelunker voxels; default the first neuron's
  seed (if found in the seed table)

- layout:

  Neuroglancer layout, e.g. `"xy-3d"`, `"3d"`, `"4panel"`

- shorten:

  upload the state and return a short link

- open:

  open the link in the browser

- table:

  SeaTable table name

## Value

the link (invisibly if `open = TRUE`)

## Details

The image and segmentation sources, voxel size and Spelunker address
come from the datastack's settings on the CAVE server. Set
`options(octor.spelunker_url = ...)` to use another viewer.

## Examples

``` r
if (FALSE) { # \dontrun{
octo_scene(octo_find_ids("^MBON"), color_by = "cell_type", open = TRUE)
octo_scene(c("720575940...", "720575940..."), colors = c("red", "cyan"))
} # }
```
