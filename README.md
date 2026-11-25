AI & automation engineer. I build LLM agents, RAG systems and production tooling at PACCAR (Kenworth · Peterbilt), working AI-first with a multi-agent coding workflow and independent review gates.

> **About these write-ups.** Most of my work is internal. The projects below are described without proprietary code, data, system names, people or customers. Numbers are real; where a target was missed, the page says so. Code you can run is in the [public projects](#public-projects-you-can-run) section.

## At a glance

| Project | What it is | Status | Headline result |
|---|---|---|---|
| [Field-technician assistant](projects/field-technician-assistant.md) | RAG over 270 service manuals, offline-first PWA, MCP server | Prototype | hit@5 81% vs 59.5% keyword; wrong citation codes 354 → 0 |
| [Warranty Insights "Ask"](projects/warranty-insights-ask.md) | LangGraph text-to-SQL with SQL guard and grounding check | Pilot | 0 ungrounded numbers; 60/60 adversarial cases blocked |
| [Agent Dash](projects/agent-dash.md) | Control plane for AI agents: tasks, budgets, approvals | Personal use | 370 commits in 8 days; 17 review findings fixed test-first |
| [Bunki workflow](projects/bunki-workflow.md) | Multi-role Claude Code workflow with plan approval and a ledger | Workflow | 38 plans across 22 projects, 0 abandoned |
| [LLM catalogue enrichment benchmark](projects/catalogue-enrichment-benchmark.md) | Enriching e-commerce parts data with LLMs | Benchmark | Batching cut cost 1.5–2.3× |
| [Change-triage ML engine](projects/change-triage-engine.md) | Precedent matching + TF-IDF | Shipped, auto-file off | 91.5% walk-forward agreement |
| [Fleet telematics analytics](projects/fleet-telematics-analytics.md) | One analysis layer, three UIs, tool-calling chat | Data product | 857 tests; LLM never computes numbers |
| [Telematics marts + private text-to-SQL](projects/telematics-text-to-sql.md) | Pseudonymised marts with a private text-to-SQL agent | Data product | 90% of answerable eval questions; 26 s → 2 s |

## Requirements → evidence

| What AI-engineering roles ask for | Where it shows |
|---|---|
| Building LLM and agentic systems | [Field-technician assistant](projects/field-technician-assistant.md), [Warranty Insights "Ask"](projects/warranty-insights-ask.md), [Agent Dash](projects/agent-dash.md), [Fleet telematics chat](projects/fleet-telematics-analytics.md) |
| Python, plus TypeScript | Python: text-to-SQL, ML triage, automation. TypeScript: [Agent Dash](projects/agent-dash.md) (Node/React), [Field-technician assistant](projects/field-technician-assistant.md) (React, Fastify) |
| AI-first development with Claude Code | [Bunki workflow](projects/bunki-workflow.md): researcher, coder, tester, reviewer and runner roles, plan approval gate, ledger |
| Tool use, orchestration, RAG, guardrails, MCP | Hybrid RAG with enforced citations and an MCP server ([field assistant](projects/field-technician-assistant.md)); LangGraph routing, sqlglot guard ([Ask](projects/warranty-insights-ask.md)); ACP + MCP ([Agent Dash](projects/agent-dash.md)) |
| Evals | Golden sets with dev/holdout split ([Ask](projects/warranty-insights-ask.md)), hit@5 retrieval eval ([field assistant](projects/field-technician-assistant.md)), walk-forward backtest ([triage](projects/change-triage-engine.md)), 400-day replay ([FX](projects/fx-rate-automation.md)) |
| Accuracy, latency and cost trade-offs | Latency under a live 2 s timeout ([field assistant](projects/field-technician-assistant.md)); median latency vs accuracy ([Ask](projects/warranty-insights-ask.md)); batching and prompt caching ([catalogue benchmark](projects/catalogue-enrichment-benchmark.md)); 26 s → 2 s ([text-to-SQL](projects/telematics-text-to-sql.md)) |
| Security and responsible AI | Role permissions inside SQL, 38/38 access matrix; redaction review; pseudonymised views; fail-closed auth; spend caps; shipping an ML feature disabled when it missed its target |
| APIs, Docker, CI/CD, Azure | Azure Container Apps, Easy Auth, Bicep, OIDC pipeline, non-root Docker ([Ask](projects/warranty-insights-ask.md)); Fastify API; Postgres |
| Ownership and code review | Independent GO/NO-GO reviews, NO-GOs fixed before release ([field assistant](projects/field-technician-assistant.md), [Agent Dash](projects/agent-dash.md), [ECU bulk update](projects/ecu-bulk-update.md)) |
| Standouts: search, e-commerce, conversational | [Trolley](https://github.com/bunki-dev/trolley): a grounded shopping agent with allergen-aware search, basket, orders and refunds; hybrid search with reciprocal-rank fusion; e-commerce parts catalogue enrichment; voice and chat interfaces |

## Featured projects

### [Field-technician assistant (RAG)](projects/field-technician-assistant.md)
An offline-first assistant that answers technicians' questions from 270 service manuals (10,573 chunks) with enforced citations. Postgres hybrid search (full-text + vectors, fused with reciprocal-rank fusion) lifted hit@5 from 59.5% (keyword) to 81%, or 70% under a live 2-second timeout. Role permissions are enforced inside SQL and pass a 38/38 access matrix. Includes an MCP server with five tools, voice, and a field-case learning loop with redaction review. 1,494 tests. The independent review said NO-GO twice before GO.

### [Warranty Insights "Ask"](projects/warranty-insights-ask.md)
Plain-English questions over warranty data. A LangGraph text-to-SQL agent routes from a small to a large model, every query passes an sqlglot guard, and a grounding check rejects any number that isn't in the result. On a 76-question golden set, accuracy rose from 21.6% to 60.8% on dev and from 4% to 44% on holdout, with zero ungrounded numbers and zero crashes. The 90% target wasn't met, and the page says why. All 60 adversarial cases were blocked.

### [Agent Dash](projects/agent-dash.md)
A Node/TypeScript/React control plane for running AI agents like a small organisation. It has an org chart, atomic task checkout, budgets (warning at 80%, auto-pause at 100%), an approvals inbox, cron, Windows process supervision, and a CEO console that delegates work, over ACP and MCP. It took 370 commits in 8 days. The review came back NO-GO with 17 findings, and all were fixed with tests written to fail first.

### [Bunki workflow](projects/bunki-workflow.md)
How I build with Claude Code. Separate researcher, coder, tester, reviewer and runner roles, a `/plan` step that waits for approval, and a ledger of every plan. 38 plans across 22 projects: 4 went through clean, 34 were corrected along the way, and none were abandoned. Reviews recorded 25 findings, including at least 7 NO-GOs that were fixed before release.

## All projects

### AI agents & ML
- [Field-technician assistant (RAG)](projects/field-technician-assistant.md): prototype
- [Warranty Insights "Ask"](projects/warranty-insights-ask.md): pilot
- [Agent Dash](projects/agent-dash.md): personal use
- [Bunki workflow](projects/bunki-workflow.md): my AI-first build process
- [LLM catalogue enrichment benchmark](projects/catalogue-enrichment-benchmark.md): e-commerce parts
- [Change-triage ML engine](projects/change-triage-engine.md): shipped with auto-file disabled

### Data products
- [Fleet telematics analytics](projects/fleet-telematics-analytics.md)
- [Telematics marts + private text-to-SQL](projects/telematics-text-to-sql.md)
- [Customer-fit scoring dashboard](projects/customer-fit-scoring.md)
- [BOM cost explorer](projects/bom-cost-explorer.md): live
- [Finance-report enrichment](projects/finance-report-enrichment.md): live

### Vehicle engineering
- [Guarded 3270 mainframe automation](projects/mainframe-automation.md)
- [Parameter configuration desk](projects/parameter-configuration-desk.md)
- [Definition-file builder rewrite](projects/definition-file-builder.md)
- [ECU bulk update](projects/ecu-bulk-update.md)
- [Supplier guide ↔ drawing verification](projects/supplier-drawing-verification.md)

### Automation
- [Warranty-agreement rule engine](projects/warranty-agreement-engine.md)
- [FX rate automation](projects/fx-rate-automation.md)
- [Supplier Contact Hub](projects/supplier-contact-hub.md)
- [Exactly-once escalation emailer](projects/escalation-emailer.md)
- [Calibration change control](projects/calibration-change-control.md)
- [Six Sigma form skill](projects/six-sigma-form-skill.md)

## Public projects you can run

Clean-room projects built in my own time, with no work code or data.

| Project | What it shows | Try it |
|---|---|---|
| [Trolley](https://github.com/bunki-dev/trolley) | A supermarket shopping agent over 1,600+ real Australian products (Open Food Facts): find products, build a basket, manage orders and sort out problems. Rules live in typed tools, a confirmation gate means nothing is spent, cancelled or refunded without a yes, and every reply is checked so it can't cite a product or price the tools didn't return or promise allergy safety. 34 deterministic eval scenarios in CI, including 11 adversarial. Runs in the browser via Pyodide. | [Open the demo](https://bunki-dev.github.io/trolley/) |
| [FitBasket](https://github.com/bunki-dev/fitbasket) | Tool-using agent that plans meals and workouts around a sport schedule, with inline how-to videos, and builds a deals-aware grocery basket. Pydantic-typed tools shared by the LLM and an MCP server, guardrails in code, offline and LLM-as-judge evals. Python runs in the browser via Pyodide. | [Open the app](https://bunki-dev.github.io/fitbasket/) |
| [Game Night](https://github.com/bunki-dev/game-night) | A party game hosted by an AI game master. Real-time FastAPI WebSockets, phones as controllers, QR join, an anonymous LLM judge with an injection filter, and judge-agreement evals. | [Play it](https://game-night-nq9e.onrender.com) |
| [ShelfTalk](https://github.com/bunki-dev/shelftalk) | Text-to-SQL for a fictional grocery chain. A semantic-layer planner answers common questions with no model; an LLM agent handles the rest through an engine-level read-only guard that blocks personal data. Execution-accuracy evals in CI. | [Ask it](https://bunki-dev.github.io/shelftalk/) |
| [Bunki HQ](https://github.com/bunki-dev/bunki-hq) | My personal assistant as a talking orb that runs a small company of AI agents across my projects: tool-using agents with role-scoped tools, delegation, atomic task checkout, approval gates for anything external, per-agent budgets that auto-pause, and live build health from GitHub. TypeScript, runs in the browser or on a PC with SQLite. | [Open it](https://bunki-dev.github.io/bunki-hq/) |

## How I work

- **Plan first.** Every change starts as a written plan that is approved before code is written.
- **Measure.** Golden sets, holdout splits, backtests and replays decide whether something works, not demos.
- **Independent review on high-risk releases.** A separate reviewer gives GO or NO-GO. A NO-GO is fixed and re-reviewed, not argued away.
- **Safe by default.** Dry-run modes, read-only access, fail-closed auth, spend caps, checkpoints after the first item in a batch.
- **Report honestly.** When a target is missed, I say so and ship what is safe. The change-triage engine shipped with auto-file disabled because it covered 29% of cases at 100% precision, against a 60% target.
