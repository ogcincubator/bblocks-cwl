
# StepInputExpressionRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.StepInputExpressionRequirement` *v1.2.1*

Indicates that the 'Workflow' must support the 'valueFrom' field of 'WorkflowStepInput'.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Enabling StepInputExpressionRequirement on a Workflow
A `Workflow` requirements entry that enables the use of `valueFrom` expressions on
workflow step inputs, letting a step input's value be computed rather than only ever
copied from its `source`.

#### json
```json
{
  "class": "StepInputExpressionRequirement"
}

```

## Schema

```yaml
additionalProperties: false
description: Indicates that the 'Workflow' must support the 'valueFrom' field of 'WorkflowStepInput'.
properties:
  class:
    description: CWL requirement class specification.
    enum:
    - StepInputExpressionRequirement
    type: string
title: StepInputExpressionRequirement
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/StepInputExpressionRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/StepInputExpressionRequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/StepInputExpressionRequirement`

