# Texture Attributes Across Material Contexts

A dataset of 5,553 real-world texture photographs, each labeled with one of 47 texture categories (*banded*, *cracked*, *honeycombed*, *marbled*, *zigzagged*, ...), with context tags describing the material or object the texture appears on.

## Overview

The task is to predict the texture category (`classe`) of each image.

The same texture category appears on very different materials (a *striped* shirt, a *striped* zebra, a *striped* wall), and very different-looking surfaces can share the same category. Each image also comes with `context_tags` (e.g. `fabric`, `food`, `rock`, `home_furnishing`) describing the material, object or scene on which the texture appears.

Image filenames are randomly generated UUIDs, so filenames do not reveal the category.

## Files

- `data.csv` — one row per image:
  - `id`: String. Random UUID of the image.
  - `path`: String. Relative path to the image, `images/<id>.jpg`.
  - `classe`: String. Texture category, one of 47 values. Target column.
  - `context_tags`: String. 1–4 tags separated by `|`, from a vocabulary of 24 tags.
- `images/` — 5,553 JPEG files (RGB, variable resolution, roughly 230–900 px per side, not resized).
- `LICENSE` — license file.

## Example

```csv
id,path,classe,context_tags
78b2ac33-78dd-46c3-a71a-29256ac2049d,images/78b2ac33-78dd-46c3-a71a-29256ac2049d.jpg,knitted,clothing|home_furnishing|fabric
3c7457fa-c4a4-48cc-834d-7c3f12105cf9,images/3c7457fa-c4a4-48cc-834d-7c3f12105cf9.jpg,stained,painting|wallpaper
00ed33c2-330d-4cae-8c93-6951f27fd508,images/00ed33c2-330d-4cae-8c93-6951f27fd508.jpg,waffled,food
```

## Categories

`banded`, `blotchy`, `braided`, `bubbly`, `bumpy`, `chequered`, `cobwebbed`, `cracked`, `crosshatched`, `crystalline`, `dotted`, `fibrous`, `flecked`, `freckled`, `frilly`, `gauzy`, `grid`, `grooved`, `honeycombed`, `interlaced`, `knitted`, `lacelike`, `lined`, `marbled`, `matted`, `meshed`, `paisley`, `perforated`, `pitted`, `pleated`, `polka-dotted`, `porous`, `potholed`, `scaly`, `smeared`, `spiralled`, `sprinkled`, `stained`, `stratified`, `striped`, `studded`, `swirly`, `veined`, `waffled`, `woven`, `wrinkled`, `zigzagged`.

Between 103 and 120 images per category.

## Context tags

`animal`, `clothing`, `concrete`, `fabric`, `food`, `glass`, `hair`, `home_furnishing`, `human`, `ice`, `liquid`, `man_made`, `metal`, `nature`, `painting`, `paper`, `photography`, `plastic`, `rock`, `rubber`, `tree`, `wall`, `wallpaper`, `wood`.

## Source

The images were collected from the internet. The dataset is maintained in this repository.

## License

The images were collected from the internet and remain the property of their respective owners. The dataset is intended for research, education and benchmarking use only. See [`LICENSE`](./LICENSE).

## Known Limitations

- Each image has a single category, although some textures show more than one attribute.
- Some `context_tags` combinations appear mostly with one category (e.g. 58 of the 60 images tagged `nature|liquid` are `bubbly`).
- Images are not resized; resizing and cropping are left to the user.
- The images reflect the content and photographic style of what is commonly published online.

## Intended Use

Texture attribute recognition, multimodal prediction combining images with context tags, and benchmarking image feature extractors on fine-grained visual recognition.
