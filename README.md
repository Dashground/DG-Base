# Dashground Documentation

Dashground is an open-source, self-hosted dashboard platform. Startups and small or medium companies assemble their own business apps from modules, and configurable **agents** do the customization work. It leads with **sovereign AI**: dashboards, data and models all run on infrastructure the company controls.

These docs are the plan: why we are building it, what we build and in what order, and how each part works. The source of truth for the decisions is `Open Dashboard Platform Final Architecture with Agents.md` (4 Nov 2026). These docs expand it; if they disagree, fix the docs or record a new decision.

## Reading order

| # | Doc | Answers |
| --- | --- | --- |
| 01 | [Introduction and story](/docs/01-introduction.md) | Why does this exist? Who is it for? What is it not? |
| 02 | [Product model](/docs/02-product-model.md) | What is free, what is paid, what are the four layers? |
| 03 | [System architecture](/docs/03-architecture.md) | How do the pieces fit together and how does a request flow? |
| 04 | [Data builder](/docs/04-data-builder.md) | How do users change their schema safely on a live app? |
| 05 | [Views, dashboards and access](/docs/05-views-and-dashboards.md) | How are screens defined, stored and permissioned? |
| 06 | [Modules and bundles](/docs/06-modules-and-bundles.md) | How is the product extended, installed and removed? |
| 07 | [Agent system](/docs/07-agents.md) | How do agents run, and why are they safe? |
| 08 | [Sovereign AI and model gateway](/docs/08-sovereign-ai-and-model-gateway.md) | How do local and public models work behind one interface? |
| 09 | [Integrations](/docs/09-integrations.md) | REST, webhooks, n8n, MCP, model servers |
| 10 | [Security model](/docs/10-security.md) | Threats, controls and release gates |
| 11 | [Tech stack and database strategy](/docs/11-tech-stack-and-database.md) | What we use and why |
| 12 | [Setup and deployment](/docs/12-setup-and-deployment.md) | Install paths, wizard, upgrades, backups |
| 13 | [Marketplace and licensing](/docs/13-marketplace-and-licensing.md) | How paid items are delivered and trusted |
| 14 | [Pricing and monetization](/docs/14-pricing-and-monetization.md) | Seats, bundles, services, revenue order |
| 15 | [Module plan and roadmap](/docs/15-module-plan-and-roadmap.md) | What we build, step by step, with gates |
| 16 | [Risks and open decisions](/docs/16-risks-and-open-decisions.md) | What could go wrong, what is still undecided |
| 17 | [Glossary](/docs/17-glossary.md) | Terms used across the docs |
| 18 | [Builder studio overview](/docs/18-builder-studio-overview.md) | How the builders fit together and share rules (proposed) |
| 19 | [Theme builder](/docs/19-theme-builder.md) | Design tokens, light and dark modes (proposed) |
| 20 | [Form builder](/docs/20-form-builder.md) | Drag-and-drop forms, logic, public forms (proposed) |
| 21 | [Page builder](/docs/21-page-builder.md) | Dashboards, app, portal and public pages (proposed) |
| 22 | [Widget builder](/docs/22-widget-builder.md) | Reusable data widgets (proposed) |
| 23 | [Agent builder](/docs/23-agent-builder.md) | No-code agent creation, testing, operations (proposed) |
| 24 | [Three-month plan](/docs/24-three-month-plan.md) | Week-by-week plan to 5 Feb 2027, with AI-assisted workflow (proposed) |

## Conventions

- Diagrams use [Mermaid](https://mermaid.js.org/), which GitHub and most editors render.
- **Decided** means it is in the architecture note. **Proposed** means these docs suggest it to fill a gap, and it needs confirming.
- Each doc ends with a "Decisions and reasons" or "Open questions" section where relevant, so the *why* is never separate from the *what*.

## The one-paragraph summary

A free AGPL base gives you login, roles, a data builder, views, dashboards, a module installer and an agent runtime. On top sit building-block modules and paid **vertical bundles** (booking first, then recruiting, healthcare much later): a data model, screens, dashboards, workflows and pre-configured agents installed in one step. Customers customize by configuring agents and dragging components, never by running AI-generated code. Models are reached through one gateway, with local models first-class. The whole thing is one container plus a database.
