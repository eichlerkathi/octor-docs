# Package index

## Setup

Python environment, tokens and connections.

- [`octo_python_setup()`](https://eichlerkathi.github.io/octor-docs/reference/octo_python_setup.md)
  [`octo_python_check()`](https://eichlerkathi.github.io/octor-docs/reference/octo_python_setup.md)
  : Set up or check the Python environment
- [`octo_get_token()`](https://eichlerkathi.github.io/octor-docs/reference/octo_get_token.md)
  : Get a CAVE token and save it
- [`octo_docs()`](https://eichlerkathi.github.io/octor-docs/reference/octo_docs.md)
  : Open the octor documentation website
- [`octo_cave_client()`](https://eichlerkathi.github.io/octor-docs/reference/octo_cave_client.md)
  [`octo_cloudvolume()`](https://eichlerkathi.github.io/octor-docs/reference/octo_cave_client.md)
  [`octo_seatable()`](https://eichlerkathi.github.io/octor-docs/reference/octo_cave_client.md)
  : Connect to CAVE and SeaTable
- [`octor`](https://eichlerkathi.github.io/octor-docs/reference/octor-package.md)
  [`octor-package`](https://eichlerkathi.github.io/octor-docs/reference/octor-package.md)
  : octor: tools for the octo L1 larva connectome

## Seed table (SeaTable)

Keep root IDs current, flag neurons seeded more than once, and find
neurons.

- [`octo_update_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_update_ids.md)
  : Update supervoxel and root IDs in the SeaTable seed table
- [`octo_flag_duplicates()`](https://eichlerkathi.github.io/octor-docs/reference/octo_flag_duplicates.md)
  : Flag neurons seeded more than once
- [`octo_seeds()`](https://eichlerkathi.github.io/octor-docs/reference/octo_seeds.md)
  : Read the seed table from SeaTable
- [`octo_find_ids()`](https://eichlerkathi.github.io/octor-docs/reference/octo_find_ids.md)
  : Find root IDs by searching a SeaTable column
- [`parse_position()`](https://eichlerkathi.github.io/octor-docs/reference/parse_position.md)
  : Parse position strings

## Meshes, synapses and edits

- [`octo_read_meshes()`](https://eichlerkathi.github.io/octor-docs/reference/octo_read_meshes.md)
  [`octo_clear_mesh_cache()`](https://eichlerkathi.github.io/octor-docs/reference/octo_read_meshes.md)
  : Read neuron meshes from CAVE
- [`octo_synapses()`](https://eichlerkathi.github.io/octor-docs/reference/octo_synapses.md)
  : Query synapses by root ID
- [`octo_synapse_positions()`](https://eichlerkathi.github.io/octor-docs/reference/octo_synapse_positions.md)
  : Download all synapse positions from the annotation service
- [`octo_edit_history()`](https://eichlerkathi.github.io/octor-docs/reference/octo_edit_history.md)
  : Edit history of neurons

## Seymour and octo

Read Seymour neurons from CATMAID and transform between the two
datasets.

- [`seymour2octo()`](https://eichlerkathi.github.io/octor-docs/reference/seymour2octo.md)
  [`octo2seymour()`](https://eichlerkathi.github.io/octor-docs/reference/seymour2octo.md)
  : Transform neurons between Seymour and octo
- [`xform_seymour_to_octo()`](https://eichlerkathi.github.io/octor-docs/reference/xform_seymour_to_octo.md)
  [`xform_octo_to_seymour()`](https://eichlerkathi.github.io/octor-docs/reference/xform_seymour_to_octo.md)
  : Transform points between Seymour and octo
- [`seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/seymour_octo_reg.md)
  : Load the Seymour \<-\> octo registration
- [`fit_seymour_octo_reg()`](https://eichlerkathi.github.io/octor-docs/reference/fit_seymour_octo_reg.md)
  : Fit a Seymour -\> octo registration
- [`read_seymour_octo_landmarks()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_octo_landmarks.md)
  : Read the landmark sheet
- [`read_seymour_neurons()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_neurons.md)
  [`seymour_connectors()`](https://eichlerkathi.github.io/octor-docs/reference/read_seymour_neurons.md)
  : Read Seymour neurons and connectors from CATMAID

## Coordinates

- [`octo_nm2voxel()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nm2voxel.md)
  [`octo_voxel2nm()`](https://eichlerkathi.github.io/octor-docs/reference/octo_nm2voxel.md)
  : Convert octo coordinates between nm and Spelunker voxels
