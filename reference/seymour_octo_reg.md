# Load the Seymour \<-\> octo registration

The registration (about 60 MB) is not part of the package. Point octor
to it once, e.g. in `.Rprofile`:
`options(octor.seymour_reg = "/path/to/seymour_octo_reg.rds")`, or a URL
(e.g. a GitHub release asset), which is downloaded once to the user
cache. Make your own with
[`fit_seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/fit_seymour_octo_reg.md).

## Usage

``` r
seymour_octo_reg(path = getOption("octor.seymour_reg"), refresh = FALSE)
```

## Arguments

- path:

  file path or URL

- refresh:

  reload / download again
