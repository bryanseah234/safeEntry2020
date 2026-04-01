# SafeEntry Pass Generator

A Python tool that generates SafeEntry check-in pass images for Singapore locations.

## Description

This project creates SafeEntry pass images by overlaying location names onto a template image. SafeEntry was Singapore's national digital check-in system used during the COVID-19 pandemic for contact tracing purposes. The script uses the Pillow library to handle image manipulation and text rendering, with automatic text wrapping for long location names.

## Features

- Generates SafeEntry pass images with custom location names
- Automatic text wrapping for long location names
- Supports both short and long text layouts
- Outputs high-quality PNG images

## Technologies Used

- Python 3
- Pillow (PIL) - Python Imaging Library for image processing
- TrueType Font rendering

## Installation

```bash
# Clone the repository
git clone https://github.com/bryanseah234/safeEntry2020.git

# Navigate to project directory
cd safeEntry2020

# Install dependencies
pip install Pillow
```

## Usage

```bash
# Run the script to generate SafeEntry images
python safeentry.py
```

To customize the locations, edit the `longplaces` list in `safeentry.py` with your desired location names. The script will generate a PNG image for each location.

## Demo

After running the script, PNG images will be generated in the project directory with the location name as the filename.

## Disclaimer

1. FOR EDUCATIONAL PURPOSES ONLY
2. USE AT YOUR OWN DISCRETION

## License

MIT License

---

**Author:** <a href="https://github.com/bryanseah234">bryanseah234</a>
