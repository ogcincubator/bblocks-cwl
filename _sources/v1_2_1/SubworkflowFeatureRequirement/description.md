To specify a nested workflow as part of a workflow step, `SubworkflowFeatureRequirement` must be
specified in the workflow or workflow step `requirements`. When present, it indicates that the
workflow platform must support another `Workflow` document as the value of the `run` field of a
[CWLWorkflowStepObject](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepObject), rather than only a
`CommandLineTool` or `ExpressionTool`.

It is a fatal error if a workflow directly or indirectly invokes itself as a subworkflow — recursive
workflows are not allowed.

`SubworkflowFeatureRequirement` is one of the two standard extensions to core workflow semantics, the
other being `ScatterFeatureRequirement`.
