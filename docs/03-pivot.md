# Phase 3 — pivot to the maintained OutSystems skill

The discovery of [`OutSystems/outsystems11-mcp`](https://github.com/OutSystems/outsystems11-mcp) changed the project from reverse-engineering to evaluation and integration.

## Why we pivoted

The official repository was not merely an MCP configuration file. It contained the exact component our prototype was trying to reconstruct: agent instructions, Model API references, examples, host setup guides, and the safety rules around temporary OML changes.

The sensible engineering choice was therefore:

```text
keep our architectural understanding
+ keep our use cases and evaluation notes
+ use the maintained skill for the fragile Model API contract
- stop duplicating its generated references and mutation recipes
```

## What remained original work

- Identifying suitable lab use cases for agent-assisted development.
- Understanding the local trust boundary and approval flow.
- Separating safe inspection from privileged mutation.
- Designing the read-before-write workflow.
- Testing a real connection against an open Service Studio module.
- Evaluating whether the official skill answered the unresolved prototype questions.

## What we adopted

- The maintained `servicestudio-mcp-oml` skill.
- Tested Model API examples instead of guessed method names.
- Explicit session and merge lifecycle rules.
- Style-aware reads for different O11 module types.

This is the main engineering lesson of the project: prototyping was valuable because it revealed the real problem, but owning a duplicate of the official knowledge base would not have been valuable.
