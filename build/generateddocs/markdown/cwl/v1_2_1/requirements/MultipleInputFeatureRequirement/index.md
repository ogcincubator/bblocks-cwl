
# MultipleInputFeatureRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.MultipleInputFeatureRequirement` *v1.2.1*

Indicates that the 'Workflow' must support multiple inbound data links listed in the 'source'
field of 'WorkflowStepInput'.


[*Status*](http://www.opengis.net/def/status): Under development

## Description

Without this requirement, a [`WorkflowStepInput`](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase)'s
`source` field must reference a single upstream parameter. Declaring
`MultipleInputFeatureRequirement` lifts that restriction, allowing `source` to list an array of
upstream parameters whose values are merged into the sink input.

The merge behavior is controlled by the sink input's `linkMerge` field
(see [`LinkMergeMethod`](bblocks://ogc.cwl.v1_2_1.LinkMergeMethod)): `merge_nested` (the default)
wraps the value from each link into one entry of a list, while `merge_flattened` concatenates
array-valued links into a single flat list. If `linkMerge` is left unset and `source` lists more
than one upstream parameter, `merge_nested` applies; if `source` lists only one, the input takes
that single value directly, unwrapped.

## Examples

### Enabling multiple inbound data links
Adapted from the CWL conformance test `count-lines7-wf.cwl`: a `Workflow` declares
`MultipleInputFeatureRequirement` so that a step input's `source` field
(see [CWLWorkflowStepInputBase](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase)) can list
more than one upstream parameter, merged according to `linkMerge`.

#### json
```json
{
  "class": "MultipleInputFeatureRequirement"
}

```

## Schema

```yaml
additionalProperties: false
description: 'Indicates that the ''Workflow'' must support multiple inbound data links
  listed in the ''source''

  field of ''WorkflowStepInput''.

  '
properties:
  class:
    description: CWL requirement class specification.
    enum:
    - MultipleInputFeatureRequirement
    type: string
title: MultipleInputFeatureRequirement
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/MultipleInputFeatureRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/MultipleInputFeatureRequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/MultipleInputFeatureRequirement`

