
# CWLInputsDefinition (Schema)

`ogc.cwl.v1_2_1.CWLInputsDefinition` *v1.2.1*

All inputs available to the Application Package.

[*Status*](http://www.opengis.net/def/status): Under development

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
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "basename": "cwl:basename",
    "nameroot": "cwl:File/nameroot",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "cwl": "https://w3id.org/cwl/cwl#",
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

