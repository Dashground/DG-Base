# Dashground build checklist

The complete list of features and steps to build, in order. Tick a box (`- [x]`) when the step is **done and verified**. A step is done only when its tests pass on **both PostgreSQL and MySQL** where the database is involved.

- Phases follow [doc 15](15-module-plan-and-roadmap.md). Each phase ends with a **gate** that must pass before the next phase starts.
- Items tagged **(3-mo)** are in the 3-month plan ([doc 24](24-three-month-plan.md)). Untagged items come later.
- Items from docs 18-26 are **proposed**; confirm them before building.
- Doc links in brackets show where the detail lives.

## Progress

| Phase | Gate | Status |
| --- | --- | --- |
| 0. Spikes and validation | Gate 0 | Not started |
| 1. Core platform | Gate 1 | Not started |
| 2. Modules, API and builders | Gate 2 | Not started |
| 3. Booking bundle | Gate 3 | Not started |
| 4. Agents and sovereign AI | Gate 4 | Not started |
| 5. Second vertical, marketplace, 1.0 | Gate 5 | Not started |

---

## Phase 0: Spikes and validation

**Spikes (one week each, written pass or fail)**
- [ ] Runtime module install and remove on NestJS; else fall back to Next.js (3-mo) [[06](06-modules-and-bundles.md), [11](11-tech-stack-and-database.md)]
- [ ] Kysely vs Drizzle on both databases, including a staged schema change (3-mo) [[04](04-data-builder.md)]
- [ ] Dashboard grid and view builder: adopt a library or build our own (3-mo) [[05](05-views-and-dashboards.md)]
- [ ] Local models via Ollama on the booking reminder task: tool calling, structured output (3-mo) [[08](08-sovereign-ai-and-model-gateway.md)]

**Research and validation**
- [ ] Compare NocoBase, Budibase, Appsmith; write what we do differently (3-mo)
- [ ] Compare Dify, Flowise, Langflow, n8n on local-model agents
- [ ] Interview three sovereignty-minded companies (3-mo)
- [ ] Confirm booking with three real businesses (3-mo)
- [ ] Confirm the name; check domain, GitHub org, `@dashground` npm scope, Docker Hub, trademarks
- [ ] Choose first model servers and public providers for the gateway
- [ ] Legal review: AGPL core with proprietary bundles, CLA, licensing of AI-assisted code

**Gate 0**
- [ ] Module spike has a clear pass or fail
- [ ] Query layer chosen and recorded in the decision log
- [ ] Demand confirmed by at least three conversations
- [ ] Name cleared

---

## Phase 1: Core platform (free base)

**1.1 Repo and rails** [[11](11-tech-stack-and-database.md), [24](24-three-month-plan.md)]
- [ ] pnpm + Turborepo monorepo, strict TypeScript (3-mo)
- [ ] Lint, formatting, test runner (3-mo)
- [ ] CI matrix on PostgreSQL 16 and MySQL 8.4 from the first commit (3-mo)
- [ ] `CLAUDE.md` / `AGENTS.md` with the AI coding rules (3-mo)
- [ ] PR template, commit conventions, decision log
- [ ] Dependency scanning and lockfile checks in CI
- [ ] `SECURITY.md` and private reporting address

**1.2 Server skeleton** [[03](03-architecture.md)]
- [ ] NestJS on Fastify, config loading, validation of env vars
- [ ] Health endpoint, structured logging, error format
- [ ] Zod schemas package shared by server and UI (3-mo)

**1.3 Authentication** [[10](10-security.md)]
- [ ] Argon2id password hashing (3-mo)
- [ ] Secure cookie sessions, session list and revoke (3-mo)
- [ ] CSRF protection, strict security headers (3-mo)
- [ ] Rate limits on login and sensitive endpoints
- [ ] Optional TOTP
- [ ] Owner account creation flow

**1.4 Roles and the query layer** [[05](05-views-and-dashboards.md), [10](10-security.md)]
- [ ] Roles with create/read/update/delete per collection (3-mo)
- [ ] Query layer applying `site_id`, role CRUD and row-level rules (3-mo)
- [ ] Lint rule: no direct database access outside the query layer
- [ ] Boundary test suite: cross-role and cross-site, both databases (3-mo)
- [ ] Basic audit log

**1.5 Data builder** [[04](04-data-builder.md)]
- [ ] Collections stored as `app_<name>` tables, standard columns, soft delete (3-mo)
- [ ] Field types: text, number, money, date/time, boolean, select, multi-select (3-mo)
- [ ] Field types: relation, file, JSON
- [ ] Field tags (for example `personal-data`)
- [ ] Staged schema changes: preview, expand, backfill, contract (3-mo)
- [ ] Backup before destructive changes, confirmation step
- [ ] Dependency check before changing or dropping a field
- [ ] Forced mid-way failure test passes on both databases (3-mo)

