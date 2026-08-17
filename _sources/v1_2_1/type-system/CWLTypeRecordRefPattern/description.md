This pattern matches values of the form:

```
[<document-path-or-URL>]#<RecordName>
```

The document part is optional and, when present, may be a bare relative path (e.g.
`schema.yml`), an absolute local path, or a full `http(s)://`/`ftp(s)://` URL. What follows
the `#` is the record's local name (e.g. `HelloType`). A bare `#RecordName` with no document
part is also valid, and resolves relative to the current document.

This is the syntax used to reference a `record` type defined out-of-line — most commonly one
declared in a `SchemaDefRequirement` document (via [`$import`](https://www.commonwl.org/v1.2/SchemaSalad.html#Import))
rather than inlined with [bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema].
[bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef] narrows this pattern further, excluding
the strings that are already reserved as CWL primitive/array type keywords or as the
`stdin`/`stdout`/`stderr` literals, so a plain type reference is never ambiguous with a named
record reference.
