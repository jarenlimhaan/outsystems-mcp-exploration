# Phase 0 — attempting direct computer use

Before investigating MCP, we tried giving Codex and Claude the lab context and asking them to operate Service Studio through computer-use capabilities.

This established an important distinction: understanding the written lab was not the same as reliably manipulating the visual development environment.

## What the agents could do

- Interpret the broad requirements from the lab instructions.
- Identify likely entities, actions, screens, and logic steps.
- Suggest the next operation in Service Studio.
- Navigate ordinary menus and dialogs in simple cases.

## What remained difficult

- Service Studio uses large visual canvases whose important state may be outside the current viewport.
- Logic depends on spatially connected nodes, making drag-and-drop placement and connector creation fragile.
- Properties can be distributed across panels, tabs, dialogs, and expression editors.
- Similar-looking nodes and icons are difficult to distinguish consistently from screenshots.
- A click or drag can appear successful without proving that the underlying model changed correctly.
- Small UI-layout or resolution differences can invalidate a previously successful sequence.
- Long workflows compound errors because each later step assumes every earlier visual operation succeeded.

Providing more lab context improved planning, but it did not solve those interaction and verification problems.

## Resulting design decision

We stopped treating the graphical interface as the primary automation surface. Computer use remained potentially useful for setup, approval dialogs, and visual confirmation, while structured model reads and writes needed a semantic interface.

That requirement led us to the Service Studio MCP server:

```text
computer use: operate pixels and infer whether the model changed
MCP tools:     address model elements and receive structured results
```

The MCP approach did not remove the need for validation or human review. It moved the core operation from brittle screen coordinates to explicit tools and Model API objects.

The accompanying [`computer-use-skill-prototype`](../computer-use-skill-prototype/SKILL.md) reconstructs what a more complete visual-operation skill would have looked like. It documents stable navigation paths, common data, logic, REST, timer, and interface workflows, plus verification and recovery rules. Its length also illustrates why adding more instructions could reduce some mistakes but could not make pixel interaction equivalent to a semantic model API.
