
# CWLOutputObject (Schema)

`ogc.cwl.v1_2_1.CWLOutputObject` *v1.2.1*

The type/parameter definition of a single CWL output when
expressed as a nested object (as opposed to a bare type shorthand): `type`, an optional
`outputBinding`, plus the shared documentation fields.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

An output parameter of a `CommandLineTool` or `Workflow`, expressed as a nested object rather than
using the bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand. This is the value shape used
wherever an output is written as a mapping under its identifier — for example as an entry of a
[CWLOutputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLOutputsDefinition) expressed in map form — so the
identifier itself is carried externally as the map key rather than as a property of this object.

The `type` property (required) specifies the valid type(s) of data that may be assigned to the
output, following the same [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) type system used across CWL —
a primitive (`File`, `Directory`, `string`, ...), an array of a type, a nullable type, or an inline
record/enum schema.

The optional `outputBinding` property describes how the value of the output is generated or
extracted, typically by globbing files produced by the process on disk — see
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding). It is not required: `type: stdout`/`type:
stderr` outputs (see [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) and
[CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)) capture the process's standard streams
directly and need no `outputBinding` of their own.

`CWLOutputObject` also mixes in [CWLDocumentation](bblocks://ogc.cwl.v1_2_1.CWLDocumentation), so
`doc` and `label` may be used to document the parameter for humans and tooling.

The full CWL specification additionally defines `secondaryFiles`, `format`, and `streamable` on
output parameters (for describing companion files, the output's media type, and whether it may be
read as a stream). These are not modeled as explicit properties here, but the schema's open
`additionalProperties` still allows them to appear on an instance.

## Examples

### File output located with a glob pattern
A `File` output whose value is retrieved from disk after the tool runs, using
`outputBinding.glob` to locate it.

#### json
```json
{
  "type": "File",
  "outputBinding": {
    "glob": "output.txt"
  },
  "doc": "The output file produced by the tool."
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/context.jsonld",
  "type": "File",
  "outputBinding": {
    "glob": "output.txt"
  },
  "doc": "The output file produced by the tool."
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] rdfs:comment "The output file produced by the tool." ;
    cwl:outputBinding [ ns1:glob "output.txt" ] ;
    sld:type cwl:File .


```


### Array of Directory outputs
An output whose type is an array of `Directory`, matching every directory produced under
`outdir/`.

#### json
```json
{
  "type": "Directory[]",
  "outputBinding": {
    "glob": "outdir/*"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/context.jsonld",
  "type": "Directory[]",
  "outputBinding": {
    "glob": "outdir/*"
  }
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] cwl:outputBinding [ ns1:glob "outdir/*" ] ;
    sld:type <https://example.org/Directory[]> .


```

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml
- additionalProperties: {}
  properties:
    outputBinding:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/OutputBinding/schema.yaml
      x-jsonld-id: https://w3id.org/cwl/cwl#outputBinding
    type:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      x-jsonld-id: https://w3id.org/cwl/salad#type
      x-jsonld-type: '@vocab'
  required:
  - type
  summary: CWL type definition with parameters.
  title: CWLOutputObject
  type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputObject/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputObject`

