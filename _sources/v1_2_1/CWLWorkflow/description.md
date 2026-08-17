A workflow describes a set of steps and the dependencies between those steps. When a step
produces output that will be consumed by a second step, the first step is a dependency of the
second step.

When there is a dependency, the workflow engine must execute the preceding step and wait for it
to successfully produce output before executing the dependent step. If two steps are defined in
the workflow graph that are not directly or indirectly dependent, these steps are independent,
and may execute in any order or execute concurrently. A workflow is complete when all steps have
been executed.

Dependencies between parameters are expressed using the `source` field on workflow step input
parameters and the `outputSource` field on workflow output parameters. The `source` field on
each workflow step input parameter expresses the data links that contribute to the value of the
step input parameter (the "sink"). A workflow step can only begin execution when every data link
connected to a step has been fulfilled. The `outputSource` field on each workflow output
parameter expresses the data links that contribute to the value of the workflow output parameter;
workflow execution cannot complete successfully until every data link connected to an output
parameter has been fulfilled.

A completed step must result in one of `success`, `temporaryFailure` or `permanentFailure`
states. An implementation may choose to retry a step execution which resulted in
`temporaryFailure`, and may choose to either continue running other steps of a workflow or
terminate immediately upon `permanentFailure`. If any step of a workflow execution results in
`permanentFailure`, the workflow status is `permanentFailure`; if one or more steps result in
`temporaryFailure` and all other steps complete `success` or are not executed, the workflow
status is `temporaryFailure`; if all workflow steps are executed and complete with `success`,
the workflow status is `success`.

This block represents a complete, top-level CWL Workflow document as it appears at the root of a
`.cwl` file: the `class: Workflow` discriminator
([CWLWorkflowClass](bblocks://ogc.cwl.v1_2_1.CWLWorkflowClass)) and workflow structure — `inputs`,
`outputs`, `steps`, `requirements` and `hints`
([CWLWorkflowBase](bblocks://ogc.cwl.v1_2_1.CWLWorkflowBase)) — combined with the document-level
fields that only apply at the root of a CWL file: `cwlVersion`
([CWLVersion](bblocks://ogc.cwl.v1_2_1.CWLVersion)), metadata
([CWLMetadata](bblocks://ogc.cwl.v1_2_1.CWLMetadata)), and documentation
([CWLDocumentation](bblocks://ogc.cwl.v1_2_1.CWLDocumentation)). A workflow's own steps can, in
turn, nest another workflow definition in their `run` field — see
[CWLWorkflowStepObject](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepObject) — which reuses
`CWLWorkflowClass` and `CWLWorkflowBase` but not `CWLVersion`, since `cwlVersion` is only declared
once, at the document root.

[ScatterFeatureRequirement](bblocks://ogc.cwl.v1_2_1.ScatterFeatureRequirement) and
[SubworkflowFeatureRequirement](bblocks://ogc.cwl.v1_2_1.SubworkflowFeatureRequirement) are
available as standard extensions to core workflow semantics, letting a step fan out over an array
input or run a nested workflow, respectively.
