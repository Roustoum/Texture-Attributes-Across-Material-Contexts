# Texture Attributes Across Material Contexts

A cleaned and anonymized dataset of 5,553 real-world texture photographs labeled with one of 47 human-describable texture attributes (*banded*, *cracked*, *honeycombed*, *marbled*, *zigzagged*, ...), with per-image context tags describing the material or object the texture appears on.

## Overview

The task is to predict the texture class (`classe`) of each image among **47 categories**.

The images are photographs collected "in the wild": the same attribute can appear on very different materials (a *striped* shirt, a *striped* zebra, a *striped* wall), and very different-looking surfaces can share the same attribute. Each image also comes with `context_tags` (e.g. `fabric`, `food`, `rock`, `home_furnishing`) describing the material, object or scene on which the texture appears.

## Files

- `data.csv` — one row per image:
  - `id`: String. Random UUID of the image (carries no class information).
  - `path`: String. Relative path to the image, `images/<id>.jpg`.
  - `classe`: String. Texture category, one of 47 classes. **Target.**
  - `context_tags`: String. 1–4 tags separated by `|`, from a vocabulary of 24 tags.
- `LICENSE` — license terms (images: research use only; modifications: CC BY 4.0).
- `images/` — 5,553 JPEG files (RGB, variable resolution, roughly 230–900 px per side, not resized).

## Example

```csv
id,path,classe,context_tags
78b2ac33-78dd-46c3-a71a-29256ac2049d,images/78b2ac33-78dd-46c3-a71a-29256ac2049d.jpg,knitted,clothing|home_furnishing|fabric
3c7457fa-c4a4-48cc-834d-7c3f12105cf9,images/3c7457fa-c4a4-48cc-834d-7c3f12105cf9.jpg,stained,painting|wallpaper
00ed33c2-330d-4cae-8c93-6951f27fd508,images/00ed33c2-330d-4cae-8c93-6951f27fd508.jpg,waffled,food
```

## Classes

`banded`, `blotchy`, `braided`, `bubbly`, `bumpy`, `chequered`, `cobwebbed`, `cracked`, `crosshatched`, `crystalline`, `dotted`, `fibrous`, `flecked`, `freckled`, `frilly`, `gauzy`, `grid`, `grooved`, `honeycombed`, `interlaced`, `knitted`, `lacelike`, `lined`, `marbled`, `matted`, `meshed`, `paisley`, `perforated`, `pitted`, `pleated`, `polka-dotted`, `porous`, `potholed`, `scaly`, `smeared`, `spiralled`, `sprinkled`, `stained`, `stratified`, `striped`, `studded`, `swirly`, `veined`, `waffled`, `woven`, `wrinkled`, `zigzagged`.

Between 103 and 120 images per class.

## Context tags

`animal`, `clothing`, `concrete`, `fabric`, `food`, `glass`, `hair`, `home_furnishing`, `human`, `ice`, `liquid`, `man_made`, `metal`, `nature`, `painting`, `paper`, `photography`, `plastic`, `rock`, `rubber`, `tree`, `wall`, `wallpaper`, `wood`.

## Source

This dataset was prepared by the author from publicly available photographs collected from the internet. It is maintained in this repository, and its commit history documents how it has been cleaned and revised over time.

## Processing

Compared with the raw collection (5,640 images), this version:

1. **Removes duplicates.** All images were compared using an exact hash (MD5), a perceptual hash (pHash) and a color signature. Candidate groups were reviewed manually, and 87 duplicate / near-duplicate images were removed, including one identical image that was labeled both `grid` and `meshed`.
2. **Repairs the annotation file.** One missing row was restored, one row that had been merged into its neighbor by an unclosed quote was split, and stray quote characters were removed from `context_tags`.
3. **Strips metadata.** EXIF, GPS, camera, author/copyright, XMP, Photoshop and comment blocks were removed losslessly (the compressed image data is copied unchanged, so the pixels are identical to the source).
4. **Anonymizes file names.** Images are renamed with random UUIDs and rows are shuffled, so neither file names nor row order reveal the class.

## License

The images are made available for research purposes. They were originally collected from the internet and remain the property of their respective owners. This repository is intended for research, education and benchmarking use only.

The changes made in this repository (duplicate removal, annotation repair, anonymization, scripts and documentation) are released under the **Creative Commons Attribution 4.0 International (CC BY 4.0)** license. This does not extend to the images themselves. See [`LICENSE`](./LICENSE) for the full terms.

## Known Limitations

- **Single label per image.** Many textures show several attributes at once; only the main one is given.
- **Context tags correlate with the class.** Some tag combinations appear almost exclusively with one class (e.g. 58 of the 60 images tagged `nature|liquid` are `bubbly`), which models can use as a shortcut.
- **Variable image size.** Images are not resized; resizing and cropping are left to the user.
- **Web-collection bias.** The images reflect the content and photographic style of what is commonly published online.
- **Near-duplicate removal is not exhaustive.** Heavily edited or cropped copies of the same photograph may remain.

## Intended Use

Texture attribute recognition, multimodal prediction combining images with material/object context tags, benchmarking image feature extractors on fine-grained attribute recognition, and studying how well models separate a visual attribute from the object or material it appears on.
