# Show the layer sources used by octo_scene()

Prints the EM image and segmentation sources
[`octo_scene()`](https://eichlerkathi.github.io/octor-docs/reference/octo_scene.md)
uses, and where each comes from (option or datastack settings). Useful
when a scene does not open correctly.

## Usage

``` r
octo_scene_sources()
```

## Value

invisibly, a list with `image`, `segmentation`, `viewer`
