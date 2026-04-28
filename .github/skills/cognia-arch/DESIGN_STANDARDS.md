# System Design HTML Standard

This file is fully self-contained and is the canonical source of theme, format, colors, fonts, and content structure.

> ⚠️ **CRITICAL FILE RULE**: Always **overwrite** `{project_name}-architecture.html` completely — NEVER append to it.
> If the file already exists, replace its entire contents. Two complete HTML documents in one file will break rendering.


## 1) Document Identity

- `<html lang="en">`
- `<meta charset="UTF-8" />`
- `<meta name="viewport" content="width=device-width, initial-scale=1.0" />`
- Title pattern: `<title>[Project Short Name] New System Design</title>`

## 2) Required Visual Theme Tokens (Do Not Change)

Use these exact CSS variables:

```css
:root {
  --primary: #0a2540;
  --secondary: #1a56db;
  --accent: #f59e0b;
  --green: #10b981;
  --red: #ef4444;
  --bg: #f8fafc;
  --card-bg: #ffffff;
  --text: #1e293b;
  --border: #e2e8f0;
  --code-bg: #f1f5f9;
}
```

## 3) Typography Standard (Do Not Change)

- Base body font stack:
  - `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif`
- Code font:
  - `'Consolas', monospace`
- Body line-height: `1.65`
- Header title:
  - `font-size: 2.2rem`
  - `font-weight: 800`
  - `letter-spacing: -0.5px`

## 4) Page Layout Standard

- `main` max width: `1440px`
- Main padding: `36px 48px`
- Header padding: `36px 48px`
- Sticky nav at top:
  - `position: sticky; top: 0; z-index: 100;`

## 5) Header + Navigation Standard

### Header
- Gradient background:
  - `linear-gradient(135deg, var(--primary), #1e3a5f, var(--secondary))`
- Bottom border: `4px solid var(--accent)`
- Include:
  1. Main H1 with emoji + product name + “New System Design”
  2. Subtitle sentence
  3. Tech badge row (`.badge-stack` + `.tech-badge`)

### Nav
- Background: `var(--primary)`
- Link color default: `#94a3b8`
- Hover: background `var(--secondary)`, text `white`

## 6) Section & Title Hierarchy

- Section wrapper: `<div class="section" id="...">`
- Section title: `<h2>`
  - `font-size: 1.6rem`
  - left accent bar: `border-left: 5px solid var(--accent)`
- Subsection title: `<h3>`
  - `font-size: 1.1rem`
  - color: `var(--secondary)`

## 7) Content Blocks

### Card
Use `.card` for standard textual/technical content.

### Diagram Card
Use `.diagram-wrap` + `.diagram-title` + `.mermaid` for Mermaid diagrams.

### Table
- Header background: `var(--primary)`
- Zebra rows and hover states must remain enabled.

### Highlight Box
Use `.highlight-box` for key design notes or decisions.

### Rule Card
Use `.rule-card` and `.rule-number` for enforceable design rules.

## 8) Standard Utility Grids

- `.grid-2`: two-column layout
- `.grid-3`: responsive feature cards
- `.phase-grid`: responsive phase cards

## 9) Table of Contents Standard

- Use `.toc` block near the top of `<main>`
- Title must be: `📋 Table of Contents`
- Use ordered list with two columns on desktop (`columns: 2`)

## 10) Footer Standard

- Background: `var(--primary)`
- Text color: `#64748b`
- Centered text, compact size

## 11) Responsive Rules (Mobile)

At `max-width: 768px`:
- `main` padding: `20px 16px`
- `header` padding: `24px 20px`
- `nav` padding: `0 8px`
- `.grid-2` becomes single column
- TOC list becomes single column

## 12) Required Section Order

Use this section order for consistency unless explicitly overridden by project needs:

1. Vision & Goals
2. High-Level Architecture
3. Backend Structure
4. Frontend Structure
5. Service Design
6. Domain Model Class Diagrams
7. Database Schema
8. Authentication & Authorization
9. Deployment / Runtime Flows
10. Monitoring Service Design
11. Security Architecture
12. Deployment Architecture
13. Migration Strategy
14. Design Rules

## 13) Mermaid Requirement

- Include Mermaid script:

```html
<script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
```

- Initialize after content:

```html
<script>
  mermaid.initialize({ startOnLoad: true, securityLevel: 'loose' });
</script>
```

## 14) Standard HTML Starter Template

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>[Project] New System Design</title>
  <script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js"></script>
  <style>
    /* Paste full standardized CSS from this standard */
  </style>
</head>
<body>
  <header>
    <h1>🚀 [Project Name] — Architecture</h1>
    <div class="subtitle">[One-line transformation summary]</div>
    <div class="badge-stack">
      <span class="tech-badge">[Tech]</span>
    </div>
  </header>

  <nav>
    <a href="#overview">Overview</a>
    <a href="#architecture">Architecture</a>
    <a href="#backend">Backend</a>
    <a href="#frontend">Frontend</a>
  </nav>

  <main>
    <div class="toc">
      <h3>📋 Table of Contents</h3>
      <ol>
        <li><a href="#overview">Vision & Goals</a></li>
      </ol>
    </div>

    <div class="section" id="overview">
      <h2>Vision & Goals</h2>
      <div class="card">...</div>
    </div>
  </main>

  <footer>
    [Project] Architecture | Version [x.y]
  </footer>

  <script>
    mermaid.initialize({ startOnLoad: true, securityLevel: 'loose' });
  </script>
</body>
</html>
```

## 15) Quality Gate Checklist (Before Finalizing)

- [ ] Uses exact color token values.
- [ ] Uses exact typography stacks.
- [ ] Header gradient + accent border is unchanged.
- [ ] Sticky nav behavior works.
- [ ] All section H2s use left accent bar style.
- [ ] Cards/diagram cards/tables follow standard styles.
- [ ] TOC exists and links to all major sections.
- [ ] Mobile layout verified at <= 768px.
- [ ] Mermaid diagrams render correctly.
- [ ] Footer exists and follows standard colors.

## 16) Non-Negotiable Rule

If a project needs visual deviation, create a **project-specific extension layer** only after this base standard is applied. Do not change base tokens directly.

---

## Architectural Weakness Table Template

| # | Weakness | Evidence | Impact | Migration Risk |
|---|---|---|---|---|
| 1 | Shared database between modules | Multiple modules write to `USERS` table | High coupling | High |
| 2 | Business logic in stored procedures | 40+ stored procs with complex logic | Hard to test/migrate | High |
| 3 | Hard-coded configuration | DB URLs in source code | Security risk | Medium |

Use `High / Medium / Low` for Impact and Migration Risk columns.