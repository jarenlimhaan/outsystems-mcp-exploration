# Phase 1 — discovering the local MCP surface

The starting observation was that newer Service Studio builds expose an MCP server locally. The official documentation answered several architectural questions immediately:

- The server runs inside Service Studio rather than in the OutSystems cloud environment.
- It binds to the loopback interface (`127.0.0.1`), with `41820` as the default port.
- The port can move when it is already occupied, so the endpoint shown by Service Studio is authoritative.
- A user must approve a new agent session before the agent can read or change a module.
- Read operations are generally available; write and merge operations are beta capabilities.
- Module changes are first made against a copy and normally reach the live module through Compare and Merge.

This changed the problem definition. We did not need to invent a remote OutSystems API or upload OML files to another service. We needed two client-side pieces:

1. MCP host configuration pointing to Service Studio's current endpoint.
2. A domain skill teaching the model how to sequence the advertised tools safely.

## Initial hypothesis

The first prototype assumed a skill could remain small:

```text
connect → list modules → inspect model → generate C# mutation → validate → merge
```

The read half of this hypothesis was realistic. The write half hid most of the complexity.

## Questions that drove the experiment

- How does an agent identify the module currently open in Service Studio?
- What does a read tool return: JSON, Model API code, or both?
- Does mutation code contain a complete C# lambda or only its body?
- Who chooses the output OML path?
- How are multiple edits chained before merge?
- How are compiler errors different from TrueChange validation errors?
- Does Reactive, Mobile, Traditional Web, or Service module style alter the tool sequence?
- When does the user review the generated change?

Those questions became the scope of the prototype skill and experiment log.
