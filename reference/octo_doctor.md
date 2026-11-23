# Check that everything octor needs is set up

Checks R packages, Python and its packages, both tokens, the CAVE server
(token accepted, materialization), the SeaTable seed table (columns and
column types) and the Seymour registration. Run this first when
something does not work, or when helping someone set up.

## Usage

``` r
octo_doctor(table = getOption("octor.seatable_table"))
```

## Arguments

- table:

  SeaTable table name

## Value

invisibly, a data.frame of checks with `status` `"ok"`, `"note"`
(optional or informational) or `"problem"`

## Examples

``` r
if (FALSE) { # \dontrun{
octo_doctor()
} # }
```
