
# SubworkflowFeatureRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.SubworkflowFeatureRequirement` *v1.2.1*

Indicates that the 'Workflow' must support nested workflows in the 'run' field of 'WorkflowStep'.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

To specify a nested workflow as part of a workflow step, `SubworkflowFeatureRequirement` must be
specified in the workflow or workflow step `requirements`. When present, it indicates that the
workflow platform must support another `Workflow` document as the value of the `run` field of a
[CWLWorkflowStepObject](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepObject), rather than only a
`CommandLineTool` or `ExpressionTool`.

It is a fatal error if a workflow directly or indirectly invokes itself as a subworkflow — recursive
workflows are not allowed.

`SubworkflowFeatureRequirement` is one of the two standard extensions to core workflow semantics, the
other being `ScatterFeatureRequirement`.

## Examples

### Enabling subworkflows on a Workflow
A `Workflow` declares `SubworkflowFeatureRequirement` so that one of its steps may use
another `Workflow` document as its `run` process, i.e. a nested subworkflow.

#### json
```json
{
  "class": "SubworkflowFeatureRequirement"
}

```

## Schema

```yaml
additionalProperties: false
description: Indicates that the 'Workflow' must support nested workflows in the 'run'
  field of 'WorkflowStep'.
properties:
  class:
    description: CWL requirement class specification.
    enum:
    - SubworkflowFeatureRequirement
    type: string
title: SubworkflowFeatureRequirement
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SubworkflowFeatureRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SubworkflowFeatureRequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/SubworkflowFeatureRequirement`