**1.6 Views** [[05](05-views-and-dashboards.md)]
- [ ] Zod-validated view configuration (3-mo)
- [ ] Table view: sort, filter, group, inline edit, bulk actions (3-mo)
- [ ] Form view (basic) (3-mo)
- [ ] Kanban view (3-mo)
- [ ] Calendar view (3-mo)
- [ ] Detail view with related lists and activity
- [ ] Chart view: bar, line, pie, number cards

**1.7 Theme foundations** [[19](19-theme-builder.md)]
- [ ] Design tokens used by every component (3-mo)
- [ ] Light, dark and system modes, no flash on load (3-mo)
- [ ] Default light and dark themes pass WCAG AA

**1.8 Dashboards and widgets (foundations)** [[05](05-views-and-dashboards.md), [22](22-widget-builder.md)]
- [ ] Drag-and-drop dashboard grid (3-mo)
- [ ] Shared filters and date range (3-mo)
- [ ] Dashboard versioning and rollback (3-mo)
- [ ] Built-in widgets: number, charts, table, list (3-mo)
- [ ] Access-scope-aware widget cache, with its security test (3-mo)

**1.9 Platform basics** [[12](12-setup-and-deployment.md)]
- [ ] File storage: local disk and S3-compatible, safe uploads
- [ ] SMTP email with provider presets
- [ ] Admin UI shell (React + Vite) served by the same server (3-mo)
- [ ] Fixed homepage: dashboard when signed in, sign-in otherwise [[25](25-landing-pages-and-homepage.md)]

**1.10 Packaging** [[12](12-setup-and-deployment.md)]
- [ ] Dockerfile; one container, one port (3-mo)
- [ ] Docker Compose file for PostgreSQL and MySQL (3-mo)
- [ ] Automatic backup before migrations; restore on failure
- [ ] Setup wizard: database check, owner, storage, SMTP, sample dashboard

**Gate 1**
- [ ] A non-developer installs with Compose and builds a collection, a table view and a dashboard
- [ ] Boundary tests green on both databases
- [ ] Staged schema change survives a forced failure

---

## Phase 2: Modules, API and builders

**2.1 Job queue** [[03](03-architecture.md)]
- [ ] Database-backed queue with `SKIP LOCKED`
- [ ] Retries, backoff, dead-letter handling
- [ ] Worker runs in the same process

**2.2 Module system** [[06](06-modules-and-bundles.md)]
- [ ] `@dashground/sdk` with `defineModule` (3-mo)
- [ ] Manifest validation (3-mo)
- [ ] Lifecycle: install, migrate, register, activate, seed (3-mo)
- [ ] Deactivate, uninstall (data kept), explicit purge (3-mo)
- [ ] Dependency resolution and SDK compatibility check
- [ ] Installer UI with permission prompts and trust labels
- [ ] Backup, smoke check and rollback on install (3-mo)
- [ ] Trust tiers: official, declarative, community code
- [ ] Package signing and digest verification

**2.3 REST API** [[09](09-integrations.md), [26](26-rest-api-and-mobile-access.md)]
- [ ] Scoped API tokens (3-mo)
- [ ] OpenAPI generated from Zod (3-mo)
- [ ] Master on/off switch, off by default; 404 when off (3-mo)
- [ ] Cursor pagination, filtering, consistent errors, versioned path
- [ ] Rate limits and API activity log
- [ ] Client apps: register, pause, revoke
- [ ] Per-client exposure of collections, operations and fields
- [ ] Mobile sign-in with PKCE, rotating refresh tokens, reuse detection
- [ ] Device list and revoke
- [ ] Idempotency keys and ETags
- [ ] Declared actions endpoint

**2.4 Outbound webhooks** [[09](09-integrations.md)]
- [ ] Signed events with timestamp
- [ ] Retries and dead-letter alerts
- [ ] Destination and data-tag checks

**2.5 Theme builder** [[19](19-theme-builder.md)]
- [ ] Token editor with live light and dark preview (3-mo)
- [ ] Contrast checker (WCAG AA) blocking bad themes (3-mo)
- [ ] Presets and "derive palette from one brand color"
- [ ] Logo and favicon upload, light and dark variants
- [ ] Self-hosted custom fonts (no external font calls)
- [ ] Theme import and export
- [ ] Chart palette validation
- [ ] Email theming subset

**2.6 Form builder** [[20](20-form-builder.md)]
- [ ] Drag-and-drop canvas, palette and inspector (3-mo)
- [ ] Field binding to collection fields (3-mo)
- [ ] Validation rules, server-side Zod generated from the form (3-mo)
- [ ] Conditional logic with cycle detection (3-mo)
- [ ] Layout blocks: sections, columns, tabs, multi-step
- [ ] Repeating groups
- [ ] On-submit actions: record, email, webhook, workflow
- [ ] Public forms with a create-only public role, rate limits, honeypot, captcha option
- [ ] Form versioning; submissions record the form version
- [ ] Preview as role, device and theme

