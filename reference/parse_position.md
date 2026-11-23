# Parse position strings

Reads `"1234, 5678, 910"`, `"[1234 5678 910]"`, tab-separated values
etc.

## Usage

``` r
parse_position(x)
```

## Arguments

- x:

  character vector

## Value

n x 3 numeric matrix; `NA` rows where a value does not contain exactly
three numbers

## Examples

``` r
parse_position(c("1, 2, 3", "[4 5 6]", "7\t8\t9", "bad"))
#>       x  y  z
#> [1,]  1  2  3
#> [2,]  4  5  6
#> [3,]  7  8  9
#> [4,] NA NA NA
```
