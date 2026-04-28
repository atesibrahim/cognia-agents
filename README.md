# Cognia

A collection of specialised AI agents and skills for comprehensive project analysis — covering architecture, backend, frontend, iOS, Android, UX, technical quality, product ownership, performance, security, reverse engineering, and test engineering.

## Agents

Agents auto-detect the platform(s) present in a project (backend, frontend, iOS, Android, or mixed) and apply only the relevant analysis playbook(s). Every agent writes its findings to a mandatory output file in `cognia/`.

| Agent | Domain | Description |
|-------|--------|-------------|
| `cognia-android` | Android mobile | Full Android codebase audit: screens, components, networking, navigation, state management |
| `cognia-arch` | System architecture | Component map, data flow, service boundaries, scalability, and architectural risk assessment |
| `cognia-backend` | Backend / API | Endpoint inventory, service catalogue, integrations, database schema, auth, and background jobs |
| `cognia-frontend` | Frontend / Web | Page and route inventory, component catalogue, state management, API integration, and build config |
| `cognia-ios` | iOS mobile | Full iOS codebase audit: screens, components, networking, navigation, state management |
| `cognia-perf` | Performance analysis | Auto-detects platform(s) and audits for bottlenecks: slow queries, large bundles, blocking threads, memory issues — with a prioritised improvement roadmap |
| `cognia-po` | Product ownership | Feature inventory, user stories, requirements gaps, business value mapping, and backlog recommendations |
| `cognia-reverse` | Reverse engineering | Extracts business domain, user roles, workflows, business rules, and integrations from code — output written for business analysts and product owners |
| `cognia-sec` | Security analysis | Auto-detects platform(s) and audits for vulnerabilities: injection, broken auth, insecure storage, exposed secrets, dependency CVEs — with a CVSS-aligned remediation roadmap |
| `cognia-tech` | Technical quality | Code quality, tech debt, dependency audit, security vulnerabilities, and test coverage gaps |
| `cognia-test` | Test engineering | Audits existing test coverage for correctness and quality, identifies missing unit/integration/e2e tests, and produces a prioritised test backlog with acceptance criteria |
| `cognia-ux` | UI/UX design | Page inventory, user flow mapping, design consistency, accessibility audit, and UX improvements |

## Skills

| Skill | Description |
|-------|-------------|
| `cognia-arch` | System architecture visualisation — Mermaid diagrams, component relationships, data flows |
| `cognia-tech` | Deep technical analysis — reverse engineering, dependency mapping, security posture |
| `cognia-ux` | UI/UX design — wireframes, design systems, user journeys, WCAG accessibility |

## Usage with GitHub Copilot

All agent definitions live in `.github/agents/*.agent.md`. Reference them in VS Code's agent mode or any Copilot-compatible tool.

### Quick start

1. Install the package (or copy the files into your project):

```bash
npm install cognia
```

2. Copy the agent and skill files into your project's `.github/` directory, or point your Copilot configuration at `node_modules/cognia/.github/`.

3. In VS Code agent mode, select the relevant agent (e.g. `cognia-arch`) and describe the project or sub-system to analyse.

## Cross-Agent Rules

1. **Evidence first** — every finding cites at least one concrete file path.
2. **Tag confidence** — claims are marked `Confirmed` (directly evidenced) or `Inferred` (best-fit interpretation).
3. **Missing evidence** — states `Not found in scanned files` rather than guessing.
4. **Output files are mandatory** — analysis is not complete until the designated output file is written.
5. **No domain creep** — each agent respects its scope; cross-domain observations belong in a handoff note.

## License

MIT
