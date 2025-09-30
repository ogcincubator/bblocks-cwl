
# CWLFileOnlyParameters (Schema)

`ogc.cwl.v1_2_1.CWLFileOnlyParameters` *v1.2.1*

CWLFileOnlyParameters

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$defs:
  CWLTypeRecordSecondaryFiles:
    oneOf:
    - $comment: Either an expression or the regex pattern directly.
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    - $ref: '#/$defs/CWLTypeRecordSecondaryFileSchema'
    - items:
        $comment: Either an expression or the regex pattern directly.
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      type: array
    - items:
        $ref: '#/$defs/CWLTypeRecordSecondaryFileSchema'
      type: array
  CWLTypeRecordSecondaryFileSchema:
    additionalProperties: false
    properties:
      pattern:
        $comment: Either an expression or the regex pattern directly.
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      required:
        oneOf:
        - type: boolean
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    required:
    - pattern
    type: object
properties:
  format:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    - items:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      type: array
  loadContents:
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#loadContents
  secondaryFiles:
    $ref: '#/$defs/CWLTypeRecordSecondaryFiles'
  streamable:
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#FieldBase/streamable
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/schema.yaml)


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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLFileOnlyParameters`

