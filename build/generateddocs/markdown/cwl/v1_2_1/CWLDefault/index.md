
# CWLDefault (Schema)

`ogc.cwl.v1_2_1.CWLDefault` *v1.2.1*

Default value of input if not provided for task execution.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The `default` field of an [`InputParameter`](https://www.commonwl.org/v1.2/Workflow.html#InputParameter)
supplies the value to use for that input when it is missing from the input object, or when its value
is `null`. Default values are applied before evaluating any expressions that depend on the input
(e.g. a dependent `valueFrom` field).

This block enumerates the shapes a `default` value may take:

- a single literal — number, boolean or string (`AnyLiteralType`);
- an array of such literals (`AnyLiteralList`);
- a [`CWLDefaultLocation`](bblocks://ogc.cwl.v1_2_1.CWLDefaultLocation) object — a literal `File` or
  `Directory` identified by `path`/`location` — for File- or Directory-typed inputs;
- an arbitrary JSON object that does *not* declare a `File`/`Directory` `class` (`CWLDefaultObject`),
  covering `record`-typed defaults; or
- an array of such objects.

The `CWLDefaultObject` branch's `not` constraint exists purely to keep it from swallowing what is
actually a `File`/`Directory` default, so that shape is unambiguously matched by
[`CWLDefaultLocation`](bblocks://ogc.cwl.v1_2_1.CWLDefaultLocation) instead. This block does not check
the default's shape against the input's declared `type` — see
[CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional) for that.

## Examples

### Literal string default
A plain string literal used as the `default` value of a `string`-typed input parameter,
adapted from [`paramref_arguments_inputs.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/paramref_arguments_inputs.cwl).

#### json
```json
"z"

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": "z"
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value "z" .


```


### File default identified by location
A `default` value for a `File`-typed input, given as a literal File object identified by
`location`, adapted from
[`bwa-mem-tool.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/bwa-mem-tool.cwl).

#### json
```json
{
  "class": "File",
  "location": "args.py"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/context.jsonld",
  "class": "File",
  "location": "args.py"
}
```

#### ttl
```ttl

<https://example.org/args.py> a <https://example.org/File> .


```

## Schema

```yaml
$defs:
  AnyLiteralType:
    oneOf:
    - type: number
    - type: boolean
    - type: string
    title: AnyLiteralType
  AnyLiteralList:
    items:
      $ref: '#/$defs/AnyLiteralType'
    title: AnyLiteralList
    type: array
  CWLDefaultObject:
    additionalProperties: {}
    not:
      $comment: Avoid false-positive match of default File or Directory location definition.
      properties:
        class:
          enum:
          - File
          - Directory
          type: string
    title: CWLDefaultObject
    type: object
description: Default value of input if not provided for task execution.
oneOf:
- $ref: '#/$defs/AnyLiteralType'
- $ref: '#/$defs/AnyLiteralList'
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.yaml
- $ref: '#/$defs/CWLDefaultObject'
- items:
    $ref: '#/$defs/CWLDefaultObject'
  type: array
title: CWLDefault

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "basename": "cwl:basename",
    "class": "@type",
    "location": "@id",
    "nameroot": "cwl:File/nameroot",
    "path": {
      "@id": "cwl:path",
      "@type": "@id"
    },
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLDefault`

