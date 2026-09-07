This is the nested-object form used to describe a single input parameter of a `CommandLineTool` or
`Workflow` when more than a bare type is needed. It is one of the value shapes accepted for an entry
of the map form of [CWLInputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLInputsDefinition) — the identifier
itself comes from the surrounding map key rather than from a property on this object (contrast with
[CWLInputItem](bblocks://ogc.cwl.v1_2_1.CWLInputItem), the list-form entry, which carries its own `id`).

At minimum a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) is required, specifying the valid type(s) of
data that may be assigned to the parameter. Beyond that, this object may declare:

- an [InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding), describing how the parameter's value is
  turned into a command line argument (position, prefix, item separator, etc.);
- a `default` value, applied when the parameter is missing from the input object or explicitly `null`,
  before any expressions (such as `valueFrom`) are evaluated — its shape is cross-checked against the
  declared `type` (see [CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional));
- documentation fields (`doc`, `label`) shared with other CWL elements
  (see [CWLDocumentation](bblocks://ogc.cwl.v1_2_1.CWLDocumentation)).

A process is ready to run once every required input parameter is associated with a concrete value; the
input parameters' schemas are also what a runner or UI uses to validate — or build a form for — the
input object supplied at invocation time.
