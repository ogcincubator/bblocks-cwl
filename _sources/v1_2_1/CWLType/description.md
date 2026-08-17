`CWLType` is the schema used everywhere a CWL document declares the `type` of an input parameter,
output parameter, or record field. A value conforming to `CWLType` is one of:

- a [CWLTypeDefinition](bblocks://ogc.cwl.v1_2_1.CWLTypeDefinition) string — a CWL primitive
  (`string`, `int`, `boolean`, ...), `File`, `Directory`, `Any`, or one of their `?` (nullable) or
  `[]` (array) suffixed forms;
- an inline enum schema (`type: enum` with a `symbols` list);
- an inline record schema (`type: record` with `fields`);
- a reference to a named record or enum type defined elsewhere in the document (an identifier/CURIE
  string, e.g. `"#MyRecord"`);
- an array of one of the above (`type: array` with an `items` schema), for a homogeneous array type;
- or a JSON array combining several of these alternatives, forming a **type union** — the field
  accepts a value matching any one of the listed types (schema-salad's "convenience" `type` array
  syntax, e.g. `type: [File, "null"]` for an optional `File`).

Because `enum` constraints intersect cleanly under JSON Schema's `allOf`, `CWLType` (together with
[CWLTypeDefinition](bblocks://ogc.cwl.v1_2_1.CWLTypeDefinition)) is this register's primary entry
point for **profiling** CWL type declarations — e.g. a platform that only wants to accept
`File`/`Directory`/`string`/`int`/`float` and arrays thereof, and reject `enum`/`record` types, can
narrow `CWLTypeDefinition`'s enum to that subset with a plain `allOf` profile, without having to
reconstruct any of the surrounding union/array machinery.

See also: [CWL Type](https://www.commonwl.org/v1.2/Workflow.html#CWLType) in the CWL specification.
