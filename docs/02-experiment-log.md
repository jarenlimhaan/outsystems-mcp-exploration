# Phase 2 — reconstructed experiment log

This is a retrospective reconstruction of the investigation, not a dated laboratory notebook.

## Experiment 0: direct computer use

We first tried using Codex and Claude computer-use capabilities with the lab instructions supplied as context. Both approaches could reason about the intended result, but operating Service Studio remained unreliable. Visual-canvas navigation, drag-and-drop flow construction, property editing, and confirmation of the underlying model state were difficult to perform consistently.

This experiment reframed the problem. Instead of asking how to improve a long sequence of mouse operations, we asked whether Service Studio exposed a structured interface that an agent could call directly. That question led to the local MCP documentation.

## Experiment A: prove the endpoint is useful

Goal: connect through an MCP host and ask the server which modules are loaded.

Expected sequence:

1. Start the MCP server from Service Studio.
2. Register the endpoint displayed by Service Studio in the MCP host.
3. Start a new agent session.
4. Approve the connection dialog in Service Studio.
5. Call the module-listing tool.

Result during reconstruction: the server reported an open Service module named `EmployeeTest`. This established that the integration was reading live Service Studio state rather than a manually exported OML file.

## Experiment B: teach an agent to inspect before changing

The first skill prototype made reads mandatory before mutations. This was needed because generated code must target the names and model shapes that actually exist in the module.

The proposed read sequence was:

```text
listApps
  → choose the open, non-reference module
  → read its data model
  → read the relevant action, screen, timer, or structure
  → summarize the current state
```

This part was straightforward enough for a small instruction-only skill.

## Experiment C: infer the write contract

The difficult step was generating C# for the OutSystems Model API. Several details could not safely be guessed:

- whether the tool expected a full lambda or a sequence of statements;
- which namespaces were available;
- whether the agent or host called `Save`;
- which model interfaces represented each module style;
- how references and global keys were resolved;
- how generated flows were positioned visually;
- how a successful save differed from a valid OutSystems model;
- how the temporary OML was merged into the module.

Guessing any of these could produce compilation failures, invalid models, or changes that appeared successful but never reached Service Studio.

## Prototype stopping rule

The home-grown skill therefore stopped at safe reads and documented writes as experimental. It required an observed tool schema and a tested example before allowing any mutation. That was a more defensible result than embedding speculative C# snippets.

## Experiment D: consider parallel agents

We considered placing an orchestrator in front of several specialized agents:

- a requirements agent to break a lab into verifiable outcomes;
- a module-discovery agent to inventory entities, actions, screens, and timers;
- a Model API researcher to investigate the C# surface;
- a validation agent to review proposed changes and failure modes.

These tasks could run independently while they remained read-only. Their findings would return to the orchestrator, which would build one ordered implementation plan.

We rejected parallel mutation of the same module. Concurrent writers could start from different snapshots, generate incompatible temporary OML files, or invalidate assumptions made by another agent. The proposed rule became **parallelize understanding, serialize changes**.

## What the later official skill clarified

The maintained OutSystems repository supplied the missing operational contract, including:

- session-token handling;
- the full-lambda requirement for Model API code;
- sandbox and import restrictions;
- the temporary OML/session-pointer lifecycle;
- validation result interpretation;
- module-style-specific reads;
- merge, reset, refresh, and publish rules;
- tested examples and generated Model API references.

At that point, continuing the original skill would have meant recreating and maintaining the same knowledge less reliably.
