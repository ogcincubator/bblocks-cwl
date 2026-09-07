
# CWLInputObject (Schema)

`ogc.cwl.v1_2_1.CWLInputObject` *v1.2.1*

The type/parameter definition of a single CWL input when expressed
as a nested object (as opposed to a bare type shorthand): `type`, an optional `inputBinding`, plus
the shared default-type-consistency and documentation fields.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This is the nested-object form used to describe a single input parameter of a `CommandLineTool` or
`Workflow` when more than a bare type is needed. It is one of the value shapes accepted for an entry
of the map form of [CWLInputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLInputsDefinition) — the identifier
itself comes from the surrounding map key rather than from a property on this object (contrast with
[CWLInputItem](bblocks://ogc.cwl.v1_2_1.CWLInputItem), the list-form entry, which carries its own `id`).

At minimum a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) is required, specifying the valid type(s) of
data that may be assigned to the parameter. Beyond that, this object may declare:

- an [InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding), describing how the parameter's value is
  turned into a command line argument (position, prefix, item separator, etc.);
- a `default` value, applied when the parameter is missing from the input object or explicitly `null`,
  before any expressions (such as `valueFrom`) are evaluated — its shape is cross-checked against the
  declared `type` (see [CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional));
- documentation fields (`doc`, `label`) shared with other CWL elements
  (see [CWLDocumentation](bblocks://ogc.cwl.v1_2_1.CWLDocumentation)).

A process is ready to run once every required input parameter is associated with a concrete value; the
input parameters' schemas are also what a runner or UI uses to validate — or build a form for — the
input object supplied at invocation time.

## Examples

### File input with command-line binding
A single required `File` input, positioned on the command line, adapted from the
`reference` input of the CWL `binding-test.cwl` conformance test.

#### json
```json
{
  "type": "File",
  "inputBinding": {
    "position": 2
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/context.jsonld",
  "type": "File",
  "inputBinding": {
    "position": 2
  }
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] cwl:inputBinding [ ns1:position 2 ] ;
    sld:type cwl:File .


```


### Optional numeric input with a default
An optional integer input with a default value used when the parameter is omitted from
the input object. The `default` value's type must be consistent with the declared `type`.

#### json
```json
{
  "type": "int?",
  "default": 10,
  "doc": "Threshold value used to filter results"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/context.jsonld",
  "type": "int?",
  "default": 10,
  "doc": "Threshold value used to filter results"
}
```

#### ttl
```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] rdfs:comment "Threshold value used to filter results" ;
    sld:default 10 ;
    sld:type <https://example.org/int> .


```

## Schema

```yaml
$defs:
  CWLInputObjectBase:
    additionalProperties: {}
    properties:
      inputBinding:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/schema.yaml
        additionalProperties: {}
        x-jsonld-id: https://w3id.org/cwl/cwl#inputBinding
      type:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
    required:
    - type
    type: object
allOf:
- $ref: '#/$defs/CWLInputObjectBase'
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml
summary: CWL type definition with parameters.
title: CWLInputObject
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "inputBinding": {
      "@context": {
        "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
        "position": "cwl:CommandLineBinding/position",
        "prefix": "cwl:CommandLineBinding/prefix",
        "shellQuote": "cwl:CommandLineBinding/shellQuote",
        "valueFrom": "cwl:valueFrom"
      },
      "@id": "cwl:inputBinding"
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
    "default": {
      "@context": {
        "basename": "cwl:basename",
        "class": "@type",
        "location": "@id",
        "nameroot": "cwl:File/nameroot",
        "path": {
          "@id": "cwl:path",
          "@type": "@id"
        }
      },
      "@id": "sld:default"
    },
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLInputObject`

