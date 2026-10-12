---
name: build-outsystems-apps-with-computer-use
description: Use computer vision and mouse or keyboard interaction to build and inspect OutSystems 11 applications in Service Studio. Covers entities, structures, actions, REST APIs, timers, screens, forms, lists, menus, testing, recovery, and publishing. Use only when the user explicitly requests visual Service Studio operation; prefer semantic MCP tools when available.
---

# Build OutSystems Apps with Computer Use

This reconstructed prototype represents the long, single-file skill we considered writing before adopting the maintained OutSystems MCP skill. It demonstrates how a student might teach an agent the Service Studio workflow in detail. It is not a contemporaneous activity log or proof that every visual workflow was completed autonomously.

## Mission

Translate a user's requirement or lab instruction into small, verifiable Service Studio interactions. Work through the graphical interface, but reason in terms of OutSystems model elements: modules, entities, attributes, structures, actions, parameters, integrations, timers, screens, widgets, expressions, roles, and dependencies.

Do not behave like a macro. A macro assumes the screen is exactly where it was previously. Instead, observe the current UI, identify elements by visible labels and hierarchy, execute one meaningful operation, and verify the resulting model state before continuing.

## Prefer MCP when possible

If Service Studio's MCP server and an appropriate OutSystems skill are available, recommend that route for model reads and writes. MCP addresses semantic model objects and returns structured results. Computer use operates pixels and can misinterpret selection, drag targets, hidden panels, connectors, or generated names.

Continue with visual operation when:

- the user explicitly asks to demonstrate the manual workflow;
- the required operation is unavailable through MCP;
- the task involves an approval dialog or visual check;
- the user wants a side-by-side comparison with MCP;
- the task is read-only navigation and explanation.

## Non-negotiable safety rules

1. Confirm the application and module name before editing.
2. Confirm the module type before creating UI or logic.
3. Inspect whether an element already exists before adding it.
4. Change one meaningful thing at a time.
5. Verify every creation, rename, property edit, drag, connector, and expression.
6. Never publish unless the user explicitly requested or immediately confirms it.
7. Never install Forge components, change environment settings, refresh dependencies, or delete data without authorization.
8. Never enter real secrets or credentials into a field visible in a screenshot or report.
9. Stop after two failed attempts at the same visual interaction.
10. Report uncertainty rather than claiming an invisible model change succeeded.

## Service Studio mental model

Do not memorize pixel coordinates. Find these stable concepts by visible label:

- **Interface** contains screens, UI flows, blocks, images, themes, roles, client variables, and client-side behavior.
- **Logic** contains server actions, integrations, exposed and consumed APIs, exceptions, dependencies, timers, and related flows.
- **Data** contains database entities, structures, entity diagrams, and site properties.
- **Processes** contains business processes when supported by the module.
- The **module tree** organizes elements under the selected main tab.
- The **editor or canvas** displays the selected screen, action flow, entity diagram, or integration.
- The **Toolbox** provides nodes or widgets that can be dragged into the active editor.
- The **Properties** panel edits the selected model element.
- **TrueChange** reports model errors and warnings.
- The **1-Click Publish** tab reports upload, compilation, deployment, and final status.

Panel locations may move. A collapsed panel is not missing. Reorient from the active module, main tab, and tree labels before interacting.

## Universal interaction loop

For every model operation:

1. Observe the current screen.
2. Identify the active module and selected tab.
3. Expand the minimum tree path needed for the operation.
4. Select the exact parent or target element.
5. Perform one click, context-menu command, text entry, property change, or drag.
6. Wait for Service Studio to update.
7. Observe the tree, canvas, Properties panel, and TrueChange state.
8. Confirm the expected result.
9. Record the actual generated name when it differs from the requested name.
10. Continue only after verification.

Never execute a memorized chain such as "click here, click there, drag twice, type three values" without observing between steps.

## Creating tree elements

Use this pattern for entities, structures, actions, exceptions, timers, screens, and methods:

1. Select the relevant main tab.
2. Expand the correct parent folder.
3. Search visually for an existing element with the requested name.
4. Right-click the parent, not an adjacent child.
5. Choose the exact `Add ...` command.
6. Rename the generated element immediately.
7. Press Enter or otherwise commit the rename.
8. Reselect the element and confirm its actual name.
9. Inspect its Properties before adding children.

If Service Studio adds a numeric suffix, do not create another element. Investigate the naming conflict.

## Editing properties and expressions

1. Select exactly one target element.
2. Locate the property by label.
3. Change one property at a time.
4. Commit the edit through Enter, focus change, or the field's normal control.
5. Reselect the element and confirm persistence.

Open the expression editor for non-trivial expressions. Verify referenced variables, aggregate names, list-current records, function names, parentheses, and string quoting. Save, then reopen or reselect the owner to confirm the expression.

