# SYSTEM DESIGN HTML SKILL

Use this skill whenever generating a new system design HTML file.

## Goal
Produce a system design HTML document that strictly follows the self-contained baseline defined in this skill file.

Do not invent a new theme. Reuse the exact format, typography system, spacing rhythm, color palette, and section treatment.

## Hard Constraints

1. Output must be a complete HTML5 document.
2. Language must be English unless the user explicitly requests otherwise.
3. Preserve the same visual identity:
   - header gradient style
   - sticky top navigation
   - section title accents
   - card/diagram/table style
   - TOC style
4. Keep responsive behavior for mobile (`max-width: 768px`).
5. Use Mermaid for architecture and flow diagrams.
6. Keep readability-first layout with `main` centered and bounded width.

## Required Head Structure

- `<!DOCTYPE html>`
- `<html lang="en">`
- `<meta charset="UTF-8" />`
- `<meta name="viewport" content="width=device-width, initial-scale=1.0" />`
- `<title>[Project Short Name] New System Design</title>`
- Mermaid CDN include:
  - `https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js`

## Required Theme Tokens (Exact)

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

## Typography Rules (Exact)

- Body font: `'Segoe UI', Tahoma, Geneva, Verdana, sans-serif`
- Code font: `'Consolas', monospace`
- Body line-height: `1.65`
- Header title style:
  - `font-size: 2.2rem`
  - `font-weight: 800`
  - `letter-spacing: -0.5px`

## Layout Rules (Exact)

- `main` max-width: `1440px`
- `main` padding: `36px 48px`
- header padding: `36px 48px`
- nav sticky behavior:
  - `position: sticky; top: 0; z-index: 100;`

## Required Components

1. `header`
- H1 with emoji + system name + “New System Design”
- One subtitle line
- Technology badges (`.badge-stack`, `.tech-badge`)

2. `nav`
- Anchor links to major sections
- Desktop-friendly and wrapping enabled

3. `main`
- TOC block (`.toc`) near top
- Multiple sections (`.section`) with `id` attributes

4. Reusable content blocks
- `.card`
- `.diagram-wrap`
- `.diagram-title`
- `.highlight-box`
- `.rule-card`
- Tables with themed headers and zebra rows

5. `footer`
- Themed closing footer

## Title and Section Hierarchy

- Major section title: `<h2>` with left accent border
- Subsection title: `<h3>` in `var(--secondary)`

## Preferred Section Order

1. Vision & Goals
2. High-Level Architecture
3. Backend Structure
4. Frontend Structure
5. REST API Design
6. Domain Model Class Diagrams
7. Database Schema
8. Authentication & Authorization
9. Deployment / Runtime Flows
10. Monitoring Service Design
11. Security Architecture
12. Deployment Architecture
13. Migration Strategy
14. Design Rules

## Mermaid Usage Rules

- Each major architecture/flow should be in a `.diagram-wrap`
- Add a `.diagram-title` above each Mermaid block
- Initialize Mermaid at end:

```html
<script>
  mermaid.initialize({ startOnLoad: true, securityLevel: 'loose' });
</script>
```

## Mobile Responsiveness Rules

At `max-width: 768px`:
- `main { padding: 20px 16px; }`
- `header { padding: 24px 20px; }`
- `nav { padding: 0 8px; }`
- `.grid-2` becomes single column
- TOC columns collapse to one

## Output Quality Checklist

- [ ] Theme tokens exactly match baseline
- [ ] Fonts exactly match baseline
- [ ] Header/nav styling matches baseline
- [ ] TOC exists and links are correct
- [ ] H2/H3 hierarchy consistent
- [ ] Diagram cards and Mermaid render correctly
- [ ] Tables follow standard styles
- [ ] Mobile rules included
- [ ] Footer included

## Copy-Ready Prompt (Optional)

Use this prompt to generate a new file with the same standard:

"Create a complete `system_design.html` for [PROJECT NAME] using the SYSTEM DESIGN HTML SKILL. Keep the exact visual standard (colors, fonts, layout, card styles, nav, TOC, section structure, responsiveness), and populate content for [DOMAIN/PROJECT CONTEXT]. Include Mermaid diagrams for architecture and key runtime flows."
