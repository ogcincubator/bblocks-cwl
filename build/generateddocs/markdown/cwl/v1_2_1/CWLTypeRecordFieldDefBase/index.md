
# CWLTypeRecordFieldDefBase (Schema)

`ogc.cwl.v1_2_1.CWLTypeRecordFieldDefBase` *v1.2.1*

CWLTypeRecordFieldDefBase

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
properties:
  name:
    $comment: 'Required if list item. Otherwise, optional since it is the mapping
      key.

      This requirement is defined in ''CWLTypeRecordFieldsItem'' to allow reuse of
      this schema.

      '
    type: string
  type:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
required:
- type
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordFieldDefBase/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordFieldDefBase/schema.yaml)


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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordFieldDefBase/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLTypeRecordFieldDefBase`

