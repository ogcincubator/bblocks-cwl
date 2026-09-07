
# SchemaDefRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.SchemaDefRequirement` *v1.2.1*

An array of named `enum`/`record` type definitions available
for reuse via IRI reference from `inputs`/`outputs` type fields. Definitions are processed in the
order listed, so later definitions may refer to earlier ones.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Type definitions may only use the `enum` and `record` forms — see
[type-system/CWLTypeEnum](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeEnum) and
[type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema) — or an
array whose `items` resolve to one of those, via
[type-system/CWLTypeRecordArray](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordArray). Each entry
may instead be an [CWLImport](bblocks://ogc.cwl.v1_2_1.CWLImport) (`$import`) directive, so a set of
shared type definitions can be kept in a separate file and reused across multiple CWL documents rather
than repeated inline.

Once declared here, a definition can be referenced by IRI from an `inputs`/`outputs` `type` field
elsewhere in the document, instead of being written out inline at the point of use.

## Examples

### Inline enum and record type definitions
Declares a reusable `Species` enum and a `SequencingRun` record whose `organism` field refers
back to it by name; `SequencingRun` can then be used as a `type` elsewhere in the document's
`inputs`/`outputs`.

#### json
```json
{
  "class": "SchemaDefRequirement",
  "types": [
    {
      "type": "enum",
      "name": "Species",
      "symbols": ["human", "mouse", "zebrafish"]
    },
    {
      "type": "record",
      "name": "SequencingRun",
      "fields": {
        "organism": "Species",
        "reads": {
          "type": "File"
        }
      }
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/context.jsonld",
  "class": "SchemaDefRequirement",
  "types": [
    {
      "type": "enum",
      "name": "Species",
      "symbols": [
        "human",
        "mouse",
        "zebrafish"
      ]
    },
    {
      "type": "record",
      "name": "SequencingRun",
      "fields": {
        "organism": "Species",
        "reads": {
          "type": "File"
        }
      }
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#SchemaDefRequirement/> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/SequencingRun> sld:fields <https://example.org/reads>,
        "Species" ;
    sld:type <https://example.org/record> .

<https://example.org/Species> sld:type <https://example.org/enum> .

<https://example.org/reads> sld:type cwl:File .

[] a <https://example.org/SchemaDefRequirement> ;
    ns1:types <https://example.org/SequencingRun>,
        <https://example.org/Species> .


```


### Type definitions shared via $import
Instead of writing type definitions inline, an entry can be an `$import` directive pointing to
a file holding a shared set of `enum`/`record` definitions reused across multiple CWL documents.

#### json
```json
{
  "class": "SchemaDefRequirement",
  "types": [
    {
      "$import": "types/readgroup.yml"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/context.jsonld",
  "class": "SchemaDefRequirement",
  "types": [
    {
      "$import": "types/readgroup.yml"
    }
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SchemaDefRequirement/> .

[] a <https://example.org/SchemaDefRequirement> ;
    ns1:types [ ] .


```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - SchemaDefRequirement
    type: string
    x-jsonld-id: '@type'
  types:
    items:
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeEnum/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordSchema/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordArray/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#SchemaDefRequirement/types
required:
- types
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "types": {
      "@context": {
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
        "items": {
          "@id": "sld:items",
          "@type": "@vocab"
        }
      },
      "@id": "cwl:SchemaDefRequirement/types"
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
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/SchemaDefRequirement`

