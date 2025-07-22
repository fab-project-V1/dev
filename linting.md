# Documentation Linting & Validation Guide

Maintaining a high-quality user manual requires automated linting and validation of Markdown files. This document outlines the setup and use of linting tools to catch common issues early and enforce consistent standards.

---

## ✅ Tools Used

- **[markdownlint](https://github.com/DavidAnson/markdownlint)** – Lints Markdown files for style violations.
- **[markdown-link-check](https://github.com/tcort/markdown-link-check)** – Checks for broken links in documentation.
- **[cspell](https://github.com/streetsidesoftware/cspell)** – Spell checker for source and Markdown files.

---

## 📦 Installation

Use `npm` to install the tools:

```bash
npm install --save-dev markdownlint-cli markdown-link-check cspell
⚙️ Configuration
.markdownlint.json
json

{
  "default": true,
  "MD013": false, // Disable line length
  "MD033": false  // Allow inline HTML
}
.cspell.json
json

{
  "version": "0.2",
  "language": "en",
  "words": ["FabricDSL", "UDAP", "quantization", "K8s"],
  "ignorePaths": ["node_modules", "CHANGELOG.md"]
}
📁 Running Linters
Markdown Lint
bash

npx markdownlint "**/*.md"
Link Checker
bash

npx markdown-link-check ./README.md
Spell Checker
bash

npx cspell "**/*.md"
✅ GitHub CI Integration
In .github/workflows/docs-ci.yml:

yaml

name: Docs CI

on:
  pull_request:
    paths:
      - "**/*.md"

jobs:
  lint:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm install
      - run: npx markdownlint "**/*.md"
      - run: npx markdown-link-check README.md
      - run: npx cspell "**/*.md"
💡 Tips
Run linters locally before pushing.

Extend dictionaries as new terms appear.

Disable specific rules locally using HTML-style comments.

Keep documentation pristine to ensure user trust and accessibility.
