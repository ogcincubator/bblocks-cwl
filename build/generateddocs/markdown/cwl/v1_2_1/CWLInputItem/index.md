
# CWLInputItem (Schema)

`ogc.cwl.v1_2_1.CWLInputItem` *v1.2.1*

Input specification. Note that multiple formats are supported and
not all specification variants or parameters are presented here. Please refer
to official CWL documentation for more details (https://www.commonwl.org).


[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### File input, list form
A required `File` input with a command-line binding, adapted from the `reference` input
of the CWL `binding-test.cwl` conformance test's list-form `inputs`.

#### json
```json
{
  "id": "reference",
  "type": "File",
  "inputBinding": {
    "position": 2
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/context.jsonld",
  "id": "reference",
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

<https://example.org/reference> cwl:inputBinding [ ns1:position 2 ] ;
    sld:type cwl:File .


```


### Optional string input with documentation
An optional string input, documented with `doc` and given a `default` that is used when
the input is omitted.

#### json
```json
{
  "id": "message",
  "type": "string?",
  "default": "hello world",
  "doc": "Message to print"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/context.jsonld",
  "id": "message",
  "type": "string?",
  "default": "hello world",
  "doc": "Message to print"
}
```

#### ttl
```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/message> rdfs:comment "Message to print" ;
    sld:default "hello world" ;
    sld:type <https://example.org/string> .


```

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml
additionalProperties: {}
description: 'Input specification. Note that multiple formats are supported and

  not all specification variants or parameters are presented here. Please refer

  to official CWL documentation for more details (https://www.commonwl.org).

  '
properties:
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
    description: Identifier of the CWL input.
    x-jsonld-id: '@id'
  inputBinding:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#inputBinding
  type:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputStdIn/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/salad#type
    x-jsonld-type: '@vocab'
required:
- type
- id
title: Input
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
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
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "id": "@id",
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
    "cwl": "https://w3id.org/cwl/cwl#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLInputItem`

