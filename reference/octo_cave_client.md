# Connect to CAVE and SeaTable

Connections are created once and reused within an R session.

## Usage

``` r
octo_cave_client(
  datastack = getOption("octor.datastack"),
  server = getOption("octor.cave_server"),
  refresh = FALSE
)

octo_cloudvolume(refresh = FALSE)

octo_seatable(url = getOption("octor.seatable_url"), refresh = FALSE)
```

## Arguments

- datastack, server:

  CAVE datastack and server

- refresh:

  create a new connection even if one is cached

- url:

  SeaTable server

## Value

a Python CAVEclient / CloudVolume / seatable_api Base object

## Examples

``` r
if (FALSE) { # \dontrun{
client <- octo_cave_client()
client$info$get_datastack_info()
} # }
```
