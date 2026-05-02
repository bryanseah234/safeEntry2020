# PRD: safeEntry2020

## Overview
A Python PIL-based image generator that creates fake Singapore Safe Entry QR check-in passes by overlaying venue names onto a template image. Built in 2020 during COVID-19 when Safe Entry was Singapore's mandatory contact tracing check-in system. Published as a security demonstration to highlight that visual-only passes can be trivially forged.

## Goals
- Accept a list of venue names (hardcoded)
- Overlay each venue name onto a template Safe Entry image using PIL
- Handle both short and long venue names with appropriate font sizing and Y-position
- Save each result as a `.png` file named after the venue

## Non-Goals
- QR code generation (images don't contain functional QR codes)
- Real Safe Entry API integration
- Any form of authentication bypass
- Production deployment

## User Stories
- As a security researcher in 2020, I want to demonstrate that visual Safe Entry passes have no cryptographic integrity verification.
- As a developer, I want to understand PIL's `ImageDraw` API for text overlay on images.

## Tech Stack
- **Language**: Python 3.x
- **Libraries**: `Pillow` (PIL fork) — `Image`, `ImageFont`, `ImageDraw`
- **Assets**: `template.png` (Safe Entry pass template), `block.png` (text measurement canvas), `12.ttf` (font file)

## Architecture
```
safeEntry2020/
├── safeentry.py     # main script
├── template.png     # Safe Entry pass template image
├── block.png        # white image used for text width measurement
└── 12.ttf           # custom font (size 60/56)
```

**Functions:**
- `text_wrap(text, font, max_width)` → list of wrapped lines
- `draw_text(text)` → returns wrapped lines (uses `block.png` for width reference)
- `shortcreate_image(place)` — font size 60, Y offset 760
- `longcreate_image(place)` — font size 56, Y offset 740

**Flow:**
1. For each venue in `longplaces` list, call `longcreate_image(place)`
2. Open `template.png`, draw wrapped venue text centered horizontally
3. Save as `{place_name}.png`

## Features (detailed)

### Text Wrapping
- Splits text by spaces, measures each word via `font.getsize()`
- Accumulates words until line exceeds `max_width`
- Returns list of wrapped line strings

### Image Generation
- Opens `template.png` as base
- Centers each line horizontally: `left = (image.width - text_width) / 2`
- Stacks lines vertically with `line_height` spacing
- Saves as PNG named after venue

### Font Sizing
- Short names: size 60, Y start 760px
- Long names: size 56, Y start 740px
- `shortcreate_image` and `longcreate_image` differ only in these constants

## Data / Config
| Item | Description |
|------|-------------|
| `longplaces` | Hardcoded list of venue names to process |
| `template.png` | Background image — Safe Entry pass template |
| `block.png` | White image used for text measurement |
| `12.ttf` | Font file — must be in same directory |

## Deployment / Run
```bash
pip install Pillow
python safeentry.py
# Outputs: one .png per venue name
```

## Constraints & Notes
- **LEGAL/ETHICAL**: Generating fake Safe Entry passes to bypass Singapore's COVID-19 contact tracing was illegal under the COVID-19 (Temporary Measures) Act. This code is preserved as a historical security demonstration only.
- **No QR codes**: output images are visual only — no functional QR data
- **Hardcoded venues**: add/remove from `longplaces` list directly
- **PIL deprecations**: `font.getsize()` and `image_editable.textsize()` are deprecated in Pillow 10+; replace with `font.getbbox()` for new Pillow versions
