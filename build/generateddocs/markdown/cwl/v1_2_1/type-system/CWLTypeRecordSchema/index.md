
# CWLTypeRecordSchema (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema` *v1.2.1*

An inline CWL `record` type definition: `type:
record`, an optional `name`, and its `fields`, given either as a map keyed by field name or as a
list of field definitions (each of which must then carry its own `name`).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

A CWL `record` is schema-salad's structured type: a set of named `fields`, each with its own
`type`, that together describe a compound value (analogous to a `struct` or an object type).
Records may be declared inline wherever a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) is expected —
e.g. as the `type` of a `CommandLineTool` input or output — or given a `name` and referenced from
elsewhere by an IRI (see [type-system/CWLTypeRecordRef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef)).

The `fields` themselves — each a [type-system/CWLTypeRecordFieldDef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef) —
can be written in two equivalent forms:

- **Map form**: an object whose keys are the field names and whose values are each field's type
  (either a bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType), or a full field definition when
  additional parameters such as `format` or `secondaryFiles` are needed). The field's `name` is
  implied by its key and must not be repeated inside the value.
- **List form**: an array of field definitions, each of which must carry its own `name` property
  since there is no map key to imply it.

Both forms are accepted anywhere a `record`'s `fields` are expected; this block's schema expresses
that as a `oneOf` between the two shapes.

## Examples

### Record with fields given as a map
A `record` input type whose `fields` are written in map form: each key is a field name and
each value is that field's `type`, adapted from CWL's `record-output.cwl` conformance test.

#### json
```json
{
  "type": "record",
  "name": "irec",
  "fields": {
    "ifoo": "File",
    "ibar": "File"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/context.jsonld",
  "type": "record",
  "name": "irec",
  "fields": {
    "ifoo": "File",
    "ibar": "File"
  }
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/irec> sld:fields "File" ;
    sld:type <https://example.org/record> .


```


### Record with fields given as a list
The same kind of `record` type, but with `fields` written in list form — here each field
definition must carry its own `name`, since there is no map key to imply it.

#### json
```json
{
  "type": "record",
  "name": "a",
  "fields": [
    {
      "name": "b",
      "type": "int"
    },
    {
      "name": "c",
      "type": "int"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/context.jsonld",
  "type": "record",
  "name": "a",
  "fields": [
    {
      "name": "b",
      "type": "int"
    },
    {
      "name": "c",
      "type": "int"
    }
  ]
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/a> sld:fields <https://example.org/b>,
        <https://example.org/c> ;
    sld:type <https://example.org/record> .

<https://example.org/b> sld:type xsd:int .

<https://example.org/c> sld:type xsd:int .


```

## Schema

```yaml
$defs:
  CWLTypeRecordFieldsMap:
    additionalProperties:
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/schema.yaml
    type: object
  CWLTypeRecordFieldsList:
    items:
      allOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordFieldDef/schema.yaml
      - required:
        - name
    type: array
properties:
  fields:
    oneOf:
    - $ref: '#/$defs/CWLTypeRecordFieldsMap'
    - $ref: '#/$defs/CWLTypeRecordFieldsList'
    x-jsonld-id: https://w3id.org/cwl/salad#fields
    x-jsonld-container: '@id'
  name:
    type: string
    x-jsonld-id: '@id'
  type:
    enum:
    - record
    type: string
    x-jsonld-id: https://w3id.org/cwl/salad#type
    x-jsonld-type: '@vocab'
required:
- type
type: object
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "fields": {
      "@context": {
        "format": {
          "@id": "cwl:format",
          "@type": "@id"
        },
        "loadContents": "cwl:loadContents",
        "secondaryFiles": "cwl:secondaryFiles",
        "streamable": "cwl:FieldBase/streamable",
        "loadListing": "cwl:loadListing"
      },
      "@id": "sld:fields",
      "@container": "@id"
    },
    "name": "@id",
    "type": {
      "@id": "sld:type",
      "@type": "@vocab"
    },
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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeRecordSchema`

