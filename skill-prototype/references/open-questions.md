# Open questions from the first prototype

These questions defined the boundary between safe module inspection and unsupported mutation:

## Connection and discovery

- Which tool creates or approves a session?
- Is the current port stable across Service Studio sessions?
- How does the client distinguish the open module from references?

## Model reads

- Which reads return code and which return structured data?
- Does UI inspection differ between Reactive and Traditional Web modules?
- How are actions, screens, timers, integrations, and structures addressed by name?

## Model mutation

- Does the write tool expect a full `Action<IESpace>` lambda or only a body?
- Which imports and Model API namespaces are available?
- Who saves the resulting OML and chooses its output path?
- What response distinguishes compilation failure, runtime failure, and model validation failure?
- How are several changes chained without repeatedly merging?

## Finalization

- Which result identifies the mutated OML?
- When is Compare and Merge opened?
- What happens to temporary state after merge rejection?
- Is publishing part of merge or a separate privileged operation?

The maintained OutSystems skill later supplied tested answers to these questions, which is why this prototype remained read-only.
