# Get a CAVE token and save it

Opens the token page of the octo CAVE server in your browser, asks you
to paste the token, checks that it works, and saves it to your user
`.Renviron` (as `CAVE_TOKEN_BRAININBRAIN` by default) and to the current
R session, so octor finds it from now on.

## Usage

``` r
octo_get_token(
  token = NULL,
  new = FALSE,
  validate = TRUE,
  server = getOption("octor.cave_server"),
  renviron = Sys.getenv("R_ENVIRON_USER", "~/.Renviron")
)
```

## Arguments

- token:

  a token you already have. If `NULL` (the default), the browser opens
  and you are asked to paste one.

- new:

  open the page that creates a new token (`TRUE`) or the page that lists
  your existing tokens (`FALSE`, the default). Reusing an existing token
  is usually better.

- validate:

  check the token against the server before saving

- server:

  CAVE server whose auth service issues the token

- renviron:

  file to save the token in

## Value

invisibly, the token

## Details

The variable name is set by `options(octor.cave_token_env)`. Tokens for
other CAVE servers (e.g. in `~/.cloudvolume/secrets`) are not touched.

## Examples

``` r
if (FALSE) { # \dontrun{
octo_get_token()               # look up an existing token
octo_get_token(new = TRUE)     # create a new one
octo_get_token("abc123...")    # save a token you already have
} # }
```
