
# CWLOutputsDefinition (Schema)

`ogc.cwl.v1_2_1.CWLOutputsDefinition` *v1.2.1*

All outputs produced by the Application Package.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The `outputs` field of a CWL `Process` (a `CommandLineTool`, `Workflow`, or `ExpressionTool`),
defining the parameters representing the output of the process. It is used both to generate the
process's output object and to validate it. CWL allows this field to be written in either of two
equivalent shapes, plus an `$import` escape hatch:

- **List form** (`CWLOutputList`) — an array of
  [CWLOutputItem](bblocks://ogc.cwl.v1_2_1.CWLOutputItem) objects, each carrying its own `id`
  alongside `type` and the other output properties. This is the more verbose but unambiguous form.
- **Map form** (`CWLOutputMap`) — an object whose keys are the output identifiers and whose values
  are either a bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand (e.g. `"File"`), a full
  [CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject), or a `stdout`/`stderr` shorthand (see
  [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) /
  [CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)). This is the more compact form
  typically seen in hand-written CWL documents.
- An `$import` directive (see [CWLImport](bblocks://ogc.cwl.v1_2_1.CWLImport)), pointing to an
  external file that supplies the outputs definition. The schema explicitly excludes documents that
  would otherwise also match the map form from matching as a plain map, to avoid the two branches
  overlapping on a generic `$import`-only mapping key.

Only one of these three shapes may be used for a given `outputs` field; a CWL processor accepts
whichever the document uses and treats them as equivalent.

## Examples

### Outputs as a list
Outputs written in list form, where each entry is a
[CWLOutputItem](bblocks://ogc.cwl.v1_2_1.CWLOutputItem) with its own `id`.

#### json
```json
[
  {
    "id": "output_file",
    "type": "File",
    "outputBinding": {
      "glob": "output.txt"
    }
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/context.jsonld",
  "@graph": [
    {
      "id": "output_file",
      "type": "File",
      "outputBinding": {
        "glob": "output.txt"
      }
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/output_file> cwl:outputBinding [ ns1:glob "output.txt" ] ;
    sld:type cwl:File .


```


### Outputs as a map
The same outputs written in the more compact map form, keyed by output identifier. Values may
be a bare type shorthand, as with `classification` below, or a full
[CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject), as with `count_output`.

#### json
```json
{
  "count_output": {
    "type": "int",
    "outputSource": "step2/output"
  },
  "classification": "string"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/context.jsonld",
  "@graph": [
    {
      "id": "count_output",
      "type": "int",
      "outputSource": "step2/output"
    },
    {
      "id": "classification",
      "type": "string"
    }
  ]
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/classification> sld:type xsd:string .

<https://example.org/count_output> sld:type xsd:int .


```

## Schema

```yaml
description: All outputs produced by the Application Package.
$defs:
  CWLOutputList:
    description: Package outputs defined as items.
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/schema.yaml
    title: CWLOutputList
    type: array
  CWLOutputMap:
    additionalProperties:
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdOut/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    description: Package outputs defined as mapping.
    properties: {}
    required: []
    title: CWLOutputMap
    type: object
oneOf:
- $ref: '#/$defs/CWLOutputList'
- $comment: Avoid 'oneOf' conflict of generic mapping key strings as output identifier
    matching against '$import'.
  allOf:
  - $ref: '#/$defs/CWLOutputMap'
  - not:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
title: CWLOutputsDefinition

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "id": "@id",
    "outputBinding": {
      "@context": {
        "glob": "cwl:CommandOutputBinding/glob"
      },
      "@id": "cwl:outputBinding"
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
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputsDefinition`

