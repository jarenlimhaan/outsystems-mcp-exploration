# Candidate lab use cases

The supplied coursework suggested a useful progression for evaluating an OutSystems-aware agent. This file records use cases only; it does not reproduce the lab documents or claim the agent completed them.

| Lab area | Candidate agent task | Main capability being tested |
|---|---|---|
| Order Service | Summarize entities, relationships, and exposed actions. | Data-model and service inspection |
| Place Order Service | Trace the order flow and explain validation or transaction boundaries. | Server-action inspection |
| Bookstore UI, parts 1–4 | Inventory screens, data sources, navigation, and reusable blocks. | Reactive UI inspection |
| Timers | Identify timers, their actions, schedules, and safe retry behavior. | Asynchronous logic inspection |

## Safe evaluation order

1. Ask for an explanation of an existing module.
2. Ask for a structured inventory of entities and actions.
3. Ask the agent to trace one end-to-end use case.
4. Attempt a small reversible mutation in a disposable module.
5. Review validation output and the Compare and Merge result.
6. Only then consider a larger lab-shaped change.

This ordering tests understanding before granting the agent a mutation path.
