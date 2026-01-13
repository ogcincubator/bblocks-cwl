
# CWLTypeRecordArray (Schema)

`ogc.cwl.v1_2_1.CWLTypeRecordArray` *v1.2.1*

CWLTypeRecordArray

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
properties:
  items:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
  type:
    enum:
    - array
    type: string
required:
- type
- items
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordArray/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeRecordArray/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLTypeRecordArray`

