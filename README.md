# Quarto FH-SWF Theme

A Quarto theme implementing the **FH Südwestfalen (FH-SWF) Corporate Design** guidelines for academic documents and presentations.

## Overview

This theme provides consistent branding for FH-SWF using Quarto's `_brand.yml` system, supporting:

- **RevealJS presentations** with custom title slides and branded styling
- **HTML documents** with FH-SWF colors, typography, and design elements
- **Cross-format consistency** through a single `_brand.yml` configuration

## Installation

### Method 1: Direct Copy (Recommended)

1. Copy the entire `Quarto-FH-SWF-Theme/` directory to your project
2. Ensure all files are preserved (especially `_brand.yml`)
3. Reference the theme in your `_quarto.yml` or document frontmatter

### Method 2: GitHub Repository (Future)

```bash
# Coming soon: Install as a Quarto extension
quarto add fh-swf/quarto-fhswf-theme
```

## Usage

### Basic Setup

Add to your project's `_quarto.yml`:

```yaml
project:
  type: default
  output-dir: _site

brand: _brand.yml

format:
  html:
    theme: [brand, fhswf-html.scss]
    toc: true
  
  revealjs:
    theme: [brand, fhswf-revealjs.scss]
    slide-number: true
```

### Individual Documents

Add to document frontmatter:

```yaml
---
title: "My Presentation"
author: "Your Name"
format:
  revealjs:
    theme: [brand, fhswf-revealjs.scss]
---
```

```yaml
---
title: "My Document"
format:
  html:
    theme: [brand, fhswf-html.scss]
---
```

## Features

### Colors

- **Primary Blue**: `#39569F` (CMYK 100/70/0/0 | RAL 5005)
- **7 Secondary Colors**: Each with specific roles (Bachelor/Master, dual programs)
- **Semantic Color Mapping**: Bootstrap-compatible names (`primary`, `success`, `warning`, etc.)

### Typography

- **Sans-serif**: Lato (replaces Arial from CD guidelines)
- **Serif**: Source Serif 4 (replaces Fedra Serif B)
- **Monospace**: JetBrains Mono for code
- **German quotation marks**: `»...«` formatting

### Logo Support

- Multiple sizes (`small`, `medium`, `large`)
- Light/dark variants for different backgrounds
- Placeholder included - add official FH-SWF logos to `assets/logos/`

### Design Elements

- **Rounded corners**: 9px radius (9mm at A4, ratio 1:3)
- **Blue header bars**: Consistent heading styling
- **Color-coded callouts**: For different content types
- **German claim**: "Wir geben Impulse" styling

## Examples

See the `examples/` directory:

- `slides.qmd` - RevealJS presentation example
- `document.qmd` - HTML document example

## File Structure

```
Quarto-FH-SWF-Theme/
├── _brand.yml               # Core brand configuration
├── _quarto.yml              # Project configuration
├── styles/                  # SCSS theme files
│   ├── _variables.scss      # Shared variables
│   ├── fhswf-revealjs.scss  # RevealJS theme
│   └── fhswf-html.scss      # HTML theme
├── templates/               # Template partials
│   └── title-slide.html     # Custom RevealJS title slide
├── assets/logos/            # Logo files (placeholders included)
├── examples/                # Example documents
│   ├── slides.qmd          # Presentation example
│   └── document.qmd        # Document example
└── README.md               # This file
```

## Customization

### Colors

Edit `_brand.yml` to adjust colors. The file includes:

```yaml
color:
  palette:
    blau: "#39569F"
    rot: "#CC0000"
    # ... more colors
  primary: blau
  success: gruen
  # ... semantic mappings
```

### Typography

```yaml
typography:
  fonts:
    - family: Lato
      source: google
      weight: [300, 400, 500, 600, 700]
  base: Lato
  headings: Lato
```

### SCSS Customization

Create additional SCSS files and layer them:

```yaml
format:
  html:
    theme: [brand, fhswf-html.scss, custom.scss]
```

## Development

### Requirements

- Quarto 1.6+ (for `_brand.yml` support)
- Git (for version control)

### Building Examples

```bash
# Build presentation example
quarto render examples/slides.qmd

# Build document example  
quarto render examples/document.qmd

# Preview with live reload
quarto preview examples/slides.qmd
```

## License

This theme is provided under the MIT License. Note that FH-SWF logos and branding elements are property of Fachhochschule Südwestfalen and must be used in accordance with their guidelines.

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make changes and test with examples
4. Submit a pull request

## Acknowledgments

- Based on the FH-SWF Corporate Design Handbook (August 2014)
- Uses open-source fonts (Lato, Source Serif 4, JetBrains Mono)
- Built with Quarto's modern theming system

## Support

For issues and questions:
- Create an issue on GitHub
- Contact: [cd-support@fh-swf.de](mailto:cd-support@fh-swf.de)

---

**Fachhochschule Südwestfalen** • University of Applied Sciences • [www.fh-swf.de](https://www.fh-swf.de)