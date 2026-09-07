
# CWLTypeRecordFieldDef (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef` *v1.2.1*

The definition of a single field within an
inline CWL `record` type: its `type` and, for the list form of `fields`, its `name`. Also carries
the file-only and directory-only parameters (`format`, `secondaryFiles`, `loadListing`, ...), since a
record field's type can itself be File- or Directory-typed.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The definition of one field of an inline [type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema):
its `type` (any [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType)) and, depending on how the record's
`fields` are written, an optional or required `name`.

**`name` is conditionally required.** This schema alone only requires `type` — `name` is left
optional here because the same field-definition shape is reused for both forms a record's `fields`
can take:

- In the **map form** of `fields` (an object keyed by field name), the field's name is already
  given by the map key, so repeating it as a `name` property would be redundant, and this schema
  leaves it optional.
- In the **list form** of `fields` (an array of field definitions), there is no key to imply the
  name, so `name` must be present on each item. That requirement is layered on top of this schema —
  not built into it — by [type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema),
  which combines this schema with a sibling `required: [name]` constraint specifically for the
  list form. This keeps the field-definition schema reusable across both forms instead of forking
  it into two near-identical copies.

Because a record field's `type` may itself resolve to `File` or `Directory` (directly, as an
optional/array variant such as `File?`/`Directory[]`, or as part of a type union), this schema also
conditionally admits the File-only parameters
([CWLFileOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLFileOnlyParameters): `format`, `loadContents`,
`secondaryFiles`, `streamable`) and the Directory-only parameter
([CWLDirectoryOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters): `loadListing`) —
via `if`/`then`/`else` conditional logic built directly into this schema, which disallows them
outright for non-matching types.

## Examples

### File-typed field with secondary files
A field definition used in the list form of a record's `fields`, so `name` is required.
Because its `type` resolves to `File`, the File-only parameters `secondaryFiles` become
available.

#### json
```json
{
  "name": "ofoo",
  "type": "File",
  "secondaryFiles": ".idx"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/context.jsonld",
  "name": "ofoo",
  "type": "File",
  "secondaryFiles": ".idx"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/ofoo> cwl:secondaryFiles ".idx" ;
    sld:type cwl:File .


```


### Directory-typed field, map form
A field definition used inside the map form of a record's `fields` (so `name` is omitted —
it is implied by the map key). Because its `type` resolves to `Directory`, the
Directory-only `loadListing` parameter becomes available.

#### json
```json
{
  "type": "Directory",
  "loadListing": "deep_listing"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/context.jsonld",
  "type": "Directory",
  "loadListing": "deep_listing"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] cwl:loadListing "deep_listing" ;
    sld:type cwl:Directory .


```

## Schema

```yaml
allOf:
- properties:
    name:
      $comment: 'Required if list item. Otherwise, optional since it is the mapping
        key.

        This requirement is defined in ''CWLTypeRecordFieldsItem'' to allow reuse
        of this schema.

        '
      type: string
      x-jsonld-id: '@id'
    type:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      x-jsonld-id: https://w3id.org/cwl/salad#type
      x-jsonld-type: '@vocab'
  required:
  - type
  type: object
- $comment: 'Explicitly disallow these parameters when non-File type is detected.

    Otherwise, validate their schema definitions according to what is permitted.

    '
  description: Parameters that are only valid when 'type' or 'items' evaluates to
    'File'.
  else:
    properties:
      format:
        not: true
      loadContents:
        not: true
      secondaryFiles:
        not: true
      streamable:
        not: true
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
  type: object
- $comment: 'Explicitly disallow these parameters when non-Directory type is detected.

    Otherwise, validate their schema definitions according to what is permitted.

    '
  description: Parameters that are only valid when 'type' or 'items' evaluates to
    'Directory'.
  else:
    properties:
      loadListing:
        not: true
  if:
    oneOf:
    - $comment: Single required or optional 'Directory'.
      properties:
        type:
          enum:
          - Directory
          - Directory?
          - Directory[]
          - Directory[]?
    - $comment: Array of required or optional 'Directory'.
      items:
        oneOf:
        - type: object
          properties:
            type:
              enum:
              - Directory
              - Directory?
        - contains:
            properties:
              type:
                enum:
                - Directory
                - Directory?
            type: array
      type: array
  then:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/schema.yaml
  type: object
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "name": "@id",
    "type": {
      "@context": {
        "fields": {
          "@id": "sld:fields",
          "@container": "@id"
        }
      },
      "@id": "sld:type",
      "@type": "@vocab"
    },
    "format": {
      "@id": "cwl:format",
      "@type": "@id"
    },
    "loadContents": "cwl:loadContents",
    "secondaryFiles": "cwl:secondaryFiles",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "null": "sld:null",
    "boolean": "xsd:boolean",
    "int": "xsd:int",
    "integer": "xsd:int",
    "long": "xsd:long",
    "float": "xsd:float",
    "double": "xsd:double",
    "string": "xsd:string",
    "File": "cwl:File",
    "Directory": "cwl:Directory",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeRecordFieldDef`