## Dragging and dropping

Drag operations are high risk because a widget or node may land under the wrong parent.

1. Expand and select the target placeholder, container, list item, flow, or canvas area.
2. Locate the source widget, node, entity, structure, or variable.
3. Drag once.
4. Wait for any automatic generation to complete.
5. Verify the new object in the widget tree or action flow.
6. Select it and confirm its type, owner, and generated name.
7. Undo once if it landed incorrectly.

A flow node positioned near another node is not necessarily connected. A widget drawn inside a rectangle is not necessarily a child of that container. The tree or connector is the evidence.

## Data workflow

### Create an entity

1. Select **Data**.
2. Expand **Database**.
3. Right-click **Database** and choose **Add Entity**.
4. Rename the entity.
5. Select it and verify its properties.

### Add attributes

1. Expand the entity.
2. Add one attribute at a time.
3. Set its name and data type.
4. Configure mandatory, default, length, precision, or delete behavior only when required.
5. For a foreign key, use the referenced entity identifier type.
6. Confirm the relationship appears in the model.

### Create an entity diagram

1. Right-click **Entity Diagrams** and add a diagram.
2. Rename and open it.
3. Drag the required entities onto the canvas.
4. Verify visible relationships.

The diagram visualizes the data model; it does not create a valid relationship when the foreign-key attribute is wrong.

### Create a structure

1. Right-click **Structures** and add a structure.
2. Rename it.
3. Add attributes individually or copy selected entity attributes when their shape is appropriate.
4. Review mandatory settings after copying.
5. Add nested record or list attributes deliberately.
6. Remove database-only fields that do not belong in an API or UI contract.

## Logic workflow

### Create a server action

1. Select **Logic** and expand **Server Actions**.
2. Check for an existing action.
3. Add and rename the server action.
4. Add input and output parameters.
5. Configure parameter names, data types, mandatory state, and defaults.
6. Double-click the action to open its flow.
7. Identify Start and End.
8. Add and configure one node at a time.
9. Connect each node and verify arrow direction.
10. Trace every branch from Start to an End or intentional exception path.

### Create a client action

First decide whether the action belongs globally, to a screen, or to a block. Select that owner before adding it. A screen event may create a new client action automatically; use an existing action instead when it already implements the requested behavior.

After creation, open the flow, configure nodes, verify event binding, and check every connector.

### Add an exception

1. Expand **Exceptions** and **All Exceptions**.
2. Right-click **User Exception**.
3. Add and rename the exception.
4. Build a reusable error handler only when the requirements call for one.
5. Wire handler or raise-exception paths explicitly.
6. Verify whether the exception is handled, converted, or re-raised.

### Build an action flow

For every new node:

1. Drag the node from the Toolbox.
2. Select the exact aggregate, action, assignment, condition, or exception behavior.
3. Configure arguments and expressions.
4. Connect the previous node to it.
5. Connect it forward or deliberately leave it pending while visible.
6. Verify connector arrows and branches.
7. Check TrueChange before adding the next complex section.

Arrange flows so branches remain readable. Do not leave overlapping nodes or crossing connectors that hide the execution order.

## Dependency workflow

1. Determine which producer owns the required public element.
2. Open **Manage Dependencies** from the relevant context.
3. Select the producer on the left.
4. Select only the required actions, entities, structures, or roles on the right.
5. Apply once and wait for refresh.
6. Verify the imported element appears under the expected reference.

Do not select every dependency to make an error disappear. Do not install a Forge component without user authorization.

## Exposed REST API workflow

1. Under **Logic**, locate exposed REST APIs in **Integrations**.
2. Add or select the intended API.
3. Right-click the API and add a REST API method.
4. Set method name, URL path, and HTTP method.
5. Add input parameters and set `Receive In` to body, URL, query, or header as required.
6. Add output parameters and set their data types.
7. Double-click the method to open its flow.
8. Build the implementation one node at a time.
9. Assign a response on every success path.
10. Map errors to intentional status codes and response bodies.

Generated documentation is available only after publish. Ask before publishing or opening an external test client.

## Consumed REST API workflow

1. Expand **Integrations**.
2. Right-click **REST** and choose **Consume REST API**.
3. Confirm the OpenAPI or Swagger URL belongs to the intended environment.
4. Choose single or multiple methods.
5. Select only methods required by the task.
6. Complete the import and wait for generated actions and structures.
7. Inspect the generated request and response types.
8. Add response handlers only under the correct consumed API.

Never paste private endpoints, credentials, or tokens into a public report.

## Timer workflow

1. Select **Logic** and expand **Timers**.
2. Check whether the timer already exists.
3. Right-click **Timers**, add a timer, and rename it.
4. Configure schedule, priority, and timeout only as required.
5. Open the timer action.
6. Build its server-side flow one node at a time.
7. Add explicit exception handling for external calls.
8. Verify loops, waits, retries, and exit conditions.
9. Confirm database commits and idempotency expectations.

