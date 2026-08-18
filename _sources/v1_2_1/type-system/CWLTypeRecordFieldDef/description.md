The definition of one field of an inline [type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema):
its `type` (any [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType)) and, depending on how the record's
`fields` are written, an optional or required `name`.

**`name` is conditionally required.** This schema alone only requires `type` — `name` is left
optional here because the same field-definition shape is reused for both forms a record's `fields`
can take:

- In the **map form** of `fields` (an object keyed by field name), the field's name is already
  given by the map key, so repeating it as a `name` property would be redundant, and this schema
  leaves it optional.
- In the **list form** of `fields` (an array of field definitions), there is no key to imply the
  name, so `name` must be present on each item. That requirement is layered on top of this schema —
  not built into it — by [type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema),
  which combines this schema with a sibling `required: [name]` constraint specifically for the
  list form. This keeps the field-definition schema reusable across both forms instead of forking
  it into two near-identical copies.

Because a record field's `type` may itself resolve to `File` or `Directory` (directly, as an
optional/array variant such as `File?`/`Directory[]`, or as part of a type union), this schema also
conditionally admits the File-only parameters
([CWLFileOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLFileOnlyParameters): `format`, `loadContents`,
`secondaryFiles`, `streamable`) and the Directory-only parameter
([CWLDirectoryOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters): `loadListing`) —
via `if`/`then`/`else` conditional logic built directly into this schema, which disallows them
outright for non-matching types.
