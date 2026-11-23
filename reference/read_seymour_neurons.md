# Read Seymour neurons and connectors from CATMAID

Reads in chunks (large requests can time out with 502 errors), retries
failed chunks neuron by neuron, and skips neurons that cannot be read
(e.g. single-node skeletons).

## Usage

``` r
read_seymour_neurons(
  skids = "annotation:^all_somas$",
  conn = NULL,
  chunk = 50,
  pid = 1
)

seymour_connectors(
  skids = "annotation:^all_somas$",
  conn = NULL,
  direction = "outgoing",
  chunk = 20,
  pid = 1
)
```

## Arguments

- skids:

  skeleton IDs or a query understood by
  [`catmaid::catmaid_skids()`](https://rdrr.io/pkg/catmaid/man/catmaid_skids.html),
  e.g. `"annotation:^all_somas$"`

- conn:

  CATMAID connection from
  [`catmaid::catmaid_login()`](https://rdrr.io/pkg/catmaid/man/catmaid_login.html)

- chunk:

  skeletons per request

- pid:

  CATMAID project ID

- direction:

  `"outgoing"` (presynaptic connectors), `"incoming"` or `"both"`

## Value

`seymour_connectors()`: data.table with one row per connector
(`connector_id`, `x`, `y`, `z`, nm)
