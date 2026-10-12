# Evaluation of the three approaches

This evaluation compares the approaches explored during the project: direct computer use, a custom agent skill, and the maintained OutSystems O11 MCP skill. It is a qualitative engineering evaluation based on the observed workflow. It is not a controlled performance benchmark, and it does not claim success rates or timings that were not measured.

## Evaluation question

What is the most reliable way for an AI coding agent to understand and change an OutSystems 11 module in Service Studio?

## Common test scenario

Each approach can be evaluated against the same small workflow:

1. Identify the module currently open in Service Studio.
2. Report its module type.
3. Summarize its entities and server-side logic.
4. Propose one small, reversible change.
5. Explain how the change would be validated.
6. Do not publish unless explicitly authorized.

Using the same scenario keeps the comparison focused on the interaction method rather than differences in task complexity.

## Results summary

| Approach | What worked | Main limitation | Appropriate role |
|---|---|---|---|
| Codex or Claude computer use | Interpreted lab requirements and could navigate simple labeled UI elements | Visual canvases, drag-and-drop, connectors, hidden panels, and state verification made long workflows brittle | Setup, approval dialogs, demonstrations, and visual checks |
| Custom read-only skill | Added a disciplined read-before-write workflow and documented safety boundaries | Did not contain a tested mutation contract for Model API C#, temporary OML state, validation, and merge behavior | Learning, architectural exploration, and safe module inspection |
| Monolithic computer-use skill | Captured detailed manual workflows for data, logic, integrations, timers, and screens | More instructions could not eliminate uncertainty inherent in pixel interaction | Demonstrating what would need to be taught for GUI automation |
| Official OutSystems O11 MCP skill | Provided semantic tools, tested Model API guidance, session handling, validation interpretation, and controlled merge behavior | Requires compatible Service Studio setup; write capabilities are beta and still require careful review | Primary implementation workflow |

## Approach 1: direct computer use

The first experiments supplied Codex and Claude with the lab context and asked them to operate Service Studio visually. The agents could reason about the intended entities, actions, screens, and logic. The main difficulty was converting that plan into a long sequence of reliable graphical operations.

Service Studio is not a conventional form-based application. Important behavior is represented by spatial flows, connectors, nested widget trees, expressions, property panels, and context-sensitive toolboxes. A drag can appear successful while placing an element under the wrong parent. Two nodes can appear adjacent without being connected. Later steps can therefore build on an undetected earlier mistake.

**Conclusion:** computer use was useful for understanding the manual workflow and handling visible dialogs, but it was not the strongest primary interface for model construction.

## Approach 2: custom skill prototype

The next idea was to encode Service Studio knowledge as an agent skill. The prototype taught the agent to identify the open module, inspect before changing, avoid duplicate elements, and treat publishing as a separate authorization boundary.

This improved procedural discipline, but the experiment exposed deeper questions:

- the exact C# lambda shape expected by the mutation tool;
- allowed imports and Model API types;
- temporary OML save and chaining behavior;
- differences between compilation, runtime, and TrueChange failures;
- module-style-specific reads;
- merge, reset, reference refresh, and publish behavior.

These were implementation contracts, not merely prompting problems. Adding generic instructions without tested answers would make the skill longer but not safer.

**Conclusion:** the custom skill was valuable for discovering the real integration requirements, but it should remain read-only until those contracts are verified.

## Approach 3: official MCP skill

The maintained [`OutSystems/outsystems11-mcp`](https://github.com/OutSystems/outsystems11-mcp) repository supplied the missing operational knowledge. It includes agent instructions, Model API references, examples, setup guidance, and the state-management rules required to use Service Studio's local MCP server.

The local connection was verified against an open module. A read-only module listing returned `EmployeeTest` with module type `Service`. No mutation or publish call was needed for that test.

The key improvement was semantic interaction. Instead of inferring model state from pixels, the agent could call explicit tools and inspect structured results. Mutations still require validation and human review, but the interaction surface matches the underlying model more closely.

**Conclusion:** the official MCP skill is the preferred implementation route, while computer use remains complementary.

## Multi-agent implication

The evaluation also informs the proposed multi-agent design:

- requirements analysis, documentation research, module inspection, and review may run in parallel;
- Model API mutations, validation, and merge should remain sequential for a single module;
- the orchestrator should collect evidence from read-only agents before assigning work to one writer.

The resulting rule is: **parallelize understanding, serialize changes**.

## Reproducible demonstration prompts

Use a disposable or course-owned module and keep the first demonstration read-only.

### Prompt 1: connection

> List the modules currently loaded in Service Studio. Identify the open module and its type. Do not make any changes.

### Prompt 2: understanding

> Summarize the open module's data model, server-side actions, integrations, and timers. Separate direct observations from your interpretation. Do not modify or publish the module.

### Prompt 3: planning

> Propose the smallest reversible change that would demonstrate the integration. List the model elements involved, validation checks, and merge steps, but do not apply it yet.

### Prompt 4: controlled mutation

> After inspecting the affected model objects, apply the approved change to a disposable module, check compilation and validation results, read the change back, and merge it for review. Do not publish.

The fourth prompt uses write capabilities and should be attempted only after the user understands the beta status and review flow.

## Evidence still worth adding

The following would strengthen the demonstration when available:

- a cropped screenshot of the Service Studio connection approval dialog;
- a screenshot of the sanitized read-only module-list result;
- a short screen recording of the same read-only prompt through computer use and MCP;
- the Service Studio version used for the test;
- a disposable-module mutation with its validation and merge result.

Before publishing visual evidence, remove usernames, email addresses, environment URLs, tokens, module keys, student identifiers, and unrelated project names.

## Limitations and disclosure

- This repository is a retrospective reconstruction, not a contemporaneous development log.
- The multi-agent architecture was considered as a design; it is not presented as a completed production system.
- The long computer-use skills demonstrate the amount of guidance visual automation would require; they do not prove autonomous completion of the supplied labs.
- The only recorded live evidence currently included is a read-only connection result.
- No benchmark timings or statistical success rates were collected.
- The course documents informed the workflow categories but are not copied into this public repository.

## Overall conclusion

The investigation began as a computer-use problem and became an interface-design problem. More UI instructions improved planning but could not provide reliable access to the underlying OutSystems model. A local MCP server plus a domain-specific, maintained skill offered the stronger division of responsibility: the server exposes semantic operations, the skill teaches their contract, the agent plans and validates changes, and Service Studio retains the human review boundary.
