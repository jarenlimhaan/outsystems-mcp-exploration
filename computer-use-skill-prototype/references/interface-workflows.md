# Interface workflows

Use these workflows from the **Interface** tab. Verify whether the module is Reactive Web, Mobile, or Traditional Web before following UI-specific options.

## Add a screen

1. Expand the intended UI flow, commonly `MainFlow` in a small Reactive app.
2. Check whether the requested screen already exists.
3. Right-click the UI flow and choose **Add Screen**.
4. Select the requested template, or an empty screen when the task requires manual construction.
5. Rename the screen immediately.
6. Configure access roles and input parameters before linking navigation.

## Add screen variables and actions

1. Right-click the exact screen.
2. Add local variables one at a time and set their types.
3. Add screen-scoped client actions by name.
4. Open each action and build its flow.
5. Verify lifecycle events such as OnInitialize, OnReady, or data loading call the correct actions.

## Work with placeholders and containers

Common layout placeholders include `Title`, `Actions`, and `MainContent`.

1. Open the screen and widget tree.
2. Select the target placeholder by name.
3. Add outer containers or layout widgets before text, expressions, inputs, icons, and buttons.
4. After every drag, verify the widget appears under the correct parent in the tree.
5. Rename important containers when later instructions refer to them.

## Add a list

1. Drag a **List** widget into the intended placeholder or container.
2. Bind its source by dragging the relevant list data into the List or selecting the source property.
3. Inspect the generated list item and expressions.
4. Build the row hierarchy under the list item's content placeholder.
5. Verify all expressions reference the current list item rather than an unrelated variable.

Nested lists require extra care: confirm the inner list source belongs to the current outer record.

## Add a form

1. Add the outer container structure.
2. Drag the record or structure into the target form when generation is desired.
3. Confirm every generated input is bound to the intended field.
4. Set mandatory, enabled, visible, width, and label properties.
5. Replace generated expression widgets with inputs only when the field should be editable.
6. Bind Save, Add, Update, and Cancel buttons to the intended client actions.
7. Verify validation occurs before the service or server call.

## Add widget events

1. Select the widget.
2. Locate the event property such as On Click or On Change.
3. Select an existing action when one already implements the behavior.
4. Choose **New Client Action** only when a new action is actually required.
5. Open the resulting action and verify the event points to it.

## Edit a menu

1. Open the menu block and widget tree.
2. Locate the page-links placeholder or equivalent navigation container.
3. Add links and submenus in the requested order.
4. Set each destination explicitly.
5. For role-gated items, enclose or condition the correct menu subtree and verify the condition.
6. Test navigation using both authorized and unauthorized users when required.

## Interface completion check

- Widget hierarchy matches the intended layout.
- Lists and forms use the correct source variables.
- Events reference the intended client actions.
- Inputs have correct mandatory and enabled states.
- Role-based visibility and screen access are both configured where needed.
- The screen remains usable at the target viewport size.
- No new TrueChange errors remain.
