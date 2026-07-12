# Asset Rules

This directory defines rules for managing images, icons, fonts, and app assets.

## Files

- Asset filenames must use English and kebab-case.
- Split assets by feature, brand, or platform, and do not put everything in an arbitrary `images/` folder.
- Distinguish originals from generated assets.
- Before adding large binary assets, check their size and usage.

## Images and Icons

- Prefer the existing icon system or library.
- Do not add duplicate icons for the same meaning.
- Match image size, density, and format to platform requirements.
- Distinguish decorative images from content images and handle accessibility accordingly.
- Define one human-edited source of truth for each generated asset family. Generated PNGs, iconsets, sprite sheets, thumbnails, and installed-bundle copies must never become inputs to the next generation pass.
- Keep generation one-way and reproducible: original source -> canonical generated asset -> platform representations -> packaged artifact. Do not rebuild from screenshots, OS caches, installed bundles, or previously downscaled outputs.
- Record the canonical output contract when exact dimensions, alpha, crop bounds, density, padding, or platform representation ladders matter.
- Verification should compare expected copies by hash and inspect structural properties such as dimensions, alpha, metadata references, and required platform representations before packaging reports success.

## Fonts

- Before adding font files, check the license and whether subsetting is needed.
- Document font family names and weight mapping.
