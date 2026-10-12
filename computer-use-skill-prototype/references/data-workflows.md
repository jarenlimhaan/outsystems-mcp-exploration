# Data workflows

Use these workflows from the **Data** tab. Verify the active module before each operation.

## Add a database entity

1. Select **Data**.
2. Expand **Database**.
3. Check whether an entity with the requested name already exists.
4. Right-click **Database** and choose **Add Entity**.
5. Rename the new entity immediately.
6. Select the entity and verify its name and relevant properties.

## Add entity attributes

1. Expand the target entity.
2. Add one attribute at a time using the entity context menu or supported shortcut.
3. Set the attribute name and data type.
4. Set mandatory, default, length, decimal, or delete-rule properties only when required.
5. For a foreign key, choose the referenced entity identifier type rather than an arbitrary integer type.
6. Verify the attribute appears under the correct entity and that TrueChange recognizes the relationship.

## Add an entity diagram

1. Right-click **Entity Diagrams** and choose **Add Entity Diagram**.
2. Rename the diagram.
3. Open it and drag the required entities to the canvas.
4. Verify the diagram displays the intended relationships.

The diagram visualizes relationships; it does not replace correct foreign-key attributes.

## Add a structure

1. Expand **Structures**.
2. Right-click **Structures** and choose **Add Structure**.
3. Rename it immediately.
4. Add attributes individually, or copy selected attributes from an entity and paste them into the structure when the task requires the same shape.
5. Set each attribute's data type and mandatory state.
6. For a nested list, add an attribute whose type is the intended structure list.
7. Verify the structure contains only API or UI fields that belong in that contract.

Do not assume copied entity attributes should keep database-only identifiers, audit fields, or mandatory settings.

## Add a site property

1. Locate **Site Properties** in the Data tree.
2. Add the property and set name, data type, and default value.
3. Avoid putting credentials or secrets into public screenshots or source notes.
4. Verify logic references use the generated site-property name.

## Data completion check

- Open every new entity and structure once.
- Confirm generated identifiers and foreign keys.
- Check for duplicate or silently renamed attributes.
- Review TrueChange errors before starting logic that depends on the data model.
