# PhotoPainter Image Converter

A lightweight Python command-line tool for converting images into the **7-color BMP format** used by the [Waveshare PhotoPainter](https://www.waveshare.com/wiki/PhotoPainter).

The tool automatically resizes images to the PhotoPainter display resolution, converts them to its supported color palette, and optionally applies dithering to improve the appearance of photographs.

Designed to run on **Linux**, but compatible with other operating systems that support Python and Pillow.

## Features

- **Automatic orientation detection** – Detects landscape or portrait orientation based on the input image dimensions.
- **Manual orientation selection** – Force landscape (800 × 480) or portrait (480 × 800).
- **Image scaling** – Resize images to fit the display dimensions.
- **Image fitting** – Fit images to the display using Pillow's padding functionality.
- **7-color palette conversion** – Converts images to the PhotoPainter's seven supported colors:
  - Black
  - White
  - Green
  - Blue
  - Red
  - Yellow
  - Orange
- **Dithering support** – Supports Floyd-Steinberg dithering or no dithering.
- **BMP output** – Saves the converted image as a BMP file.

## Requirements

- Python 3
- Pillow (Python Imaging Library)

## Installation

### Linux (Ubuntu / Debian / Raspberry Pi OS)

Install Python and Pillow:

```bash
sudo apt update
sudo apt install python3 python3-pil
```

Alternatively, install Pillow using pip:

```bash
python3 -m pip install Pillow
```

### Download the script

Save the Python script as:

```text
photopainter.py
```

## Usage

Run the converter from your terminal:

```bash
python3 photopainter.py IMAGE_FILE [OPTIONS]
```

### Arguments

| Argument | Description | Default |
|---|---|---|
| `image_file` | Input image file | Required |
| `--dir` | Display orientation: `landscape` or `portrait` | Automatic |
| `--mode` | Image conversion mode: `scale` or `cut` | `scale` |
| `--dither` | Dithering algorithm: `0` or `3` | `3` |

### Display orientation

The display orientation can be specified manually or detected automatically.

**Landscape (800 × 480):**

```bash
python3 photopainter.py photo.jpg --dir landscape
```

**Portrait (480 × 800):**

```bash
python3 photopainter.py photo.jpg --dir portrait
```

**Automatic orientation:**

```bash
python3 photopainter.py photo.jpg
```

When no orientation is specified, the tool selects landscape for images wider than they are tall and portrait for all other images.

### Image conversion modes

Two conversion modes are available.

**Scale (default)**

```bash
python3 photopainter.py photo.jpg --mode scale
```

Resizes the image proportionally to cover the complete display dimensions and centers it on a white background.

**Cut**

```bash
python3 photopainter.py photo.jpg --mode cut
```

Fits the image to the target display dimensions using Pillow's `ImageOps.pad` functionality, preserving the complete image and its aspect ratio.

### Dithering

Dithering helps simulate additional shades and details using the limited seven-color palette.

**Floyd-Steinberg dithering (default):**

```bash
python3 photopainter.py photo.jpg --dither 3
```

**No dithering:**

```bash
python3 photopainter.py photo.jpg --dither 0
```

## Examples

Convert an image to landscape using the default settings:

```bash
python3 photopainter.py holiday.jpg
```

Convert an image to portrait with dithering:

```bash
python3 photopainter.py holiday.jpg --dir portrait --dither 3
```

Convert an image to landscape without dithering:

```bash
python3 photopainter.py holiday.jpg --dir landscape --mode scale --dither 0
```

Convert an image using the cut mode:

```bash
python3 photopainter.py holiday.jpg --mode cut
```

## Output

The converted image is saved in the same directory as the original image.

The output filename follows this convention:

```text
INPUT_FILENAME_MODE_output.bmp
```

For example:

```text
holiday.jpg
holiday_scale_output.bmp
```

The generated BMP image has one of the following resolutions:

| Orientation | Resolution |
|---|---|
| Landscape | 800 × 480 |
| Portrait | 480 × 800 |

## Supported Color Palette

The converter uses a fixed seven-color palette:

| Color | RGB Value |
|---|---|
| Black | `(0, 0, 0)` |
| White | `(255, 255, 255)` |
| Green | `(0, 255, 0)` |
| Blue | `(0, 0, 255)` |
| Red | `(255, 0, 0)` |
| Yellow | `(255, 255, 0)` |
| Orange | `(255, 128, 0)` |

## Notes

- The converter always produces an RGB BMP output.
- The input image is not modified.
- The conversion uses a fixed seven-color palette.
- Floyd-Steinberg dithering is recommended for photographs.
- Results may vary depending on the original image, its colors and contrast.
- The output resolution is fixed according to the selected orientation.

## License

This project is provided as an open-source utility. Add your preferred license (for example, MIT) if you intend to distribute it.

## Credits

- Original PhotoPainter project and hardware: [Waveshare](https://www.waveshare.com/)
- Image processing: [Pillow](https://python-pillow.org/)
