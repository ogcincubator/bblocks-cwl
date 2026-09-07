
# CWLTypeRecordArray (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeRecordArray` *v1.2.1*

A CWL type definition for an array whose elements
are all of the same, further-specified CWL type: `type: array` plus an `items` type.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Array of File inputs
A CWL `CommandLineTool` input declared as an array of `File` items, adapted from the
`reads` input of [bwa-mem-tool.cwl](https://github.com/common-workflow-language/common-workflow-language/blob/main/v1.2/v1.2/bwa-mem-tool.cwl).

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
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/context.jsonld",
  "type": "array",
  "items": "File"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] sld:items cwl:File ;
    sld:type <https://example.org/array> .


```


### Array of integer values
A CWL input declared as an array of `int` items, adapted from the `min_std_max_min`
input of [bwa-mem-tool.cwl](https://github.com/common-workflow-language/common-workflow-language/blob/main/v1.2/v1.2/bwa-mem-tool.cwl).

#### json
```json
{
  "type": "array",
  "items": "int"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/context.jsonld",
  "type": "array",
  "items": "int"
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] sld:items xsd:int ;
    sld:type <https://example.org/array> .


```

## Schema

```yaml
properties:
  items:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/salad#items
    x-jsonld-type: '@vocab'
  type:
    enum:
    - array
    type: string
    x-jsonld-id: https://w3id.org/cwl/salad#type
    x-jsonld-type: '@vocab'
required:
- type
- items
type: object
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "items": {
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
        "name": "@id"
      },
      "@id": "sld:items",
      "@type": "@vocab"
    },
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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeRecordArray`

