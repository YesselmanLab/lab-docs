<div align="center">

# 📚 Lab Documentation

## [👉 View Full Documentation Site 👈](https://yesselmanlab.github.io/lab-docs/)

**This repository contains the source files for the documentation.**

**The actual documentation site is hosted at: [yesselmanlab.github.io/lab-docs](https://yesselmanlab.github.io/lab-docs/)**

---

</div>

This repository contains comprehensive documentation for the lab, built with [MkDocs](https://www.mkdocs.org/) and the [Material theme](https://squidfunk.github.io/mkdocs-material/).

## Setup

### Prerequisites

- Python 3.8 or higher
- pip

### Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/lab-docs.git
cd lab-docs
```

2. Create a virtual environment (recommended):
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
pip install -r requirements.txt
```

## Development

### Preview Locally

To preview the documentation locally:

```bash
mkdocs serve
```

Then open [http://127.0.0.1:8000](http://127.0.0.1:8000) in your browser.

### Build

To build the static site:

```bash
mkdocs build
```

The site will be generated in the `site/` directory.

## Deployment

### GitHub Pages (Automatic)

This repository is configured to automatically deploy to GitHub Pages using GitHub Actions. Simply push to the `main` branch, and the site will be built and deployed automatically.

### Manual Deployment

If you prefer to deploy manually:

1. Build the site:
```bash
mkdocs build
```

2. Deploy to GitHub Pages:
```bash
mkdocs gh-deploy
```

## Configuration

Edit `mkdocs.yml` to customize:
- Site name and description
- Navigation structure
- Theme settings
- Plugins and extensions

## Documentation Structure

- `docs/` - All documentation source files (Markdown)
- `mkdocs.yml` - MkDocs configuration
- `.github/workflows/` - GitHub Actions workflows

## Contributing

1. Create a new branch for your changes
2. Make your edits in the `docs/` directory
3. Preview locally with `mkdocs serve`
4. Commit and push your changes
5. Create a pull request

## License

[Add your license here]

