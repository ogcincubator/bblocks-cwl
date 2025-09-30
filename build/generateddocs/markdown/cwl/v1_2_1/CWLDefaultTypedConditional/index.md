
# CWLDefaultTypedConditional (Schema)

`ogc.cwl.v1_2_1.CWLDefaultTypedConditional` *v1.2.1*

CWLDefaultTypedConditional

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Validate that the 'default' value, if specified, is of same type as the CWL 'type'.
This avoids over-accepting anything that does not match the intended type.
However, validation limits itself to data literals and arrays.
Nested type and multi-type definitions will validate against 'Any'.

## Schema

```yaml
$comment: 'Validate that the ''default'' value, if specified, is of same type as the
  CWL ''type''.

  This avoids over-accepting anything that does not match the intended type.

  However, validation limits itself to data literals and arrays.

  Nested type and multi-type definitions will validate against ''Any''.

  '
$defs:
  AnyType:
    type:
    - boolean
    - number
    - string
    - array
    - object
allOf:
- $comment: Object structure with minimally 'type' and 'default'. Otherwise, no point
    to continue testing.
  properties:
    default:
      $ref: '#/$defs/AnyType'
    type:
      $ref: '#/$defs/AnyType'
  required:
  - type
  type: object
- $comment: Explicit null.
  if:
    properties:
      type:
        const: 'null'
  then:
    properties:
      default:
        type: 'null'
- $comment: Required string.
  if:
    properties:
      type:
        const: string
  then:
    properties:
      default:
        type: string
- $comment: Optional string.
  if:
    properties:
      type:
        const: string?
  then:
    properties:
      default:
        type:
        - string
        - 'null'
- $comment: Required boolean.
  if:
    properties:
      type:
        const: boolean
  then:
    properties:
      default:
        type: boolean
- $comment: Optional boolean.
  if:
    properties:
      type:
        enum:
        - double?
        - float?
        - int?
        - integer?
        - long?
  then:
    properties:
      default:
        type:
        - number
        - 'null'
- $comment: Required numeric.
  if:
    properties:
      type:
        enum:
        - double
        - float
        - int
        - integer
        - long
  then:
    properties:
      default:
        type: number
- $comment: Optional numeric.
  if:
    properties:
      type:
        enum:
        - double?
        - float?
        - int?
        - integer?
        - long?
  then:
    properties:
      default:
        type:
        - number
        - 'null'
- $comment: Required enum.
  if:
    properties:
      symbols:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeSymbols/schema.yaml
      type:
        const: enum
  then:
    properties:
      default:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeSymbolValues/schema.yaml
- $comment: Optional enum.
  if:
    properties:
      symbols:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeSymbols/schema.yaml
      type:
        const: enum?
  then:
    properties:
      default:
        oneOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeSymbolValues/schema.yaml
        - type: 'null'
- $comment: Required File or Directory.
  if:
    properties:
      type:
        enum:
        - Directory
        - File
  then:
    properties:
      default:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.yaml
- $comment: Optional File or Directory.
  if:
    properties:
      type:
        enum:
        - Directory?
        - File?
  then:
    properties:
      default:
        oneOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.yaml
        - type: 'null'
- $comment: Required array of string.
  if:
    oneOf:
    - properties:
        type:
          const: string[]
    - properties:
        items:
          const: string
        type:
          const: array
  then:
    properties:
      default:
        items:
          type: string
        type: array
- $comment: Required array of boolean.
  if:
    oneOf:
    - properties:
        type:
          const: boolean[]
    - properties:
        items:
          const: boolean
        type:
          const: array
  then:
    properties:
      default:
        items:
          type: boolean
        type: array
- $comment: Required array of numeric.
  if:
    oneOf:
    - properties:
        type:
          enum:
          - double[]
          - float[]
          - int[]
          - integer[]
          - long[]
    - properties:
        items:
          enum:
          - double
          - float
          - int
          - integer
          - long
        type:
          const: array
  then:
    properties:
      default:
        items:
          type: number
        type: array
- $comment: Required anything (single).
  if:
    properties:
      type:
        const: Any
  then:
    properties:
      default:
        $comment: Match anything.
        $ref: '#/$defs/AnyType'
- $comment: Required array of anything.
  if:
    properties:
      type:
        const: Any[]
  then:
    properties:
      default:
        $comment: Match anything as long as under array.
        items:
          $ref: '#/$defs/AnyType'
        type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "basename": "cwl:basename",
    "nameroot": "cwl:File/nameroot",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLDefaultTypedConditional`

