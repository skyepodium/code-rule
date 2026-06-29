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

## Fonts

- Before adding font files, check the license and whether subsetting is needed.
- Document font family names and weight mapping.
