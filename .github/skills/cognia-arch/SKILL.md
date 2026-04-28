---
name: cognia-arch
description: 'system architecture visualization and design skill. Act as a principal architect. Use when: visualizing architecture, creating system diagrams for systems, understanding  component relationships, mapping  data flows, identifying architectural weaknesses, producing mermaid diagrams in HTML format, documenting  architectural constraints before redesign.'
argument-hint: ' system name or path to analysis report to base diagrams from'
---

#  System Design & Visualization

# Instructions

1. **Before generating HTML output**, read and follow [DESIGN_SKILL.md](./DESIGN_SKILL.md) for generation guidelines and [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md) for exact visual theme, typography, and layout standards.
2. Generate the `{project_name}-architecture.html` and `{project_name}-architecture.md` files following the standards defined in both referenced files above.
3. Read the - `{project_name}-architecture.html` and `{project_name}-architecture.md` files after created to ensure they are correctly generated and contain the required diagrams and documentation. If the HTML file is not rendering diagrams correctly, check for common Mermaid syntax issues (unclosed blocks, reserved keywords in node IDs, etc.) and regenerate the file if needed.
4. **Run validation** on the generated HTML file using the File Creation Validation Checklist from [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md) before proceeding. This ensures the diagrams will render correctly and are not broken due to syntax errors or file generation issues.
5. **Report validation results**:
   - If valid: Confirm the diagram is valid and exit
   - If invalid: Show the errors found and explain what's wrong
6. **Fix the issues** automatically (invalid diagrams have no value)
7. **Re-validate** to confirm the fix worked
8. Repeat steps 6-7 until there are no validation issues

## Role
**Principal Architect** — Reconstruct and visually document the  architecture with precision. Produce diagrams that make even the most chaotic  systems understandable.


## Output Location
Create folder `cognia/` and produce:
- `{project_name}-architecture.md` — Architecture documentation
- `{project_name}-architecture.html` — Interactive visual diagrams (Mermaid.js)

> ⚠️ **Always overwrite these files completely** — never append. Use `create_file` or write the full content from scratch. Appending produces two HTML documents in one file, which breaks rendering.

## HTML Generation Standards
When generating the `{project_name}-architecture.html` file:
1. **Follow [DESIGN_SKILL.md](./DESIGN_SKILL.md)** for generation guidelines and best practices
2. **Apply [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md)** for:
   - Exact CSS theme tokens (colors, spacing, typography)
   - Document structure and required HTML5 elements
   - Responsive behavior for mobile (`max-width: 768px`)
   - Mermaid diagram container styling
   - Navigation and section treatment

---

## Procedure

### Step 1 — Identify Architectural Style
Determine the dominant architectural pattern:
- **Monolith**: Single deployable unit, shared DB
- **Layered (N-Tier)**: Presentation → Business → Data
- **Modular Monolith**: Internal modules with clear boundaries
- **SOA**: Service-oriented, WSDL/SOAP contracts
- ** Distributed**: Multiple apps, shared DB (common anti-pattern)

Document the style formally and explain why it was likely chosen historically.

### Step 2 — Module Boundary Mapping
- List all modules/components/subsystems
- Identify responsibilities and ownership
- Mark which modules are **coupled**, **cohesive**, or **isolated**
- Identify **shared kernel** — code that is consumed by multiple modules
- Identify **cross-cutting concerns**: logging, auth, error handling

### Step 3 — Communication Pattern Analysis
Map how components communicate:
- **Synchronous**: HTTP, RPC, direct DB calls
- **Asynchronous**: JMS, MQ, file-based messaging
- **Database coupling**: Multiple services writing to same tables
- **Event-driven**: Any pub/sub or callback patterns

### Step 4 — Generate Visual Diagrams (HTML + Mermaid.js)
Produce all diagrams as an HTML file with embedded Mermaid.js.

**Use the guidelines from [DESIGN_SKILL.md](./DESIGN_SKILL.md) and exact standards from [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md) for all HTML output generation.**

Use the **HTML + Mermaid.js Page Template** from [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md) as the starting document for `{project_name}-architecture.html`.

Required diagram sections (match the template structure):
- **4.1** — High-Level Architecture (system boundary: clients, app server, DB, external)
- **4.2** — Component Dependency Diagram (all modules, coupling visible)
- **4.3** — Data Flow Diagram (request → processing → response)
- **4.4** — Authentication/Authorization Flow (login sequence)
- **4.5** — Database Architecture (ER overview, ownership, God-table highlights) — *skip if NoSQL-only*
- **4.6** — Deployment Topology (servers, network zones, load balancers, environments)

> **Important**: Replace ALL placeholder node labels with the ACTUAL  system components discovered during analysis. The template is a starting point only.

#### Diagram 4.5 — Database Architecture
Produce an entity-relationship overview (not a full-column ER — key entities and relationships only):

- Include all major tables/collections grouped by owning module (use Mermaid `subgraph` or `erDiagram`)
- Highlight **God tables** (shared by 3+ modules) with a distinct style or annotation
- Show **cross-module DB coupling** edges (dashed arrows between subgraphs)
- Mark tables with > 1M rows as high-volume (use a note or label)
- For NoSQL stores: show collection groupings and their primary access patterns instead of ER notation

