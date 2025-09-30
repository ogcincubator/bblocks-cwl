
# CWLWorkflowStepOut (Schema)

`ogc.cwl.v1_2_1.CWLWorkflowStepOut` *v1.2.1*

Mapping of Workflow step inputs to nested CWL tool definitions inputs or outputs.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: Mapping of Workflow step inputs to nested CWL tool definitions inputs
  or outputs.
items:
  oneOf:
  - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
  - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepId/schema.yaml
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepOut/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepOut/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLWorkflowStepOut`

