
# CWLTypeRecordSchema (Schema)

`ogc.cwl.v1_2_1.CWLTypeRecordSchema` *v1.2.1*

CWLTypeRecordSchema

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$defs:
  CWLTypeRecordFieldsMap:
    additionalProperties:
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordFieldDef/schema.yaml
    type: object
  CWLTypeRecordFieldsList:
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordFieldsItem/schema.yaml
    type: array
properties:
  fields:
    oneOf:
    - $ref: '#/$defs/CWLTypeRecordFieldsMap'
    - $ref: '#/$defs/CWLTypeRecordFieldsList'
  name:
    type: string
  type:
    enum:
    - record
    type: string
required:
- type
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordSchema/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordSchema/schema.yaml)


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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordSchema/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLTypeRecordSchema`

