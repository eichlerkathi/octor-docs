# Read the landmark sheet

Read the landmark sheet

## Usage

``` r
read_seymour_octo_landmarks(file)
```

## Arguments

- file:

  CSV export of the landmark sheet with columns `include`, `seymour_loc`
  and `octo_loc` (nm, `"x, y, z"`), plus optional `seg_side`,
  `landmark_name`

## Value

list with `seymour`, `octo` (n x 3, nm) and `names`
