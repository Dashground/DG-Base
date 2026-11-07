# 01. Introduction and story

## The idea in one sentence

**A company should be able to build the dashboards and workflows it needs, add AI agents that do real work inside them, and run all of it, data and models included, on its own servers.**


### Where it started: a website builder

The first plan was a **website builder**. The thinking was reasonable: lots of small businesses need sites, and open-source options are either developer-only or tied to a hosted service.

As the plan was worked through, three things stood out:

1. **A website is a shallow product.** Once the page is up, the real work of a small business happens behind it: bookings, clients, candidates, invoices, follow-ups. That is where the time and money go, and where owners cannot find software that fits.
2. **Generic internal-tool builders leave the hard part to the customer.** Tools like Budibase, Appsmith, NocoBase, Baserow, Frappe and Retool give you blocks. A salon owner or a recruiting agency still has to design the data model, screens and workflows from scratch. Most never will.
3. **AI-written code as the customization path was the wrong bet.** The earlier plan let AI generate code modules. Generated code is untrusted, needs review, breaks when the SDK changes and is hard to support. That is a poor fit for people who cannot read code in the first place.

### The pivot

Two changes produced the current plan:

- **From website builder to dashboard platform with vertical bundles.** Give away a solid base, then sell complete, ready-to-run business setups (booking, recruiting) that save weeks of work.
- **From AI-written code to configured agents.** An agent is *data*: instructions, a model, an allowlist of tools, triggers, a budget and approval rules. It can be inspected, permissioned, logged, paused and upgraded with the platform. Nobody has to trust or read generated code.

### Why sovereign AI is the lead

Many companies want AI help but cannot or will not send customer data to a third-party API: recruiters hold CVs, clinics hold health data, agencies hold client contracts. Local models (Ollama, vLLM, llama.cpp, LM Studio) are now good enough for many business tasks, but nobody has packaged them *inside a permissioned business app*.

So the pitch is not "AI dashboards". It is:

> Your dashboards. Your data. Your models. Your servers.

Public models stay available as an option. The product is fully useful with AI switched off.

### How it gets built and found

The project is built by a small team, today effectively one maintainer, with no marketing budget. Distribution is the channel itself: each bundle is **built on camera**, published as open source where it is free, and linked to its paid listing. The YouTube channel finds the first customers, who buy support and custom builds first, then bundle licenses.

That constraint shapes the design: one container, one database, one package, no cloud dependency, a small core, and documented decisions so contributors can join early.

## Who it is for

| Audience | What they get | How they use it |
| --- | --- | --- |
| **Business owners and staff** at startups and small/medium companies | A working app for their business, customized without code | Install a bundle, drag and drop, configure agents |
| **Privacy-sensitive organizations** | Dashboards and AI with no data leaving their network | Local models, air-gapped mode, egress report |
| **Developers and agencies** | A module SDK, CLI and MCP server to build and sell modules | Use Cursor, Claude Code or Codex against a running install |
| **Contributors** | A TypeScript monorepo with a small core and clear contracts | Core, modules, connectors, agent packs |

## What Dashground is, and is not

| It is | It is not |
| --- | --- |
| A self-hosted platform you assemble apps on | A hosted SaaS (hosted cloud comes only after revenue) |
| A set of vertical bundles built on a free base | A generic "build anything" tool competing on blocks alone |
| Agents that act through platform tools with approvals | An AI that writes and ships code into your server |
| A gateway that works with local or public models | A model provider. It does not ship or download models |
| Useful with AI off | Dependent on AI to function |
| Security-conscious, with release gates | A compliance guarantee. Healthcare waits for a partner or audit |

## Principles

1. **Self-hosted first.** One container plus a database. No phone-home. Licenses verify offline.
2. **Configuration over code.** Views, dashboards, workflows and agents are validated JSON. Code modules exist but are the exception, clearly labelled.
3. **Agents are governed.** Own least-privilege role, tool allowlist, approvals, budgets, full logs.
4. **One data boundary.** The query layer applies `site_id` and row-level rules on every read, so UI, API and agents all see the same data.
5. **Sovereignty is enforceable.** Data-class routing, air-gapped mode and the egress report are features, not promises.
6. **Free base must be genuinely useful.** And generic enough that it does not replace a paid bundle.
7. **Never lock the customer out.** Expired licenses stop updates or advanced features, never access to data.
8. **Prove it before building more.** Gates between phases, and spikes before risky commitments.

## Competitive position

| Space | Existing players | Our difference |
| --- | --- | --- |
| Internal tools / low-code | Budibase, Appsmith, NocoBase, Baserow, Frappe, Retool | Installable **vertical bundles** and **governed agents**, not just blocks |
| Agent tooling | Dify, Flowise, Langflow, n8n | Agents live **inside a permissioned business app** with a bundle that gives them real work |
| Sovereign AI | Mostly infrastructure projects | A finished business app on top of local models |

These comparisons are still to be verified (see [open decisions](16-risks-and-open-decisions.md)). NocoBase in particular must be studied before committing.

## Where to go next

- What is free and what is paid: [02 Product model](02-product-model.md)
- How the system fits together: [03 Architecture](03-architecture.md)
- What we build, in order: [15 Module plan and roadmap](15-module-plan-and-roadmap.md)
