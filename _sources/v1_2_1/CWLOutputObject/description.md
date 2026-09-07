An output parameter of a `CommandLineTool` or `Workflow`, expressed as a nested object rather than
using the bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand. This is the value shape used
wherever an output is written as a mapping under its identifier — for example as an entry of a
[CWLOutputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLOutputsDefinition) expressed in map form — so the
identifier itself is carried externally as the map key rather than as a property of this object.

The `type` property (required) specifies the valid type(s) of data that may be assigned to the
output, following the same [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) type system used across CWL —
a primitive (`File`, `Directory`, `string`, ...), an array of a type, a nullable type, or an inline
record/enum schema.

The optional `outputBinding` property describes how the value of the output is generated or
extracted, typically by globbing files produced by the process on disk — see
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding). It is not required: `type: stdout`/`type:
stderr` outputs (see [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) and
[CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)) capture the process's standard streams
directly and need no `outputBinding` of their own.

`CWLOutputObject` also mixes in [CWLDocumentation](bblocks://ogc.cwl.v1_2_1.CWLDocumentation), so
`doc` and `label` may be used to document the parameter for humans and tooling.

The full CWL specification additionally defines `secondaryFiles`, `format`, and `streamable` on
output parameters (for describing companion files, the output's media type, and whether it may be
read as a stream). These are not modeled as explicit properties here, but the schema's open
`additionalProperties` still allows them to appear on an instance.
