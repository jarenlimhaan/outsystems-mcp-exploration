# Logic workflows

Use these workflows from the **Logic** tab. Build flows one verified node at a time.

## Add a server action

1. Expand **Server Actions**.
2. Check whether the action already exists.
3. Right-click the intended folder or **Server Actions** and add a server action.
4. Rename it immediately.
5. Add input and output parameters from the action context menu.
6. Set parameter names, types, mandatory state, and defaults.
7. Double-click the action to open its flow.
8. Build the flow from Start toward End, configuring and connecting each node before adding the next.
9. Trace every success and exception path.

## Add a client action

Client actions may be global or scoped to a screen or block.

1. Select the intended owner before adding the action.
2. Right-click the owner and choose the client-action command, or create it from a widget event when that is the requested behavior.
3. Rename it and add parameters or local variables.
4. Open the action flow and verify every connector.
5. Confirm the screen event points to the intended action rather than a duplicate generated action.

## Add a user exception and handler

1. Expand **Exceptions**, then **All Exceptions**.
2. Right-click **User Exception** and add a new exception.
3. Rename it and verify its properties.
4. For a reusable handler, add a server action with the required error-details or status input.
5. Wire exception paths explicitly and verify whether exceptions are handled or re-raised.

## Manage a dependency

1. Right-click the relevant system, producer, or server-action area and open **Manage Dependencies**.
2. Select the correct producer on the left.
3. Select only the required public elements on the right.
4. Apply once and wait for the refresh.
5. Confirm the imported element appears under the correct reference.

Never select all dependencies merely because it is faster.

## Expose a REST API

1. Locate exposed REST APIs under **Integrations**.
2. Add or select the intended API.
3. Right-click the API and add a REST API method.
4. Set the method name, URL path, and HTTP method.
5. Add input and output parameters from the method context menu.
6. For inputs, verify `Receive In` matches body, URL, query, or header semantics.
7. Double-click the method and implement the flow.
8. Confirm the response is assigned on every successful path and errors map to intentional status codes.

Opening generated API documentation and testing with an external client requires the module to be published; obtain publish authorization first.

## Consume a REST API

1. Expand **Integrations**.
2. Right-click **REST** and choose **Consume REST API**.
3. Choose the single-method or multiple-method flow required by the task.
4. Enter the verified Swagger or OpenAPI URL.
5. Select only the required methods.
6. Finish the import and wait for generated structures and actions.
7. Inspect generated request/response structures before using them.
8. Configure response handlers only after confirming the correct consumed API.

## Add a timer

1. Expand **Timers**.
2. Check for an existing timer with the requested name.
3. Right-click **Timers** and add a timer.
4. Rename it immediately.
5. Set its schedule, priority, and timeout only when the task specifies them.
6. Open the timer action and build its flow as a server-side action.
7. Ensure loops, waits, external calls, and exception handling cannot run indefinitely.
8. Verify database commits and retry behavior are intentional.

Do not manually run a timer or publish its schedule without explicit authorization.

## Logic completion check

- Every input is consumed or intentionally unused.
- Every output is assigned on all relevant paths.
- Every node has the intended incoming and outgoing connector.
- Exception paths terminate predictably.
- External actions come from the intended dependency.
- No new TrueChange errors remain.
