# Considered multi-agent orchestration

Before adopting the maintained OutSystems skill, we considered whether several agents could reduce the amount of manual exploration needed for each lab.

This was an architecture proposal, not evidence that a production multi-agent system was implemented.

## Proposed roles

```text
                         ┌──────────────────────┐
                         │ Orchestrator agent   │
                         │ owns task + evidence │
                         └──────────┬───────────┘
                                    │
              ┌─────────────────────┼─────────────────────┐
              │                     │                     │
              ▼                     ▼                     ▼
    ┌──────────────────┐  ┌──────────────────┐  ┌──────────────────┐
    │ Requirements     │  │ Module discovery │  │ Model API        │
    │ split the lab    │  │ inspect O11      │  │ research syntax  │
    └────────┬─────────┘  └────────┬─────────┘  └────────┬─────────┘
             │                     │                     │
             └─────────────────────┼─────────────────────┘
                                   ▼
                         ┌──────────────────────┐
                         │ Reviewer agent       │
                         │ risks + validation   │
                         └──────────┬───────────┘
                                    ▼
                         one sequential writer
```

## Example task split

For a Bookstore feature, the orchestrator could delegate:

1. Extract the expected entities, actions, and screens from the lab requirements.
2. Inspect the currently open modules and record what already exists.
3. Compare requirements against the current model and identify gaps.
4. Research the Model API types needed for those gaps.
5. Review the proposed plan for destructive operations, missing dependencies, and validation risks.
6. Execute the approved changes sequentially through one writer.

## Why not let every agent write?

The Service Studio integration is stateful. A writer works against a snapshot or temporary OML chain associated with the module. If several agents mutate the same module independently, they may:

- base changes on different snapshots;
- create conflicting versions of the same element;
- overwrite assumptions about generated names or keys;
- validate successfully in isolation but fail when combined;
- present several competing merge operations to the user.

Parallel writers would therefore add coordination cost precisely where correctness matters most.

## Chosen orchestration rule

> Parallelize requirements analysis, module inspection, documentation research, and review. Serialize Model API mutations, validation, and merge.

This design preserves the main benefit of specialized agents without treating shared Service Studio state like an ordinary set of independent source files.
