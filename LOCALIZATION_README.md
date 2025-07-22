# 🌍 Localization Guide for Fabric Users Manual

## Overview

This directory defines how Fabric documentation will be translated into other languages. Our goal is to make Fabric accessible to developers and stakeholders globally by enabling high-quality community-driven translations.

---

## 🌐 Supported Languages (Planned)

- English (default)
- Spanish
- Chinese (Simplified)
- German
- Portuguese
- Japanese

---

## 🧭 Structure

Translated content mirrors the main `fabric-users-manual/` structure:

localization/
├── es/ # Spanish
│ ├── getting-started/
│ ├── fabric-language/
│ └── ...
├── zh/
├── de/
├── pt/
└── ja/

yaml
Copy
Edit

Each language folder should contain a full copy of the documentation tree, translated into the target language.

---

## 🔧 Translation Workflow

1. Fork the repo.
2. Create a branch named `translate-<lang>-<section>`.
3. Translate files faithfully and annotate unclear content with `<!-- TODO: Clarify meaning -->`.
4. Submit a PR with the `[Translation]` tag and reference source commit hash.
5. Each translation must be reviewed by a native speaker contributor.

---

## 🧰 Tooling

- Optional tools:
  - [Poedit](https://poedit.net/)
  - [Crowdin CLI](https://support.crowdin.com/cli-tool/)
  - GitBook’s i18n plugin (coming soon)

---

## 📏 Style

- Follow the original structure.
- Preserve code blocks and inline code snippets.
- Update internal links to reflect language subpaths.

---

## 🤝 Join the Localization Team

Interested in translating Fabric into your language? Submit a PR or contact the maintainers via GitHub Discussions or Matrix.

---

✍️ Let’s make AI infrastructure accessible to all—one language at a time!