**2.7 Widget builder** [[22](22-widget-builder.md)]
- [ ] Visual query builder producing saved-query JSON
- [ ] Templates, field mapping, formatting, thresholds
- [ ] Settings exposed to the page builder
- [ ] Widget library with search
- [ ] Drill-down actions
- [ ] Code widgets via the SDK (community tier)

**2.8 Page builder** [[21](21-page-builder.md)]
- [ ] Page kinds: dashboard, app, portal, public
- [ ] Layout tree with sections, columns and responsive overrides
- [ ] Blocks: widget, form, view, content, layout, page reference
- [ ] Data binding to saved queries, page parameters, shared filters
- [ ] Visibility rules by role, data and device
- [ ] Declarative block actions
- [ ] Routing and menu placement
- [ ] Server-rendered, cached public pages with invalidation
- [ ] Sanitized rich text, allowlisted embeds
- [ ] Page versioning and rollback

**2.9 Landing pages and homepage** [[25](25-landing-pages-and-homepage.md)]
- [ ] Admin pages list: create, duplicate, preview, publish, archive (3-mo)
- [ ] Landing page kind with starter templates (3-mo)
- [ ] Homepage setting: single target dropdown (3-mo)
- [ ] Homepage rules by audience, with fallback
- [ ] Guard rails: block deleting or unpublishing the active target
- [ ] SEO fields, sitemap, robots, redirect history
- [ ] Reserved slugs and module route clash checks
- [ ] Scheduled publish and scheduled homepage swap

**2.10 Developer tooling** [[06](06-modules-and-bundles.md), [12](12-setup-and-deployment.md)]
- [ ] CLI: scaffold and validate modules
- [ ] `create-dashground` installer
- [ ] Static Git catalog (read-only)
- [ ] Offline license verification

**2.11 Building-block modules**
- [ ] Contacts
- [ ] Scheduling
- [ ] Notifications

**Gate 2**
- [ ] A declarative third-party-style module installs, runs and uninstalls on both databases; a failed install rolls back
- [ ] API tokens respect row-level rules; API off means 404
- [ ] Theme, form and page builders work with light and dark

---

## Phase 3: Booking bundle (first vertical)

**3.1 Validation** [[15](15-module-plan-and-roadmap.md)]
- [ ] Booking data model validated with three real businesses

**3.2 Bundle system** [[06](06-modules-and-bundles.md)]
- [ ] Bundle manifest format
- [ ] Bundle installer: dependency order, configuration, seed (3-mo)
- [ ] Bundle-shipped themes, landing templates and client presets

**3.3 Booking content**
- [ ] Collections: customers, services, staff, bookings, payments (basic) (3-mo)
- [ ] Views: calendar, booking form, customer detail, kanban by status (3-mo)
- [ ] Dashboards: today, this week, revenue by service, no-show rate (3-mo)
- [ ] Workflows: confirm, cancel, reschedule (3-mo)
- [ ] Email confirmations and reminders by schedule (3-mo)
- [ ] Public booking landing page with booking form (3-mo)
- [ ] Customer portal pages: my bookings
- [ ] Customer booking app client preset [[26](26-rest-api-and-mobile-access.md)]
- [ ] Demo data and demo mode

**3.4 Licensing and seats** [[13](13-marketplace-and-licensing.md), [14](14-pricing-and-monetization.md)]
- [ ] License key format and offline verification
- [ ] Builder seat counting; warn at limit, never lock out
- [ ] Advanced features gated by seat license, with grace period
- [ ] Bundle license check

**3.5 Release and feedback**
- [ ] Setup wizard complete (3-mo)
- [ ] Docs pass and security checklist run (3-mo)
- [ ] Alpha tag and demo video (3-mo)
- [ ] Booking bundle built on camera and published
- [ ] First support or custom-build leads

**Gate 3**
- [ ] At least one real business runs on it
- [ ] Free/paid line reviewed
- [ ] First revenue from support, seats or a bundle

---

## Phase 4: Agents and sovereign AI

**4.1 Model gateway** [[08](08-sovereign-ai-and-model-gateway.md)]
- [ ] OpenAI-compatible provider; Ollama first
- [ ] vLLM, llama.cpp server, LM Studio support
- [ ] Private cloud / company gateway provider
- [ ] Public API providers with owner keys, encrypted at rest
- [ ] Capability profiles and the wizard's model test
- [ ] Concurrency limits and priority queue; streaming and long timeouts
- [ ] Data-class tags and routing policy
- [ ] Request log showing exactly what was sent

