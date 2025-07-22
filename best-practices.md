# ♿ Accessibility Best Practices

Fabric is committed to building inclusive and accessible AI tooling and documentation. This guide outlines accessibility best practices for all Fabric interfaces, documentation, and developer tools.

---

## 🌈 Visual Accessibility

### ✅ Color Contrast
- Ensure a contrast ratio of at least 4.5:1 for text and interactive elements.
- Use [WebAIM Contrast Checker](https://webaim.org/resources/contrastchecker/) to validate.

### 🔍 Zoom & Scale
- All interfaces should support browser zoom up to 200% without loss of functionality or readability.

### 🚫 Avoid Sole Reliance on Color
- Never use color as the only means to convey information.
- Pair colors with text, icons, or patterns.

---

## 🧭 Navigation & Structure

### ⌨️ Keyboard Navigation
- Ensure all functionality is accessible via keyboard:
  - Use `Tab`, `Shift+Tab`, `Enter`, `Esc`, and arrow keys logically.
  - Implement visible focus states.

### 🧱 Logical Headings
- Use semantic HTML (`<h1>` to `<h6>`) in a nested, meaningful order.
- Avoid skipping levels (e.g., jumping from `<h2>` to `<h4>`).

---

## 🔊 Screen Reader Support

### 🎙️ ARIA Roles
- Use ARIA landmarks and roles where native HTML lacks semantics:
  - `role="banner"`, `role="main"`, `role="navigation"`, etc.

### 🎧 Descriptive Labels
- Ensure all buttons, links, and inputs have meaningful accessible names via `aria-label`, `aria-labelledby`, or `<label>` tags.

---

## 📃 Documentation-Specific Guidance

- Use plain language with minimal jargon.
- Ensure alt text for all diagrams and screenshots.
- Avoid ASCII art or diagrams without text alternatives.
- Use descriptive link texts ("Read more about governance", not "click here").

---

## ✅ Testing Tools

- [axe DevTools](https://www.deque.com/axe/devtools/)
- [WAVE Evaluation Tool](https://wave.webaim.org/)
- Chrome DevTools Accessibility Tab
- `aria-live` and `VoiceOver` for real-time feedback

---

## 🌐 Inclusive Language

- Avoid gendered language unless contextually necessary.
- Prefer neutral phrasing: "they/them", "users", "engineer", "team", etc.

---

## 🛠 Contributor Reminders

- Test accessibility for any UI or doc changes.
- Raise accessibility issues in PR reviews.
- Make accessibility everyone's responsibility.

---

Let’s make Fabric usable by **everyone**. Inclusion is innovation.
