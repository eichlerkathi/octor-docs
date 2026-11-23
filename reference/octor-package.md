# octor: tools for the octo L1 larva connectome

Settings are R options, so they can be changed per user or per project
(e.g. in `.Rprofile`):

## Details

- `octor.cave_server`, `octor.datastack`: CAVE server and datastack

- `octor.cave_token_env`: name of the environment variable holding your
  CAVE token (default `CAVE_TOKEN_BRAININBRAIN`)

- `octor.seatable_url`, `octor.seatable_table`: SeaTable server and
  table

- `octor.seatable_token_env`: environment variable holding the SeaTable
  base API token (default `SEATABLE_API_TOKEN`)

- `octor.voxel_size`: Spelunker voxel size in nm (default `c(8, 8, 8)`)

- `octor.seymour_reg`: path to the Seymour \<-\> octo registration file

Tokens are never stored in the package. Put them in `~/.Renviron`, e.g.
`CAVE_TOKEN_BRAININBRAIN=...` and `SEATABLE_API_TOKEN=...`.

## See also

Useful links:

- <https://eichlerkathi.github.io/octor-docs/>

## Author

**Maintainer**: Katharina Eichler <eichlerkathi537@gmail.com>

Authors:

- Katharina Eichler <eichlerkathi537@gmail.com>
