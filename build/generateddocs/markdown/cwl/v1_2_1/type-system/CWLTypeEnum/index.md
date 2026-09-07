
# CWLTypeEnum (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeEnum` *v1.2.1*

An inline CWL `enum` type definition: `type: enum` plus its
allowed `symbols`.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Inline enum type for a species input
An inline `enum` type definition restricting a `CommandLineTool` input field to a fixed set of
species names, adapted from the CWL conformance test `anon_enum_inside_array.cwl`.

#### json
```json
{
  "type": "enum",
  "symbols": ["homo_sapiens", "mus_musculus"]
}

```


### Inline enum type fixing a requirement's class
CWL also uses inline `enum` types to pin a `class` field to a single permissible value, as seen
in `InlineJavascriptRequirement`.

#### json
```json
{
  "type": "enum",
  "name": "InlineJavascriptRequirement_class",
  "symbols": ["cwl:InlineJavascriptRequirement"]
}

```

## Schema

```yaml
additionalProperties: {}
properties:
  symbols:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbols/schema.yaml
  type:
    enum:
    - enum
    example: enum
    title: type
    type: string
required:
- type
- symbols
summary: CWL type as enum of values.
title: CWLTypeEnum
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeEnum/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeEnum/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeEnum`

