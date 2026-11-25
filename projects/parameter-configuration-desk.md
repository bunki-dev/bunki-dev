# Parameter configuration desk

**Type:** vehicle engineering · **Pattern:** allowlist transport, rules engine

[← Back to portfolio](../README.md)

## Problem
Vehicle parameters at a heavy-truck OEM have to be configured correctly for each build, and only approved changes may reach the vehicle systems.

## What I built
- A **rules engine** that checks parameter combinations.
- An **allowlist transport**: only explicitly allowed operations can be sent on.

## Architecture
```mermaid
flowchart LR
  U[Engineer] --> D[Configuration desk]
  D --> RE{Rules engine}
  RE -- fails --> U
  RE -- passes --> AL{Allowlist}
  AL -- not allowed --> X[Blocked]
  AL -- allowed --> T[Transport to target]
```

## Results
| Measure | Result |
|---|---|
| Tests | ~1,700 |

## Hard problems
- **Default deny.** An allowlist means a new, unreviewed operation is blocked until someone adds it, rather than allowed until someone notices.