```mermaid
erDiagram
  CUSTOMERS ||--o{ ORDERS : places
  ORDERS ||--|{ ORDER_LINES : contains
  ORDER_LINES }o--|| PRODUCTS : references
  CUSTOMERS ||--o{ ADDRESSES : has
```

#### Diagram 4.6 — Deployment Topology
Map the runtime infrastructure as a Mermaid `graph TD` (or `C4Context` style):

- **Compute**: All servers, VMs, containers, Lambda functions with their roles
- **Load balancers & reverse proxies**: nginx, HAProxy, AWS ALB, Cloudflare, etc.
- **CDN**: If present — origin and edge cache points
- **Network zones**: DMZ, internal app tier, DB tier, admin zone (use `subgraph` per zone)
- **Environment inventory**: List all environments (prod, staging, UAT, dev) and whether they are isolated or shared
- **External service endpoints**: DNS, NTP, SMTP relay, VPN gateways

```mermaid
graph TD
  subgraph DMZ
    LB[Load Balancer nginx]
    CDN[CDN CloudFront]
  end
  subgraph AppTier
    APP1[App Server 1]
    APP2[App Server 2]
  end
  subgraph DBTier
    DB[(PostgreSQL Primary)]
    DBreplica[(PostgreSQL Replica)]
  end
  CDN --> LB
  LB --> APP1
  LB --> APP2
  APP1 --> DB
  APP2 --> DB
  DB --> DBreplica
```

### Step 4.1 — Validate the Generated HTML File

After writing `{project_name}-architecture.html`, run through the **File Creation Validation Checklist** from [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md) before proceeding.

Key checks for this skill's output:
- `<!DOCTYPE html>` appears exactly **once** (no accidental file append)
- All 6 required diagrams are present as `<pre class="mermaid">` blocks (not `<div>`)
- Every `subgraph` block is closed with `end`
- `alt … else … end` in sequenceDiagram is fully closed
- No `\n` inside quoted node labels — use `<br/>` for multi-line labels
- Node IDs contain no spaces or reserved keywords (`end`, `subgraph`)
- **erDiagram labels** — every relationship label is one word or a quoted multi-word string; no empty labels after `:`; no spaces in entity names
- **Panzoom script** — `<script src="https://cdn.jsdelivr.net/npm/panzoom@9/dist/panzoom.min.js"></script>` is in `<head>` AND the full toolbar + panzoom initialisation block is present before `</body>` (copy verbatim from the template in DESIGN_STANDARDS.md — never omit it)
- **Theme tokens and typography** — verify all CSS variables and fonts match exactly with [DESIGN_STANDARDS.md](./DESIGN_STANDARDS.md)

If the file is missing or any check fails, **regenerate the entire file** from scratch using `create_file`. Do not attempt to patch individual lines.

### Step 5 — Identify Architectural Weaknesses
Document at least 3 critical weaknesses:

| # | Weakness | Evidence | Impact | Migration Risk |
|---|---|---|---|---|
| 1 | Shared database between modules | Multiple modules write to `USERS` table | High coupling | High |
| 2 | Business logic in stored procedures | 40+ stored procs with complex logic | Hard to test/migrate | High |
| 3 | Hard-coded configuration | DB URLs in source code | Security risk | Medium |

### Step 6 — Coupling Hotspot Map
Identify the tightest coupling points that will be hardest to untangle during migration:
- Shared DB tables with multiple consumers
- God classes/services with 20+ dependencies
- Circular module dependencies
- Framework-specific annotations bleeding into domain logic

---

## Output Format

### {project_name}-architecture.md
```markdown
#  System Architecture

## 1. Architectural Style
## 2. Module Inventory
  - 2.1 Module List with Responsibilities
  - 2.2 Module Dependency Matrix
## 3. Communication Patterns
  - 3.1 Synchronous Calls
  - 3.2 Asynchronous Flows
  - 3.3 Database Coupling Points
## 4. Cross-Cutting Concerns
## 5. Architectural Weaknesses
## 6. Coupling Hotspots
## 7. Constraints for New Design
```

### {project_name}-architecture.html
Full Mermaid.js HTML file containing all diagrams from Step 4 above, customized to actual system components.

---

## Definition of Done (DoD)

### Diagrams
- [ ] High-level architecture diagram (system boundary clearly shown)
- [ ] Component dependency diagram (all modules included, coupling visible)
- [ ] Data flow diagram (input → processing → output for main flows)
- [ ] Authentication/authorization flow diagram
- [ ] Database architecture diagram (entity groupings, God tables, cross-module coupling)
- [ ] Deployment topology diagram (network zones, servers, LB, CDN, environments)
- [ ] All diagrams rendered correctly in HTML (verify in browser)

### Technical Accuracy
- [ ] All integrations mapped with protocol (HTTP, JMS, DB direct, FTP, etc.)
- [ ] Sync vs async flows clearly distinguished
- [ ] Stateful vs stateless components identified
- [ ] Shared data stores identified with all consumers listed

### Insights
- [ ] At least 3 architectural weaknesses identified with evidence
- [ ] Tight coupling areas highlighted with migration risk rating
- [ ] Coupling hotspot map produced

### Validation
- [ ] Diagram walkthrough completed with system design team
- [ ] Diagrams reviewed for accuracy against design decisions
- [ ] Mermaid syntax validated and diagrams render without errors in browser

---
