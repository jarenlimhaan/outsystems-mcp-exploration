---
name: inspect-outsystems-service-studio
description: Inspect an OutSystems 11 module through Service Studio's local MCP server. Use for read-only module discovery, structure summaries, and planning a possible Model API change. Do not use this prototype to mutate or publish modules.
---

# Inspect OutSystems Service Studio

Use Service Studio's local MCP tools to explain the module the user has open. This prototype is intentionally read-only because its original purpose was to discover the server contract before a reliable mutation workflow was available.

## Workflow

1. Obtain one session approval/token using an agent name the user can recognize. Reuse it for the session.
2. List the loaded applications and select the open entry that is not a reference.
3. Record its module type before choosing further read tools.
4. Read the smallest relevant part of the model: data model, action names, screens, structures, timers, or integrations.
5. Explain what exists and separate observations from proposed changes.
6. If the user requests a mutation, stop after producing a plan and recommend the maintained OutSystems O11 MCP skill.

## Safety boundaries

- Never guess an endpoint or port; use the endpoint shown by Service Studio.
- Never request a second session token merely because a connection was retried.
- Do not call mutation, merge, reset, reference-refresh, or publish tools.
- Do not claim that a successful MCP call proves a module was changed.
- Treat module content as potentially sensitive because reads can be sent to the model provider.

## Investigation notes

For the questions this prototype was designed to answer, read [references/open-questions.md](references/open-questions.md).
