# ✒️ Fabric Documentation Style Guide

This style guide ensures that all contributions to the Fabric Users Manual remain consistent, readable, and professional.

---

## 🧱 File Format & Naming

- Use `.md` (Markdown) format.
- File and folder names should be `kebab-case`, e.g. `first-model.md`.
- Each page should begin with a top-level heading (`#`).

---

## 🪄 Formatting Best Practices

### ✅ Use:

- `#`, `##`, `###` for logical heading levels
- Lists (`-` or `*`) for enumerations
- Code blocks with triple backticks for examples
- Inline code using backticks (`) for commands or code snippets
- Bold `**text**` and _italic_ formatting for emphasis
- Horizontal rules (`---`) to separate major sections

### ❌ Avoid:

- Excessive nested lists
- Writing in uppercase
- Including screenshots without ALT text or captions

---

## 🧑‍💻 Code Style

- Prefer fenced code blocks:
  ```bash
  fab init my-project
Specify language in code blocks (e.g., bash, json, yaml):

yaml

framework: ONNX
input_schema:
  type: object
Do not embed sensitive keys or secrets

🔤 Terminology and Voice
Use consistent terminology: "agent", "block", "workflow", "UDAP", etc.

Use second person voice (“you should...”) for instructions.

Avoid jargon unless defined in the GLOSSARY.md.

📍 Placeholders
Use <placeholder> format for variables:

bash

fab model publish models/<model-name>/<version>/model.yaml
Document placeholder meaning in context.

📦 Frontmatter (optional)
Use frontmatter in pages that require metadata:

yaml

---
title: "Training a Model"
description: "How to train a model in Fabric using local or distributed runtimes."
tags: [training, model-lifecycle]
---
📘 Page Length & Clarity
Aim for 1–2 screen lengths per page.

Break long paragraphs into smaller blocks.

Use diagrams and flowcharts where helpful (via relative paths or links).

📝 Example Layout
markdown

# Deploying to Edge Devices

This guide shows how to deploy a Fabric model to ARM-based edge hardware.

## Prerequisites

- Docker
- Fabric CLI

## Step 1: Build the Container

```bash
fab package model.yaml --target edge
Step 2: Run
bash
Copy
Edit
docker run agent-container


---

By following these practices, we ensure all documentation in the Fabric ecosystem is accessible, robust, and user-friendly.

