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

- `octor.spelunker_url`: viewer for
  [`octo_scene()`](https://eichlerkathi.github.io/octor-docs/reference/octo_scene.md)
  (default: the datastack's)

- `octor.segmentation_source`, `octor.image_source`: layer sources for
  [`octo_scene()`](https://eichlerkathi.github.io/octor-docs/reference/octo_scene.md),
  as they appear in a working Spelunker state. Preset to the octo
  segmentation and EM (`precomputed://gs://fly-larva-sf/octo/clahe`);
  `NULL` takes them from the datastack's settings (see
  [`octo_scene_sources()`](https://eichlerkathi.github.io/octor-docs/reference/octo_scene_sources.md))

- `octor.seed_cache_seconds`: how long the seed table is kept in memory

Tokens are never stored in the package.
[`octo_get_token()`](https://eichlerkathi.github.io/octor-docs/reference/octo_get_token.md)
saves your CAVE token for you; otherwise put tokens in `~/.Renviron`,
e.g. `CAVE_TOKEN_BRAININBRAIN=...` and `SEATABLE_API_TOKEN=...`.

## See also

Useful links:

- <https://eichlerkathi.github.io/octor-docs/>

## Author

**Maintainer**: Katharina Eichler <eichlerkathi537@gmail.com>

Authors:

- Katharina Eichler <eichlerkathi537@gmail.com>
