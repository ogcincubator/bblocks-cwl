
# CWLOutputItem (Schema)

`ogc.cwl.v1_2_1.CWLOutputItem` *v1.2.1*

Output specification. Note that multiple formats are supported
and not all specification variants or parameters are presented here. Please
refer to official CWL documentation for more details (https://www.commonwl.org).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

The item shape used when a [CWLOutputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLOutputsDefinition) is
written in list form: one entry per output parameter, each carrying its own `id` explicitly. This is
the counterpart to [CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject), which is used instead
when outputs are written as a map keyed by identifier — there, the identifier is the map key rather
than a property, so `id` does not appear on the value itself.

Both `id` and `type` are required. `type` may be a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType), or the
`stdout`/`stderr` shorthand (see [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) /
[CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)) for capturing a process's standard
streams. The optional `outputBinding` describes how to extract the output's value — see
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding).

## Examples

### File output item with an explicit identifier
A single output entry as used in the list form of a `CWLOutputsDefinition`, carrying its own
`id` alongside `type` and `outputBinding`.

#### json
```json
{
  "id": "output_file",
  "type": "File",
  "outputBinding": {
    "glob": "output.txt"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/context.jsonld",
  "id": "output_file",
  "type": "File",
  "outputBinding": {
    "glob": "output.txt"
  }
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


### Standard output stream captured as an output item
An output item using the `stdout` shorthand `type`, redirecting the command's standard output
stream to this output without an explicit `outputBinding`.

#### json
```json
{
  "id": "result",
  "type": "stdout"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/context.jsonld",
  "id": "result",
  "type": "stdout"
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/result> sld:type <https://example.org/stdout> .


```

## Schema

```yaml
additionalProperties: {}
description: 'Output specification. Note that multiple formats are supported

  and not all specification variants or parameters are presented here. Please

  refer to official CWL documentation for more details (https://www.commonwl.org).

  '
properties:
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
    description: Identifier of the CWL output.
    x-jsonld-id: '@id'
  outputBinding:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/OutputBinding/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#outputBinding
  type:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdOut/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/salad#type
    x-jsonld-type: '@vocab'
required:
- type
- id
title: CWLOutputItem
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/schema.yaml)


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
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputItem`

