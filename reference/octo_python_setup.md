# Set up or check the Python environment

`octo_python_setup()` installs the Python packages octor needs. If the
natverse package fafbseg is installed, it uses
[`fafbseg::simple_python()`](https://rdrr.io/pkg/fafbseg/man/simple_python.html)
(the same Python environment as the rest of the natverse, which already
contains caveclient, cloud-volume and seatable-api) and adds the mesh
simplifier and skeletonizer. Otherwise it creates its own virtual
environment. `octo_python_check()` reports which Python reticulate uses
and whether the packages are available.

## Usage

``` r
octo_python_setup(use_fafbseg = TRUE, envname = "r-octor", python = NULL)

octo_python_check()
```

## Arguments

- use_fafbseg:

  use
  [`fafbseg::simple_python()`](https://rdrr.io/pkg/fafbseg/man/simple_python.html)
  when fafbseg is installed

- envname:

  name of the virtual environment (only without fafbseg)

- python:

  optional path to a Python 3 to base it on (only without fafbseg)

## Details

reticulate chooses its Python once per R session; restart R after
installing. If R picks the wrong Python, set `RETICULATE_PYTHON` in
`~/.Renviron`.
