
# CWLDefaultTypedConditional (Schema)

`ogc.cwl.v1_2_1.CWLDefaultTypedConditional` *v1.2.1*

Validates that a `default` value, if given alongside a
`type`, actually matches that declared type (e.g. a `default` for `type: boolean` must be a JSON
boolean, one for an `enum` type must be one of its `symbols`, one for `File`/`Directory` must be a
literal file/directory object). Limits itself to data literals and arrays; nested or multi-type
`type` definitions validate against `Any` instead of being over-constrained.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Validate that the 'default' value, if specified, is of same type as the CWL 'type'.
This avoids over-accepting anything that does not match the intended type.
However, validation limits itself to data literals and arrays.
Nested type and multi-type definitions will validate against 'Any'.

## Examples

### String default matching a string type
A `string`-typed input whose `default` is a plain string literal, adapted from
[`paramref_arguments_inputs.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/paramref_arguments_inputs.cwl).
The `string` branch of the conditional requires `default` to be a JSON string.

#### json
```json
{
  "type": "string",
  "default": "z"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/context.jsonld",
  "type": "string",
  "default": "z"
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .

[] sld:default "z" ;
    sld:type <https://example.org/string> .


```


### File default matching a File type
A `File`-typed input whose `default` is a literal File object, adapted from
[`bwa-mem-tool.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/bwa-mem-tool.cwl).
The `File`/`Directory` branch of the conditional requires `default` to match
[CWLDefaultLocation](bblocks://ogc.cwl.v1_2_1.CWLDefaultLocation).

#### json
```json
{
  "type": "File",
  "default": {
    "class": "File",
    "location": "args.py"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/context.jsonld",
  "type": "File",
  "default": {
    "class": "File",
    "location": "args.py"
  }
}
```

#### ttl
```ttl
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/args.py> a <https://example.org/File> .

[] sld:default <https://example.org/args.py> ;
    sld:type <https://example.org/File> .


```

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
      x-jsonld-id: https://w3id.org/cwl/salad#default
    type:
      $ref: '#/$defs/AnyType'
      x-jsonld-id: https://w3id.org/cwl/salad#type
      x-jsonld-type: '@vocab'
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
- $comment: Required string.
  if:
    properties:
      type:
        const: string
  then:
    properties:
      default:
        type: string
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
- $comment: Required boolean.
  if:
    properties:
      type:
        const: boolean
  then:
    properties:
      default:
        type: boolean
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
- $comment: Required enum.
  if:
    properties:
      symbols:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbols/schema.yaml
      type:
        const: enum
  then:
    properties:
      default:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbolValues/schema.yaml
        x-jsonld-id: https://w3id.org/cwl/salad#default
- $comment: Optional enum.
  if:
    properties:
      symbols:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbols/schema.yaml
      type:
        const: enum?
  then:
    properties:
      default:
        oneOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbolValues/schema.yaml
        - type: 'null'
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
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
        x-jsonld-id: https://w3id.org/cwl/salad#default
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultTypedConditional/schema.yaml)


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
    "sld": "https://w3id.org/cwl/salad#",
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

