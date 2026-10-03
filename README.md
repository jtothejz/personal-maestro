# Personal Maestro: Multi-Agent Task Orchestrator & Runbook Supervisor

> **An orchestrator that empties your task queues with specialized AI agent nodes—without allowing autonomous processes to send messages, spend money, or leak private data.**

`Personal Maestro` brings enterprise-grade agent orchestration to personal productivity boards (Trello, Linear, Notion, SQLite). While tools like [Inlet](https://github.com/jtothejz/inlet-capture-engine) fill the backlog, Personal Maestro executes, researches, breaks down, and stages tasks into actionable cards.

---

## Core Philosophy

1. **The Column Is the Assignment**: Dragging a card into `Maestro Doing` assigns it to the agent cluster. Nothing enters `Doing` on its own.
2. **Drafts Never Need Permission. Sends Always Do**: The agent prepares, researches, drafts, and compiles. The human operator clicks send, books, signs, or pays.
3. **Nothing Personal Reaches the Outside World**: Zero outbound emails, SMS, or external API mutations without human attended gates.
4. **Ask Everything Once**: Questions are batched per card with proposed default choices so the operator taps rather than types.
5. **No Forked Engines**: Reuses a single standard orchestrator loop and briefing-pack protocol across all domains.

---

## Board Lane Lifecycle

```
[Backlog / Intake]
       │
       ▼ (Human drags card)
[Maestro Doing] ──(Orchestrator assembles Briefing Pack)──> [Specialist Node Execution]
                                                                   │
       ┌───────────────────────────────────────────────────────────┴─────────────────────────┐
       ▼                                                           ▼                         ▼
[Needs Review]                                                 [Blocked]                   [Done]
(Waiting for human decision / send)             (Waiting on external event / re-check)   (100% complete)
```

---

## Specialist Node Roster

Each task is evaluated and routed to an isolated subagent definition:

| Node Name | Specialty / Domain | Boundary Constraint |
| :--- | :--- | :--- |
| `pm-researcher` | Price checks, contractor shortlists, product comparisons, technical research. | Never contacts vendors or submits inquiry forms. |
| `pm-planner` | Decomposes large project cards into ordered checklists, dependencies, and material lists. | Never books appointments or creates shared calendar events without approval. |
| `pm-writer` | Drafts correspondence, contractor briefs, application essays, and memos. | Staged locally; never sends messages or posts content. |
| `pm-admin` | Gathers forms, compiles checklists, indexes documents. | Never signs documents, pays invoices, or mutates third-party accounts. |

---

## Briefing Pack Architecture

Nodes are never handed raw, unstructured chat context. The orchestrator compiles each task into an immutable **Briefing Pack**:

```yaml
card_id: "card_8921"
title: "Research heat pump water heater rebates and local certified installers"
task: "Identify eligible federal + local utility rebates and compile top 3 licensed installers."
constraints:
  - "Must qualify for 2026 Inflation Reduction Act 30% credit"
  - "Installer must service Snohomish County, WA"
budget_limit: 0 # Research only
settled_answers:
  panel_capacity: "200A main service"
  current_system: "50-gallon electric tank (2014)"
```

---

## Running the Orchestrator

```bash
# Manual run from CLI:
python3 scripts/personal_maestro_orchestrator.py --scan-once

# Continuous daemon mode:
python3 scripts/personal_maestro_orchestrator.py --daemon --interval=900
```

---

## Author & License

Architected by [Jake Zimmer](https://jtothez.com). Released under the [MIT License](LICENSE).