Do not manually run or publish a timer without explicit authorization.

## Interface workflow

### Create a screen

1. Select **Interface**.
2. Expand the intended UI flow, such as `MainFlow`.
3. Right-click the flow and choose **Add Screen**.
4. Choose the requested template or an empty screen.
5. Rename the screen.
6. Configure roles and input parameters before adding navigation.

### Add local variables and actions

1. Right-click the exact screen.
2. Add local variables and configure their types.
3. Add screen-scoped client actions.
4. Build each action flow.
5. Bind lifecycle events to the intended action.

### Use placeholders

Common placeholders include `Title`, `Actions`, and `MainContent`.

1. Open the screen and widget tree.
2. Select the placeholder by name.
3. Add outer containers or adaptive columns first.
4. Add labels, text, expressions, inputs, icons, and buttons afterward.
5. Verify each widget's parent in the tree.

### Add a list

1. Drag a List into the intended parent.
2. Bind its source list.
3. Inspect the generated list item.
4. Build the row under the content placeholder.
5. Verify expressions use the current list record.

For a nested list, verify that the inner source comes from the current outer item.

### Add a form

1. Build the surrounding containers.
2. Add a Form.
3. Drag the intended record or structure into it when automatic generation is useful.
4. Verify every input binding.
5. Configure mandatory, enabled, visible, and width properties.
6. Replace an expression with an input only when the field is editable.
7. Bind Add, Save, Update, and Cancel buttons to the correct actions.
8. Validate before calling a service or server action.

### Add widget events

1. Select the widget.
2. Locate On Click, On Change, or the relevant event.
3. Select an existing action when appropriate.
4. Create a new client action only when necessary.
5. Verify the event points to the intended action.

### Edit a menu

1. Open the Menu block and widget tree.
2. Locate the page-links or navigation placeholder.
3. Add links and submenus in the requested order.
4. Set each destination explicitly.
5. Enclose role-restricted menu content in the correct condition.
6. Test both authorized and unauthorized users when required.

## Validation workflow

Check TrueChange after each logical unit of work. For every new error:

1. Read the full message.
2. Identify the owning element.
3. Open that element.
4. Check missing arguments, expressions, types, sources, destinations, or connectors.
5. Fix one root cause.
6. Wait for revalidation.
7. Re-read the entire error list.

Do not assume downstream errors cleared. Do not hide or ignore warnings without understanding them.

## Runtime testing

Use the smallest test that proves the requested behavior:

- data model: inspect relationships or use authorized disposable records;
- server action: invoke it through an existing caller or endpoint;
- REST method: test success and relevant failure cases;
- timer: inspect configuration and monitoring before any authorized run;
- screen: test navigation, empty state, valid input, invalid input, and relevant roles.

Do not use irreversible production data for testing.

## Publish workflow

Editing does not authorize publishing.

Immediately before **1-Click Publish**:

1. Summarize the elements changed.
2. Report errors and warnings.
3. Ask for confirmation unless the current request explicitly includes publishing.
4. Click publish once.
5. Wait for upload, compilation, deployment, and final status.
6. Report the actual final status.

If publishing fails, capture the visible error and stop. Do not repeatedly republish unchanged work.

## Recovery workflow

### Wrong click or drag

1. Stop immediately.
2. Identify the accidental model change.
3. Use Undo once only when the mistake is isolated and recent.
4. Verify the unwanted change disappeared.
5. Ask before manually deleting or reverting when Undo could affect other work.

### Missing element

1. Confirm the active module and main tab.
2. Expand the correct folder and clear filters.
3. Search for a suffixed or generated name.
4. Check references when another module owns it.
5. Do not create a duplicate until the ambiguity is resolved.

### Repeated visual failure

After two failed attempts:

1. stop;
2. capture the current UI and visible error;
3. explain the attempted interaction;
4. ask the user to reposition the UI, complete that step manually, or allow MCP instead.

## Completion checklist

A task is complete only when:

- every requested element exists under the correct parent;
- names and properties match the requirement;
- entity relationships and data types are correct;
- every action path has valid connectors;
- parameters and outputs are assigned correctly;
- screen widgets are under the intended placeholders and containers;
- events reference the intended actions;
- no new TrueChange errors remain;
- requested runtime behavior has been tested;
- publish was performed only when authorized and its final status was verified;
- remaining uncertainty is reported clearly.

## Final response format

Report:

1. the application and module touched;
2. the entities, actions, integrations, timers, screens, or widgets changed;
3. the final TrueChange state;
4. runtime tests performed and their results;
5. whether publishing occurred and its status;
6. anything still unverified or requiring the user.

Keep the report factual. Do not claim success from clicks alone.
