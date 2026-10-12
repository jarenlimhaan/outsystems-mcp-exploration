# Architecture and trust boundaries

## Components

| Component | Responsibility |
|---|---|
| Service Studio | Owns the open O11 module and runs the local server. |
| Service Studio MCP server | Exposes read/write tools over a loopback endpoint. |
| MCP host | Connects tools to an AI agent and maintains its session. |
| Agent | Interprets the user's intent and selects tool calls. |
| Skill | Supplies OutSystems-specific workflow and Model API knowledge. |
| Temporary OML | Holds generated changes before they reach the live module. |
| Compare and Merge | Gives the user a review boundary before accepting changes. |

## Read path

```text
User prompt
  → agent selects a read tool
  → MCP host calls Service Studio on 127.0.0.1
  → server snapshots/reads the open module
  → structured result returns to the agent
  → agent explains the result
```

## Write path

```text
User requests a change
  → agent first reads the affected model objects
  → agent generates restricted Model API C#
  → server applies it to a temporary OML copy
  → compiler and model validation results are checked
  → agent requests a merge of the successful result
  → user reviews or auto-accepts according to Service Studio settings
  → live module receives the accepted change
```

## Security observations

- Loopback binding limits network exposure but does not make generated code harmless.
- The Service Studio approval dialog is the first trust boundary.
- Read operations can expose module content to the model provider used by the MCP host.
- Mutation code is privileged and should only target modules the user owns.
- Publishing is a separate external effect and should require an explicit user request.
