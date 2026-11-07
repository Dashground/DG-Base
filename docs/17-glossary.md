# 17. Glossary

| Term | Meaning |
| --- | --- |
| **Agent** | A configured worker: instructions, model capability, tool allowlist, triggers, budget, approval rules. Acts only through platform tools |
| **Agent pack** | A set of prebuilt agents with tested instructions |
| **Agent builder** | No-code UI that produces agent definitions, tests them (playground, dry-run, evals) and manages runs. See doc 23 |
| **Air-gapped mode** | Blocks all outbound connections except owner-allowed ones; disables public providers, external MCP and marketplace fetch |
| **Approval inbox** | Queue of agent actions and configuration diffs waiting for a person |
| **App collection** | A user-defined table, named `app_<collection>` |
| **Builder seat** | A named user who works in the no-code builder. Paid ($49 per month) |
| **Bundle** | Manifest of modules, seed data, dashboards, workflows and agents that forms a vertical solution |
| **Capability profile** | Result of testing a model: tool calling, structured output, context length, speed, agents passed |
| **Collection** | A user-defined entity type (like a table) in the data builder |
| **Contract (migration)** | Final stage of a staged change: remove the old column or table |
| **Builder studio** | The admin area containing the data, form, page, widget, theme and agent builders. See doc 18 |
| **Dashboard** | Versioned drag-and-drop grid of cards with shared filters. A page in grid mode |
| **Design token** | A named theme value (color, font, radius) that components reference instead of fixed styles |
| **Form builder** | Drag-and-drop editor for forms with validation and conditional logic. See doc 20 |
| **Page builder** | Drag-and-drop editor for dashboard, app, portal and public pages. See doc 21 |
| **Theme** | A set of design tokens with light and dark modes. See doc 19 |
| **Widget** | Reusable data block built from a saved query, a template and settings. See doc 22 |
| **Data-class routing** | Gateway rule that restricts tagged fields to allowed providers |
| **Declarative module** | Module made only of collections, views, workflows and agents; no custom code |
| **Dry-run** | Agent mode where write and outbound tools are recorded but not executed |
| **Egress report** | List of outside destinations contacted in the last 30 days |
| **Expand / backfill / contract** | Three-stage schema change pattern safe on both PostgreSQL and MySQL |
| **Kill switch** | Owner control that stops all agents |
| **Model gateway** | Single interface through which all model calls pass |
| **Module** | Unit that adds a capability; installable and removable from the admin UI |
| **Module table** | Table owned by a module, prefixed `mod_<name>_` |
| **MCP** | Model Context Protocol. Dashground is both a server (for external AI tools) and a client (for approved external tools) |
| **Query layer** | The only path to the database; applies `site_id`, role CRUD and row-level rules |
| **Row-level rule** | Condition on a role, e.g. only records assigned to me |
| **Run** | One execution of an agent, fully logged |
| **Sovereign AI** | Running dashboards, data and models on infrastructure the company controls |
| **`site_id`** | Column on every table that scopes data to a site |
| **Trust tier** | Official, Declarative, or Community code |
| **Vertical bundle** | A bundle for one kind of business: booking, recruiting, clinic |
| **View** | Saved, Zod-validated configuration for displaying a collection |
| **Zod** | TypeScript schema library used for validation across the platform |
