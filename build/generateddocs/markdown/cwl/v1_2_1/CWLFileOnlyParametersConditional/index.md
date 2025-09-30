
# CWLFileOnlyParametersConditional (Schema)

`ogc.cwl.v1_2_1.CWLFileOnlyParametersConditional` *v1.2.1*

Parameters that are only valid when 'type' or 'items' evaluates to 'File'.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Explicitly disallow these parameters when non-File type is detected.
Otherwise, validate their schema definitions according to what is permitted.

## Schema

```yaml
$comment: 'Explicitly disallow these parameters when non-File type is detected.

  Otherwise, validate their schema definitions according to what is permitted.

  '
description: Parameters that are only valid when 'type' or 'items' evaluates to 'File'.
else:
  not:
    properties:
      format: {}
      loadContents: {}
      secondaryFiles: {}
      streamable: {}
  x-jsonld-extra-terms:
    loadContents: https://w3id.org/cwl/cwl#loadContents
    streamable: https://w3id.org/cwl/cwl#FieldBase/streamable
if:
  oneOf:
  - $comment: Single required or optional 'File'.
    properties:
      type:
        enum:
        - File
        - File?
        - File[]
        - File[]?
  - $comment: Array of required or optional 'File'.
    items:
      oneOf:
      - type: object
        properties:
          type:
            enum:
            - File
            - File?
      - contains:
          properties:
            type:
              enum:
              - File
              - File?
        type: array
    type: array
then:
  $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/schema.yaml
  x-jsonld-extra-terms:
    loadContents: https://w3id.org/cwl/cwl#loadContents
    streamable: https://w3id.org/cwl/cwl#FieldBase/streamable
type: object
x-jsonld-extra-terms:
  loadContents: https://w3id.org/cwl/cwl#loadContents
  streamable: https://w3id.org/cwl/cwl#FieldBase/streamable
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParametersConditional/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParametersConditional/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParametersConditional/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLFileOnlyParametersConditional`

