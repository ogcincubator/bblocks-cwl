`StepInputExpressionRequirement` declares that a workflow (or workflow step) supports the
`valueFrom` field on a step's input mappings — see
[CWLWorkflowStepIn](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepIn) and the shared
`valueFrom` field it inherits from
[CWLWorkflowStepInputBase](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase). Without this
requirement, `valueFrom` must not be used.

When `valueFrom` is a CWL expression rather than a constant string, it is evaluated to compute
the step input's actual value. The expression is evaluated with `self` bound to the value(s)
from the input's `source` field (or `null` if there is no `source`), and with `inputs` bound to
the step's input object after `source` values, `default`, and scattering have been applied. This
lets a step input be derived or transformed from other values available to the step, rather than
only ever being copied straight from a `source`.
