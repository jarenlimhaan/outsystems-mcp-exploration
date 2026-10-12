---
name: operate-outsystems-service-studio-visually
description: Operate OutSystems 11 Service Studio through computer use when a user explicitly wants visual UI interaction rather than MCP Model API tools. Use for guided creation of entities, structures, server or client actions, REST integrations, timers, screens, and widgets. Require verification after every meaningful UI action; do not publish, delete, or install dependencies without explicit authorization.
---

# Operate OutSystems Service Studio Visually

This is a reconstructed teaching prototype showing how a student might teach an agent to operate Service Studio from the graphical interface. It is not a claim that every workflow below was executed successfully by an agent.

Prefer semantic MCP tools when they are available and the user allows them. Use this visual workflow only when the user explicitly requests computer use, when an MCP operation is unavailable, or when the task is to demonstrate the manual Service Studio process.

## Core operating rule

Treat every visual interaction as an unverified hypothesis until Service Studio displays evidence that it succeeded.

For each meaningful step:

1. Observe the current module name, active main tab, selected tree element, editor, and Properties panel.
2. State the single UI action to perform.
3. Click, type, or drag only that action.
4. Observe again.
5. Confirm the expected tree node, property value, canvas node, connector, or validation state.
6. Continue only after confirmation.

Never execute a long blind sequence of clicks from memory.

## Stable navigation model

Navigate by labels and hierarchy, not stored pixel coordinates. Service Studio window layouts and panel sizes can vary, but these logical areas remain the useful anchors:

- **Interface**: screens, UI flows, blocks, images, themes, client variables, roles, and screen/client actions.
- **Logic**: server actions, integrations, REST APIs, exceptions, timers, and dependencies.
- **Data**: database entities, structures, entity diagrams, and site properties.
- **Processes**: business processes when the module supports them.
- **Editor or canvas**: the selected screen, action flow, entity diagram, or other model editor.
- **Toolbox**: draggable widgets or logic nodes relevant to the active editor.
- **Properties**: settings for the currently selected element.
- **TrueChange or errors pane**: errors and warnings that must be checked before declaring completion.

If a named area is not visible, reorient from the module tree and active tab. Do not guess that a hidden or collapsed panel is absent.

## Before changing anything

1. Confirm the correct application and module are open.
2. Identify the module type: Reactive Web, Mobile, Traditional Web, Service, or Library.
3. Read the user's requested outcome and list the model elements likely to change.
4. Inspect whether those elements already exist before creating duplicates.
5. Note current errors or warnings so they are not incorrectly attributed to the new work.
6. Ask before any destructive action, dependency installation, environment change, or publish.

## Choose the relevant workflow

- For entities, attributes, structures, diagrams, and site properties, read [references/data-workflows.md](references/data-workflows.md).
- For server actions, REST APIs, consumed services, exceptions, and timers, read [references/logic-workflows.md](references/logic-workflows.md).
- For screens, menus, local variables, client actions, forms, lists, and widgets, read [references/interface-workflows.md](references/interface-workflows.md).
- For verification, recovery, and stopping rules, always apply [references/verification-and-recovery.md](references/verification-and-recovery.md).

Read only the references needed for the current task. For a cross-layer feature, read them in this order: data, logic, interface, verification.

## Manipulating tree elements

Use this pattern whenever the instruction says to add something beneath a folder or parent object:

1. Select the correct main tab.
2. Expand the tree until the intended parent label is visible.
3. Right-click the parent, not a similarly named child.
4. Choose the exact `Add ...` command.
5. Immediately rename the generated item if the task specifies a name.
6. Select the new item and verify its name and properties.

If Service Studio silently generates a different name because the requested name is already used, stop and report the actual name. Do not create another duplicate.

## Editing properties

1. Select exactly one model element.
2. Locate the property by label rather than assumed vertical position.
3. Change one property at a time.
4. Commit the edit using the control's normal behavior, such as Enter, focus change, or selection.
5. Re-select the element and confirm the value persisted.

For expressions, open the expression editor when available. Do not type complex expressions into an uncertain inline field. After saving, reopen or reselect the element to confirm the expression text.

## Dragging nodes and widgets

Dragging is high risk because a visual drop can miss its intended parent.

1. Expand the target container, placeholder, flow, or canvas area first.
2. Locate the source element in the Toolbox or data tree.
3. Drag once and wait for Service Studio to finish updating.
4. Verify the new element appears under the correct parent in the widget tree or flow.
5. Select it and verify its type and generated name.
6. Undo immediately if it landed under the wrong parent.

For flow nodes, verify both incoming and outgoing connectors. A node merely sitting near another node is not connected.

## Building an action flow

1. Open the intended server, service, timer, REST-method, or client action by name.
2. Identify its Start and End nodes and existing branches.
3. Add one node from the Toolbox.
4. Configure its source action, aggregate, assignment, condition, or exception behavior.
5. Connect it to the flow and verify arrow direction.
6. Check node arguments and expressions in Properties.
7. Repeat for the next node.
8. Trace every path from Start to an End or intentional exception path.
9. Arrange the nodes so branches and connectors remain readable.
10. Resolve new TrueChange errors before leaving the action.

Never infer connection from proximity. Never add several unconfigured nodes and attempt to repair the flow afterward.

## Building a screen

1. Open the intended screen and its widget tree.
2. Identify named placeholders such as `Title`, `Actions`, and `MainContent`.
3. Add the outer layout/container structure before leaf widgets.
4. Place each widget under its exact intended parent.
5. Bind lists, forms, inputs, and expressions only after the hierarchy is correct.
6. Create event actions from the event property only when the requested action does not already exist.
7. Verify labels, mandatory fields, enabled state, widths, visibility, and role conditions.
8. Preview or run the screen only after TrueChange errors are cleared.

When adding UI content in a visually ordered container, account for Service Studio inserting new widgets before or after the selected sibling. Use the widget tree to verify final order.

## Dependencies and integrations

Dependencies can affect other modules and environments.

- Inspect existing dependencies first.
- Ask before installing a Forge component or adding a new external dependency.
- In Manage Dependencies, select only the explicitly required elements.
- Apply once, wait for refresh, then verify the imported action or entity appears in the expected tree.
- For consumed REST APIs, confirm the Swagger/OpenAPI URL belongs to the intended environment before importing methods.

Do not expose secrets, passwords, tokens, private endpoints, or student identifiers in screenshots or reports.

## Publish boundary

Creating or editing model elements does not authorize publishing.

Immediately before pressing **1-Click Publish**:

1. Summarize the elements changed.
2. Report remaining errors and warnings.
3. Ask the user to confirm publishing unless the current request explicitly said to publish.
4. After confirmation, click once and wait for the publish result.
5. Verify the final status in the publish tab. Do not infer success from the button animation.

If publishing fails, capture the visible error, stop, and explain it. Do not repeatedly publish unchanged work.

## Completion criteria

A task is complete only when:

- the intended element exists under the correct parent;
- names and properties match the request;
- action flows have valid connectors on every path;
- screen widgets are under the correct placeholders and containers;
- no new TrueChange errors remain;
- runtime behavior was tested when the task required it;
- publish status was verified if publishing was explicitly authorized;
- the user receives a concise summary of what changed and what remains unverified.

## When to stop

Stop and ask for user direction when:

- the visible UI differs materially from these instructions;
- more than one plausible module, screen, action, or entity matches the name;
- a click would delete data or overwrite an existing element;
- a dependency or environment credential is required;
- Service Studio reports an error whose full text is not visible;
- two attempts at the same visual interaction fail;
- the next step would publish or affect an external system without authorization.
