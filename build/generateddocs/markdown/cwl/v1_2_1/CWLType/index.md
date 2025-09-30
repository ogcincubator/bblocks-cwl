
# CWLType (Schema)

`ogc.cwl.v1_2_1.CWLType` *v1.2.1*

CWLType

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$defs:
  CWLTypeBase:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/schema.yaml
    - $ref: '#/$defs/CWLTypeArray'
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeEnum/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordRef/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordSchema/schema.yaml
    title: CWLTypeBase
  CWLTypeList:
    items:
      $ref: '#/$defs/CWLTypeBase'
    summary: Combination of allowed CWL types.
    title: CWLTypeList
    type: array
  CWLTypeArray:
    additionalProperties: {}
    properties:
      items:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      type:
        enum:
        - array
        example: array
        title: type
        type: string
    required:
    - type
    - items
    summary: CWL type as list of items.
    title: CWLTypeArray
    type: object
oneOf:
- $ref: '#/$defs/CWLTypeBase'
- $ref: '#/$defs/CWLTypeList'
title: CWL Type

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLType`

