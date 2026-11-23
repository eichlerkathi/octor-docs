# Transform points between Seymour and octo

Low-level point transforms (nm in, nm out). For neurons use
[`seymour2octo()`](https://eichlerkathi.github.io/octor-docs/reference/seymour2octo.md).

## Usage

``` r
xform_seymour_to_octo(xyz, reg = seymour_octo_reg())

xform_octo_to_seymour(xyz, reg = seymour_octo_reg(), iter = 20)
```

## Arguments

- xyz:

  n x 3 matrix or data.frame; `NA` rows pass through

- reg:

  registration, see
  [`seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/seymour_octo_reg.md)

- iter:

  iterations for inverting each displacement field