**4.2 Agent runtime** [[07](07-agents.md)]
- [ ] `defineAgent` and definition validation
- [ ] Triggers: schedule, record event, user request, webhook
- [ ] Run lifecycle with step limit, timeout, budget
- [ ] Owner kill switch
- [ ] Tool registry: read, write, configuration, outbound
- [ ] Zod validation and authorization on every tool call
- [ ] Agent roles (least privilege); no administration tools; no raw SQL
- [ ] Approval inbox with approve, reject, edit, expiry
- [ ] Dry-run mode
- [ ] Run log with prompts, tool calls, cost, approvals

**4.3 Agent builder** [[23](23-agent-builder.md)]
- [ ] Minimal JSON editor for internal testing
- [ ] Step-by-step builder UI
- [ ] Derived role preview in plain language
- [ ] Playground and dry-run on real data
- [ ] Eval suite runner and model comparison
- [ ] Enabling gated on a reviewed dry-run and passing evals
- [ ] Runs list, pending approvals, usage vs budget, pause/resume
- [ ] Agent version history and rollback
- [ ] Import and export (arrive disabled, approvals on)

**4.4 Official agents**
- [ ] Booking reminder, with evals
- [ ] No-show follow-up
- [ ] Answer agent over bookings
- [ ] Customization agent producing validated diffs across data, forms, widgets, pages, themes
- [ ] Guided templates for models that fail the customization eval

**4.5 Sovereign controls** [[08](08-sovereign-ai-and-model-gateway.md)]
- [ ] Air-gapped mode
- [ ] Egress report (30 days)
- [ ] Retention settings for prompts and run logs
- [ ] Offline update bundles

**4.6 AI integrations** [[09](09-integrations.md)]
- [ ] MCP server (scoped tokens, no production data by default)
- [ ] MCP client with per-tool admin approval
- [ ] n8n node
- [ ] Hardware and tested-model guidance published

**4.7 Agent security suite** [[10](10-security.md)]
- [ ] Prompt-injection corpus
- [ ] Budget exhaustion
- [ ] Tool misuse and escalation attempts

**Gate 4**
- [ ] Booking reminder passes its eval on at least one local model
- [ ] Agent security suite green
- [ ] Air-gapped install runs with an empty egress report

---

## Phase 5: Second vertical, marketplace, 1.0

- [ ] Recruiting bundle: pipeline, candidates, application form and landing page
- [ ] CV-screening agent producing a draft shortlist
- [ ] Advanced edition: SSO (OIDC/SAML), approval workflows, retention rules, white-labelling
- [ ] Full agent pack library (paid)
- [ ] Marketplace: Official/Verified/Community labels, revocation list, community listings
- [ ] Payment provider integration (handles sales tax and VAT)
- [ ] Independent security review, findings resolved (**required before 1.0**)
- [ ] Documented upgrade path and tested restore guide
- [ ] 1.0 release

**Gate 5**
- [ ] Two bundles in real use
- [ ] Review findings resolved
- [ ] Revenue covers continued development

---

## Later (not scheduled)

- [ ] Offline sync protocol for mobile apps [[26](26-rest-api-and-mobile-access.md)]
- [ ] Push notification module (egress-reported) [[26](26-rest-api-and-mobile-access.md)]
- [ ] Official reference mobile app
- [ ] Zapier app (on demand)
- [ ] Scheduled campaigns and A/B landing variants, custom domains [[25](25-landing-pages-and-homepage.md)]
- [ ] Healthcare bundle (only with a partner or an audit)
- [ ] Community seller payouts
- [ ] Hosted cloud (only after revenue pays for it)

---

## Cross-cutting: never skip

**Release gates for every release** [[10](10-security.md)]
- [ ] Cross-role and cross-site tests pass on both databases
- [ ] Dependency scan clean
- [ ] Agent suite passes (once agents exist)

**Security checklist** [[10](10-security.md)]
- [ ] Cross-site read impossible through any interface
- [ ] Row-level rules hold in views, widgets, API and agent tools
- [ ] API off returns 404; exposure never widens a role
- [ ] Reused refresh tokens revoke the family
- [ ] Public forms and pages cannot read non-public data
- [ ] Cached results never cross access scopes
- [ ] Tampered or revoked packages are rejected
- [ ] Uploads are safe; XSS and CSRF controls verified
- [ ] Air-gapped mode blocks undeclared egress

**Documentation**
- [ ] Docs updated alongside every change that alters a decision
- [ ] Decision log current ([doc 16](16-risks-and-open-decisions.md))
- [ ] Install, upgrade, backup and restore guides tested by someone other than the author

**Open decisions to close** [[16](16-risks-and-open-decisions.md)]
- [ ] Bundle prices, standard seat price, one-time update period
- [ ] Yearly builder seat price and grace period
- [ ] Multi-tenancy meaning of `site_id`
- [ ] Workflow engine shape
- [ ] Telemetry policy
- [ ] Contribution model and CLA
