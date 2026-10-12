# Exploring AI-assisted OutSystems development

> Retrospective reconstruction: this repository was assembled after the investigation to explain and reproduce the technical journey. It is not a contemporaneous activity log, and its Git history has not been backdated.

This project documents an attempt to understand how an AI coding agent could inspect and eventually modify an OutSystems 11 module through the local MCP server embedded in Service Studio.

Our first approach was direct computer use with Codex and Claude. We supplied the lab instructions and asked the agents to operate Service Studio through its graphical interface. They could reason about the requirements, but reliably executing them was difficult: Service Studio relies heavily on visual canvases, drag-and-drop nodes, property panels, modal dialogs, and spatial connections that are hard to verify from screenshots alone. This motivated the search for a semantic interface rather than more elaborate mouse automation.

The initial idea was to write a small agent skill ourselves. The skill would teach an agent how to connect to the local server, discover its tools, inspect the open module, and generate OutSystems Model API code. That experiment quickly showed that the difficult part was not opening an MCP connection. The difficult part was preserving the Model API contract, validation rules, temporary OML state, and safe merge workflow.

We also considered a multi-agent design. An orchestrator could split a lab into model discovery, service logic, UI analysis, and validation tasks, then delegate the research to specialized agents. The important constraint was that only research and planning should run in parallel. Writes against the same open Service Studio module share state and therefore need one controlled, sequential mutation pipeline.

We later found the official [OutSystems O11 MCP skills repository](https://github.com/OutSystems/outsystems11-mcp). It already encoded those hard-won operational rules, so the sensible outcome was to stop expanding the prototype and adopt the maintained skill.

## The short version

```text
Service Studio
  └─ local MCP server on 127.0.0.1
       └─ MCP host (Claude Code, Codex, Cursor, etc.)
            └─ agent + skill instructions
                 ├─ inspect the open module
                 ├─ generate Model API operations
                 ├─ validate a temporary OML copy
                 └─ merge reviewed changes into Service Studio
```

According to the [OutSystems MCP documentation](https://success.outsystems.com/documentation/11/outsystems_mcp/), the server runs inside Service Studio, accepts loopback connections, reads the open module, and applies agent changes to a copy. A skill supplies the domain-specific instructions that let the agent use those tools correctly.

## Repository map

- [`docs/01-discovery.md`](docs/01-discovery.md) — what the documentation revealed.
- [`docs/00-computer-use-attempt.md`](docs/00-computer-use-attempt.md) — why GUI automation was not reliable enough.
- [`docs/02-experiment-log.md`](docs/02-experiment-log.md) — the reconstructed investigation and failure points.
- [`docs/03-pivot.md`](docs/03-pivot.md) — why the official repository replaced the prototype.
- [`docs/architecture.md`](docs/architecture.md) — components, trust boundaries, and mutation lifecycle.
- [`docs/multi-agent-design.md`](docs/multi-agent-design.md) — the orchestration design we considered and its limits.
- [`docs/lab-use-cases.md`](docs/lab-use-cases.md) — how the experiment relates to the Bookstore and Timer labs.
- [`docs/demo-script.md`](docs/demo-script.md) — a short presentation walkthrough.
- [`skill-prototype/SKILL.md`](skill-prototype/SKILL.md) — the minimal home-grown skill prototype.
- [`computer-use-skill-prototype/SKILL.md`](computer-use-skill-prototype/SKILL.md) — a longer reconstructed skill for manually operating Service Studio through the GUI.
- [`monolithic-skill-prototype/SKILL.md`](monolithic-skill-prototype/SKILL.md) — the intentionally long, single-file version showing the early “teach every workflow in one skill” approach.
- [`evidence/connection-check.md`](evidence/connection-check.md) — a real read-only connection result captured during the reconstruction.

## What the prototype proves

The prototype captures a reasonable first iteration:

1. Recognize that the MCP endpoint is local and session-approved.
2. Inspect the open module before attempting changes.
3. Treat generated C# as a privileged operation.
4. Refuse to guess mutation syntax or merge behavior.
5. Record unresolved questions and compare them against the maintained implementation.
6. Parallelize research where useful while preserving a single sequential writer.

It intentionally does not duplicate the official repository's large Model API catalogue. Doing that would produce a stale fork rather than useful original work.

## Sources

- [OutSystems MCP documentation](https://success.outsystems.com/documentation/11/outsystems_mcp/)
- [OutSystems O11 MCP skills repository](https://github.com/OutSystems/outsystems11-mcp)
- [OpenAI documentation: build skills](https://developers.openai.com/plugins/build/skills#create-a-skill)

## License

MIT. See [`LICENSE`](LICENSE).
