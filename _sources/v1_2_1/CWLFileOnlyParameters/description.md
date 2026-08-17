These four fields only have meaning when the `type` (or `items`, for arrays) of the input/output
parameter they belong to resolves to `File`; on any other type they are meaningless and should be
absent. Applying them is enforced separately by
[CWLFileOnlyParametersConditional](bblocks://ogc.cwl.v1_2_1.CWLFileOnlyParametersConditional), which
uses an `if`/`then`/`else` conditional on the parameter's `type`/`items` to require this schema when
`File` is detected and forbid these properties otherwise. The directory-typed counterparts —
`loadListing` (see [LoadListingRequirement](bblocks://ogc.cwl.v1_2_1.LoadListingRequirement)) — are
covered separately by
[CWLDirectoryOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters).

- **`format`** — the IRI of a concept node (preferably from an ontology) representing the file's
  content format/media type, or a CWL expression that evaluates to one. Reasoning about format
  compatibility is done by checking that an input file's format is the same as, `owl:equivalentClass`
  of, or `rdfs:subClassOf` the format required by the input parameter.
- **`secondaryFiles`** — one or more patterns (or expressions) describing additional files or
  directories that must be staged alongside the primary file, such as an index file or an external
  reference. A plain (non-expression) pattern string is applied to the primary file's path: a
  trailing `?` marks the secondary file optional, and each leading `^` strips one file extension from
  the path before the remainder of the pattern is appended.
- **`streamable`** — when `true`, indicates the file is read or written sequentially without seeking,
  which an implementation may use to decide whether it can stream the file's contents through a named
  pipe. Defaults to `false`.
- **`loadContents`** — when `true`, requires the file to be a UTF-8 text file of 64 KiB or smaller;
  the implementation reads its entire contents into the `contents` field of the File object so it is
  available to expressions. It is a fatal error if the file exceeds the 64 KiB limit.
