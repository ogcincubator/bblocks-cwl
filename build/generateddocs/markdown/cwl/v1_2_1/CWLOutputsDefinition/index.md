
# CWLOutputsDefinition (Schema)

`ogc.cwl.v1_2_1.CWLOutputsDefinition` *v1.2.1*

All outputs produced by the Application Package.

[*Status*](http://www.opengis.net/def/status): Under development

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
    "outputBinding": "cwl:outputBinding",
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "glob": "cwl:CommandOutputBinding/glob",
    "cwl": "https://w3id.org/cwl/cwl#",
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

