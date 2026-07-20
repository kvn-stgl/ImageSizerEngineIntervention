# Changelog

All notable changes to this module are documented in this file.

## [10] - 2026-07-20

### Added

- `___install()` hook that throws a `WireException` on install if the GD extension (used as the default
  driver) is not available.
- `.gitignore` for the module's own `vendor/` directory (installed via the module's `composer.json`,
  reproducible via `composer.lock`).
- `README.md` documenting features, requirements, installation, and configuration.

### Features (since initial version)

- `ImageSizerEngine` implementation backed by Intervention Image v4.
- Selectable driver: GD, Imagick, or libvips, configurable in the module settings.
- Extended format support (AVIF, TIFF, HEIC, HEIF) when using Imagick or libvips.
- Auto-orientation, rotate, flip, cropping (including focus-zoom crop), sharpening.
- Optional WebP sibling generation (`webpAdd` / `webpOnly`).
- Greyscale and sepia conversion (`convertToGreyscale()`, `convertToSepia()`).
- Optional temporary `memory_limit` increase during resize, with an "animated images only" toggle.
- Optional debug logging to `Setup > Logs > intervention-image`.
- Module config screen showing GD/Imagick/libvips availability, FFI status, and current `memory_limit`.

## [1] - Initial version

- Initial implementation of the module.
