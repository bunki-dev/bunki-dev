# Calibration change control

**Type:** automation · **Stack:** SQL Server with temporal history

[← Back to portfolio](../README.md)

## Problem
Calibration changes at a heavy-truck OEM need a full, trustworthy history: who changed what, when, and what it was before.

## What I built
- Change control for calibrations on **SQL Server temporal tables**, so every previous version is kept automatically by the database.

## Architecture
```mermaid
flowchart LR
  E[Engineer] --> CC[Change control]
  CC --> T[(Current table)]
  T -- automatic --> H[(Temporal history)]
  H --> AUD[Audit / point-in-time view]
```

## Results
| Measure | Result |
|---|---|
| Tests | 311 |

## Hard problems
- **History you can't forget to write.** Temporal tables record history in the database itself, so no application code path can skip it.
