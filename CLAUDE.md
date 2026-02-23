# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Jupyter Book** for the course "Avenidas Torrenciales" (Torrential Flows/Debris Flows) taught at Universidad Nacional de Colombia sede Medellín. The book covers the science of debris flows, including hydrology, rheology, numerical modeling tools, and risk assessment — written in Spanish.

## Build Commands

```bash
# Install dependencies
pip install -r requirements.txt

# Build the HTML book
jupyter-book build .

# Build a PDF (requires LaTeX)
jupyter-book build . --builder pdflatex

# Clean the build cache
jupyter-book clean .
```

The built HTML output is in `_build/html/`. Open `_build/html/index.html` to preview locally.

## Book Structure

The book uses **MyST Markdown** (`.md` files) as its source format. The table of contents is defined in [_toc.yml](_toc.yml) and book settings (title, author, bibtex, execute config) are in [_config.yml](_config.yml).

Chapter files are numbered by topic area:
- `01_*` — Introduction
- `02_*` — Fundamentals (flows, climate change, dating, interactions)
- `03_*` — Governing equations
- `04_*` — Rheology
- `05_*` — Two-phase flows
- `07_*` to `16_*` — Numerical modeling tools (Routing, Flow-R, OpenLISEM, r.randomwalk, Predictor, FlowPy, GMP, r.avaflow, Grfin, Iber/NNF)
- `20_*` — Risk assessment

To add a new chapter, create a `.md` file and add its filename (without extension) to the `chapters:` list in [_toc.yml](_toc.yml).

## Citations

References are managed via [references.bib](references.bib) (BibTeX). In-text citations use MyST syntax: `` {cite}`AuthorYear` ``. The bibliography is rendered by the `bibtex_bibfiles` setting in `_config.yml`.

## Content Conventions

- Each chapter begins with an HTML `<p>` credits line attributing sources.
- Math equations use standard LaTeX inline (`$...$`) and display (`$$...$$`) syntax, rendered via MathJax.
- Figures use MyST `{figure}` directives.
- The book language is Spanish; all chapter content and headings should be in Spanish.

## Notebook Execution

`_config.yml` sets `execute_notebooks: force`, meaning any `.ipynb` or MyST notebook with executable code cells will be re-run on every build. If a chapter contains computational examples (matplotlib/numpy plots), ensure the Python environment from `requirements.txt` is active before building.
