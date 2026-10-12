# Verification and recovery

Apply this reference to every visual Service Studio task.

## Evidence after each operation

Accept an action as successful only when at least one stable signal confirms it:

- a new tree item appears under the correct parent;
- a property retains its value after re-selection;
- a widget appears under the correct widget-tree node;
- a flow connector visibly joins the intended source and target;
- TrueChange removes the corresponding error;
- a publish tab reports successful completion;
- runtime testing produces the requested behavior.

A changed screenshot alone is not proof when the underlying model relationship remains ambiguous.

## Recover from a wrong click or drag

1. Stop immediately; do not continue building on the mistake.
2. Identify exactly what changed in the tree or canvas.
3. Use Undo once when the accidental action is recent and isolated.
4. Verify the unwanted element or property change disappeared.
5. If Undo would affect unrelated work, ask the user before deleting or manually reverting.

Never use repeated blind Undo commands.

## Recover from a missing element

1. Confirm the correct main tab and parent folder are open.
2. Clear tree search or filters if present.
3. Check whether Service Studio generated a suffixed or slightly different name.
4. Check references when the element should come from another module.
5. Refresh dependencies only with user authorization.
6. Do not create a replacement until duplicate risk is resolved.

## Recover from TrueChange errors

1. Read the full error text and identify its owner.
2. Open that exact element.
3. Check missing types, arguments, expressions, connectors, sources, and destinations.
4. Fix one root cause and wait for revalidation.
5. Re-read the error list rather than assuming all downstream messages cleared.

## Runtime verification

Use the smallest test that proves the requested behavior:

- entity work: inspect the model or create a disposable test record when authorized;
- server action: exercise it through an existing caller or test endpoint;
- REST method: verify method, URL, body, response, and failure case;
- timer: verify configuration and use monitoring only when running it is authorized;
- screen: test navigation, empty state, valid input, invalid input, and role restrictions relevant to the request.

Do not insert real credentials, personal information, or irreversible production data merely to test a workflow.

## Retry limit

After two failed attempts at the same visual interaction:

1. stop repeating it;
2. capture the current UI state and visible error;
3. explain what was attempted and what changed;
4. ask the user to reposition the UI, perform the interaction, or allow a semantic MCP alternative.

## Final report

Report:

- module and element names changed;
- validation state;
- whether runtime testing occurred;
- whether publishing occurred and its final status;
- anything that remains visually or behaviorally unverified.
