
# CWLTypeRecordRef (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef` *v1.2.1*

An IRI with minimally a '{Record}' identifier to look for a schema definition locally or remotely.

The identifier resolution is performed accordingly to the specified reference and as described in
https://www.commonwl.org/v1.2/SchemaSalad.html#Identifier_resolution.


[*Status*](http://www.opengis.net/def/status): Under development

## Description

Avoid 'oneOf' conflict of valid strings between this CWL record reference and the generic CWL types.
## Examples

### Reference to a record type defined in an external schema document
A field `type` value referencing the `HelloType` record defined in an external
`SchemaDefRequirement` document, adapted from
[schemadef-tool.cwl](https://github.com/common-workflow-language/common-workflow-language/blob/main/v1.2/v1.2/schemadef-tool.cwl).

#### json
```json
"schemadef-type.yml#HelloType"

```


### Reference to a record type imported from another document
A field `type` value referencing the `readgroups_bam_file` record, adapted from
[schemadef_types_with_import-tool.cwl](https://github.com/common-workflow-language/common-workflow-language/blob/main/v1.2/v1.2/schemadef_types_with_import-tool.cwl).

#### json
```json
"schemadef_types_with_import_readgroup.yml#readgroups_bam_file"

```

## Schema

```yaml
$comment: Avoid 'oneOf' conflict of valid strings between this CWL record reference
  and the generic CWL types.
allOf:
- not:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/schema.yaml
- not:
    enum:
    - stdin
    type: string
- not:
    enum:
    - stdout
    type: string
- not:
    enum:
    - stderr
    type: string
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRefPattern/schema.yaml
description: 'An IRI with minimally a ''{Record}'' identifier to look for a schema
  definition locally or remotely.


  The identifier resolution is performed accordingly to the specified reference and
  as described in

  https://www.commonwl.org/v1.2/SchemaSalad.html#Identifier_resolution.

  '

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRef/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRef/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeRecordRef`

