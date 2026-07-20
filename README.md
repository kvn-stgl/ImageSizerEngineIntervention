# ImageSizerEngineIntervention

ProcessWire `ImageSizerEngine` module that uses [Intervention Image v4](https://image.intervention.io/) as
the image manipulation library, with a selectable backend driver: **GD**, **Imagick**, or **libvips**.

## Features

- Drop-in `ImageSizerEngine` — works with the normal `$page->image->size()` API, no template changes needed.
- Selectable driver per installation: GD (always available), Imagick, or libvips (via FFI).
- Extended source/target format support when using Imagick or libvips: AVIF, TIFF, HEIC, HEIF (in addition
  to JPG, PNG, GIF, WEBP).
- Auto-orientation (EXIF), rotate, flip, crop (including focus-zoom cropping), sharpening.
- Optional WebP sibling generation (`webpAdd` / `webpOnly`), matching core `ImageSizerEngine` options.
- Greyscale and sepia conversion.
- Optional temporary `memory_limit` increase during resize operations (all images, or animated images only).
- Optional debug logging of resize operations to `Setup > Logs > intervention-image`.

## Requirements

- PHP >= 8.3
- GD extension (used as the default/fallback driver)
- Optional: `imagick` PHP extension for the Imagick driver
- Optional: `ffi` extension (with `ffi.enable` set to `true`) and libvips installed on the system, for the
  libvips driver

## Installation

1. Make sure this directory is at `site/modules/ImageSizerEngineIntervention`.
2. Install PHP dependencies:
   ```bash
   ddev composer install
   ```
   This installs `intervention/image` and `intervention/image-driver-vips` into the module's own `vendor/`
   directory (not the site-wide vendor folder). The `vendor/` folder is git-ignored; `composer.lock` is
   committed so installs are reproducible.
3. In the ProcessWire admin, go to **Modules > Refresh**, then install **Intervention Image Sizer**
   (`ImageSizerEngineIntervention`).
4. Configure the module (driver selection, memory limit, debug logging) under its module settings page.

## Configuration

Available in the module's config screen (`Modules > Configure > ImageSizerEngineIntervention`):

| Setting | Description |
| --- | --- |
| **Intervention Image Driver** | `gd`, `imagick`, or `vips`. Only drivers detected as available are offered for Imagick/libvips. |
| **Extension Status** | Read-only overview of GD/Imagick/libvips availability, FFI status, and current PHP `memory_limit`. |
| **Memory Limit for Image Processing** | Temporarily raises `memory_limit` during resize operations. Leave empty to keep the current limit. |
| **Apply memory limit only for animated images** | Restricts the memory limit override to animated sources (e.g. animated GIF/WebP). |
| **Enable Debug Logging** | Logs resize steps and errors to `Setup > Logs > intervention-image`. |
| **Engine priority / Sharpening / Quality** | Standard `ImageSizerEngine` options (inherited from ProcessWire core). |

If multiple `ImageSizerEngine` modules are installed, use **Engine priority** to control which one
ProcessWire prefers.

## Notes on drivers

- **GD** is always available and requires no extra setup.
- **Imagick** requires the PHP `imagick` extension. If it's not installed, the option won't appear in the
  driver dropdown.
- **libvips** requires the `ffi` PHP extension with `ffi.enable` set to `true` (not just `preload`), plus
  libvips installed on the host/container. Status for both is shown in the module config screen.

## License

MIT