# Five-minute demonstration script

## 1. Problem statement

“We wanted to know whether a general coding agent could understand and modify an OutSystems module without manually exporting and parsing OML files.”

## 2. Initial computer-use attempt

“We first gave Codex and Claude the lab context and tried to let them operate Service Studio visually. They could understand the requirements, but the canvas, drag-and-drop flows, property panels, and limited state verification made long workflows brittle.”

Show [`00-computer-use-attempt.md`](00-computer-use-attempt.md).

## 3. Discovery

“The O11 documentation showed that Service Studio already contained a local MCP server. That changed the task from building an API server to teaching an agent how to use an existing one.”

Show [`01-discovery.md`](01-discovery.md).

## 4. First prototype

“We created a minimal skill that could identify the open module and enforce inspection before mutation. The connection was easy; generating correct Model API code and handling temporary OML state were the difficult parts.”

Show [`skill-prototype/SKILL.md`](../skill-prototype/SKILL.md) and [`02-experiment-log.md`](02-experiment-log.md).

## 5. Evidence

“A read-only test reached the module open in Service Studio and returned `EmployeeTest`, a Service module.”

Show [`evidence/connection-check.md`](../evidence/connection-check.md).

## 6. Multi-agent idea

“We also considered using an orchestrator to split the work among requirements, module-discovery, Model API, and review agents. Research could happen in parallel, but allowing several agents to mutate the same Service Studio module would create competing snapshots and merge risk. Our rule became: parallelize understanding, serialize changes.”

Show [`multi-agent-design.md`](multi-agent-design.md).

## 7. Pivot

“We later found OutSystems' maintained O11 MCP skill repository. It already encoded the exact lambda, validation, session, and merge contracts we were trying to infer, so we adopted it instead of maintaining a weaker fork.”

Show [`03-pivot.md`](03-pivot.md) and the [official repository](https://github.com/OutSystems/outsystems11-mcp).

## 8. Takeaway

“The useful result was not reimplementing OutSystems' skill. It was understanding the architecture, proving the local integration, identifying its safety boundaries, and learning when to replace a prototype with maintained infrastructure.”
