
# CWLWorkflowBase (Schema)

`ogc.cwl.v1_2_1.CWLWorkflowBase` *v1.2.1*

CWLWorkflowBase

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$defs:
  CWLWorkflowStepMap:
    additionalProperties:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepObject/schema.yaml
    type: object
  CWLWorkflowStepList:
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepItem/schema.yaml
    type: array
properties:
  hints:
    $comment: Technically a different subset, but lots of redefinitions to be done.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/schema.yaml
  inputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.yaml
  outputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.yaml
  requirements:
    $comment: Technically a different subset, but lots of redefinitions to be done.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirements/schema.yaml
  steps:
    oneOf:
    - $ref: '#/$defs/CWLWorkflowStepMap'
    - $ref: '#/$defs/CWLWorkflowStepList'
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowBase/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowBase/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "when": "cwl:when",
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowBase/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLWorkflowBase`

