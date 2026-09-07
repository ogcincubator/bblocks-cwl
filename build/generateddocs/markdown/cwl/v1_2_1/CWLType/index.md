
# CWLType (Schema)

`ogc.cwl.v1_2_1.CWLType` *v1.2.1*

The set of types a CWL input or output parameter may declare: the CWL
primitive/File/Directory types, an inline enum, an inline record, a reference to a named type
(record or enum) defined elsewhere, an array of one of these, or an array combining several of
these (a type union).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

`CWLType` is the schema used everywhere a CWL document declares the `type` of an input parameter,
output parameter, or record field. A value conforming to `CWLType` is one of:

- a [CWLTypeDefinition](bblocks://ogc.cwl.v1_2_1.CWLTypeDefinition) string — a CWL primitive
  (`string`, `int`, `boolean`, ...), `File`, `Directory`, `Any`, or one of their `?` (nullable) or
  `[]` (array) suffixed forms;
- an inline enum schema (`type: enum` with a `symbols` list);
- an inline record schema (`type: record` with `fields`);
- a reference to a named record or enum type defined elsewhere in the document (an identifier/CURIE
  string, e.g. `"#MyRecord"`);
- an array of one of the above (`type: array` with an `items` schema), for a homogeneous array type;
- or a JSON array combining several of these alternatives, forming a **type union** — the field
  accepts a value matching any one of the listed types (schema-salad's "convenience" `type` array
  syntax, e.g. `type: [File, "null"]` for an optional `File`).

Because `enum` constraints intersect cleanly under JSON Schema's `allOf`, `CWLType` (together with
[CWLTypeDefinition](bblocks://ogc.cwl.v1_2_1.CWLTypeDefinition)) is this register's primary entry
point for **profiling** CWL type declarations — e.g. a platform that only wants to accept
`File`/`Directory`/`string`/`int`/`float` and arrays thereof, and reject `enum`/`record` types, can
narrow `CWLTypeDefinition`'s enum to that subset with a plain `allOf` profile, without having to
reconstruct any of the surrounding union/array machinery.

See also: [CWL Type](https://www.commonwl.org/v1.2/Workflow.html#CWLType) in the CWL specification.

## Examples

### Optional File parameter (type union)
A type union combining a plain type name with the special `"null"` type, the schema-salad
idiom for making a parameter optional (equivalent to the shorthand `File?`).

#### json
```json
["null", "File"]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": {
    "@list": [
      "null",
      "File"
    ]
  }
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value ( "null" "File" ) .


```


### Array of Files
An inline array type declaring a parameter that accepts a list of `File` values.

#### json
```json
{
  "type": "array",
  "items": "File"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/context.jsonld",
  "type": "array",
  "items": "File"
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .

[] sld:type <https://example.org/array> .


```

## Schema

```yaml
$defs:
  CWLTypeBase:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/schema.yaml
    - $ref: '#/$defs/CWLTypeArray'
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeEnum/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRef/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/schema.yaml
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
    "type": {
      "@id": "sld:type",
      "@type": "@vocab"
    },
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
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
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

