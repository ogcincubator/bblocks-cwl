A CWL [`File`](https://www.commonwl.org/v1.2/Workflow.html#File) or
[`Directory`](https://www.commonwl.org/v1.2/Workflow.html#Directory) object identifies the resource it
represents through one of two mutually-non-exclusive but here XOR-constrained properties:

- `location` — an IRI that uniquely identifies the file or directory. Implementations must support the
  `file://` scheme and may support others (e.g. `http://`); a relative reference is resolved against the
  IRI of the document it appears in.
- `path` — a filesystem path available on the same host as the CWL runner (for inputs) or the runtime
  environment of a tool execution (for outputs).

This block requires exactly one of the two (`oneOf: [{required: [path]}, {required: [location]}]`),
alongside the mandatory `class` (`File` or `Directory`) and the optional `basename`/`nameroot`
properties, which name the file as staged on disk when it differs from the resource name.

It intentionally omits every other `File`/`Directory` field (`checksum`, `size`, `secondaryFiles`,
`listing`, `contents`, …) that only matter once a value is materialized at runtime — a `default` is a
literal value supplied at authoring time, not a description of a staged file, so those fields have no
role here.

This shape is reused across the register wherever a *literal* `File`/`Directory` default value is
needed: as a `default` value branch in [CWLDefault](bblocks://ogc.cwl.v1_2_1.CWLDefault), and as the
`default` shape enforced for `File`/`Directory`-typed inputs by
[CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional).
