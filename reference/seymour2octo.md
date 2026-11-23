# Transform neurons between Seymour and octo

Works on points (matrix / data.frame), neurons, neuronlists (CATMAID
neurons including their connectors), dotprops and meshes. Coordinates
are nm.

## Usage

``` r
seymour2octo(x, reg = seymour_octo_reg(), ...)

octo2seymour(x, reg = seymour_octo_reg(), ...)
```

## Arguments

- x:

  object to transform

- reg:

  registration, see
  [`seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/seymour_octo_reg.md)

- ...:

  passed to [`nat::xform()`](https://rdrr.io/pkg/nat/man/xform.html)

## Examples

``` r
if (FALSE) { # \dontrun{
nl <- read_seymour_neurons("annotation:^MBON$")
nl_octo <- seymour2octo(nl)
} # }
```
