
# CWLInputsDefinition (Schema)

`ogc.cwl.v1_2_1.CWLInputsDefinition` *v1.2.1*

All inputs available to the Application Package.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Defines the input parameters of a `CommandLineTool` or `Workflow`. A process is ready to run when all
of its required input parameters are associated with concrete values; the schema declared for each
parameter is used both to validate a submitted input object and to build a user interface for
constructing one. If an input parameter is missing from the input object it must be treated as `null`
(or as the parameter's `default`, if one is provided) for the purposes of validation and expression
evaluation.

CWL accepts two equivalent notations for this field, reflected in this schema as a `oneOf`:

- a **list** of [CWLInputItem](bblocks://ogc.cwl.v1_2_1.CWLInputItem) objects, each carrying its own
  `id`; or
- a **map** keyed by input identifier, whose values are either a bare
  [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand, a nested
  [CWLInputObject](bblocks://ogc.cwl.v1_2_1.CWLInputObject), an input redirected from standard input
  (`CWLInputStdIn`), or an `$import` directive (`CWLImport`) pulling in externally-defined inputs.

The map form is additionally constrained to not itself look like an `$import` directive, since a
generic mapping of identifier strings to values could otherwise be ambiguous with the `$import` key.

## Examples

### Inputs as a list
Inputs declared as a list of identified items, adapted from the CWL `binding-test.cwl`
conformance test.

#### json
```json
[
  {
    "id": "reference",
    "type": "File",
    "inputBinding": {
      "position": 2
    }
  },
  {
    "id": "reads",
    "type": {
      "type": "array",
      "items": "File"
    },
    "inputBinding": {
      "position": 3,
      "prefix": "-XXX"
    }
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/context.jsonld",
  "@graph": [
    {
      "id": "reference",
      "type": "File",
      "inputBinding": {
        "position": 2
      }
    },
    {
      "id": "reads",
      "type": {
        "type": "array",
        "items": "File"
      },
      "inputBinding": {
        "position": 3,
        "prefix": "-XXX"
      }
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/reads> cwl:inputBinding [ ns1:position 3 ;
            ns1:prefix "-XXX" ] ;
    sld:type [ sld:type <https://example.org/array> ] .

<https://example.org/reference> cwl:inputBinding [ ns1:position 2 ] ;
    sld:type cwl:File .


```


### Inputs as a map
Inputs declared as a map keyed by identifier, adapted from the CWL
`scatter-valueFrom-tool.cwl` conformance test. Map values may be a nested input object, or
a bare type shorthand as with `count-lines17-wf.cwl`'s single-input form.

#### json
```json
{
  "message": {
    "type": "string",
    "inputBinding": {
      "position": 1
    }
  },
  "scattered_message": {
    "type": "string",
    "inputBinding": {
      "position": 2
    }
  },
  "file1": "File"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/context.jsonld",
  "@graph": [
    {
      "id": "message",
      "type": "string",
      "inputBinding": {
        "position": 1
      }
    },
    {
      "id": "scattered_message",
      "type": "string",
      "inputBinding": {
        "position": 2
      }
    },
    {
      "id": "file1",
      "type": "File"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/file1> sld:type cwl:File .

<https://example.org/message> cwl:inputBinding [ ns1:position 1 ] ;
    sld:type xsd:string .

<https://example.org/scattered_message> cwl:inputBinding [ ns1:position 2 ] ;
    sld:type xsd:string .


```

## Schema

```yaml
description: All inputs available to the Application Package.
$defs:
  CWLInputMap:
    additionalProperties:
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLType/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputObject/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputStdIn/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    description: Package inputs defined as mapping.
    properties: {}
    required: []
    title: CWLInputMap
    type: object
  CWLInputList:
    description: Package inputs defined as items.
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputItem/schema.yaml
    title: CWLInputList
    type: array
oneOf:
- $ref: '#/$defs/CWLInputList'
- $comment: Avoid 'oneOf' conflict of generic mapping key strings as input identifier
    matching against '$import'.
  allOf:
  - $ref: '#/$defs/CWLInputMap'
  - not:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
title: CWLInputsDefinition

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.yaml)


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
    "cwl": "https://w3id.org/cwl/cwl#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLInputsDefinition`

