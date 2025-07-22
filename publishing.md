# Documentation Publishing Workflow

To maintain high-quality and accessible documentation, Fabric uses an automated GitBook-compatible publishing process. This guide outlines how to structure, build, and deploy the documentation from the `fabric-users-manual` repository.

---

## 📁 Directory Structure

Ensure your manual adheres to this layout:

fabric-users-manual/
├── README.md
├── SUMMARY.md
├── getting-started/
├── system-architecture/
├── ...



---

## 🧰 Tooling

- **[GitBook CLI](https://github.com/GitbookIO/gitbook-cli)** – Legacy support for local builds.
- **Markdown files** – Authored manually, parsed with GitBook-compatible renderers.
- **Custom CI** – GitHub Actions or Netlify for continuous deployment.

---

## 🏗️ Build Locally (Optional)

Install GitBook CLI if building locally:

```bash
npm install -g gitbook-cli
gitbook install
gitbook build
Preview via:

bash

gitbook serve
🚀 Publish to GitHub Pages (via GitHub Actions)
.github/workflows/publish-docs.yml
yaml
Copy
Edit
name: Publish Documentation

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Build Docs
        run: |
          npm install -g gitbook-cli
          gitbook install
          gitbook build
      - name: Deploy to GitHub Pages
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./_book
📦 Netlify/Surge/Custom Hosting
You may also deploy the _book/ output to:

Netlify

Surge

Any S3/Cloudflare Bucket

🔁 Publishing Checklist
 SUMMARY.md is synced with folder structure.

 All internal links resolve correctly.

 GLOSSARY.md, CHANGELOG.md are updated.

 All Markdown files pass linting (docs-ci/linting.md).

 CI passes on GitHub.

Consistent publishing workflows keep your docs usable and authoritative for all developers.
