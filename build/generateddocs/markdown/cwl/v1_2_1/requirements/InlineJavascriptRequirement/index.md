
# InlineJavascriptRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.InlineJavascriptRequirement` *v1.2.1*

Indicates that the workflow platform must support inline Javascript expressions.

If this requirement is not present, the workflow platform must not perform expression interpolation
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

Indicates that the workflow platform must support inline Javascript expressions. If this requirement
is not present, the workflow platform must not perform expression interpolation
(see [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)).

## `expressionLib`

The `expressionLib` field lists additional code fragments that are inserted before executing any
expression code, allowing function definitions that may then be called from CWL expressions. Each
entry is either a literal string of Javascript source, or an object with a single `$include` field
naming an external file to be inlined verbatim.

See also: the
[CWL v1.2 CommandLineTool spec — InlineJavascriptRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).

## Examples

### Expression library defined inline
An `InlineJavascriptRequirement` that supplies a single Javascript function definition as a
literal string in `expressionLib`, making it callable from later CWL expressions
(adapted from the CWL conformance test `js-expr-req-wf.cwl`).

#### json
```json
{
  "class": "InlineJavascriptRequirement",
  "expressionLib": [
    "function foo() { return 2; }"
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/context.jsonld",
  "class": "InlineJavascriptRequirement",
  "expressionLib": [
    "function foo() { return 2; }"
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#InlineJavascriptRequirement/> .

[] a <https://example.org/InlineJavascriptRequirement> ;
    ns1:expressionLib "function foo() { return 2; }" .


```


### Expression library combining an included file and an inline fragment
An `InlineJavascriptRequirement` whose `expressionLib` mixes an external Javascript file,
referenced via `$include`, with an inline function definition that depends on it
(adapted from the CWL conformance test `template-tool.cwl`).

#### json
```json
{
  "class": "InlineJavascriptRequirement",
  "expressionLib": [
    { "$include": "underscore.js" },
    "var t = function(s) { return _.template(s, {variable: 'data'})({'inputs': inputs}); };"
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/context.jsonld",
  "class": "InlineJavascriptRequirement",
  "expressionLib": [
    {
      "$include": "underscore.js"
    },
    "var t = function(s) { return _.template(s, {variable: 'data'})({'inputs': inputs}); };"
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#InlineJavascriptRequirement/> .

[] a <https://example.org/InlineJavascriptRequirement> ;
    ns1:expressionLib [ ],
        "var t = function(s) { return _.template(s, {variable: 'data'})({'inputs': inputs}); };" .


```

## Schema

```yaml
additionalProperties: false
description: 'Indicates that the workflow platform must support inline Javascript
  expressions.


  If this requirement is not present, the workflow platform must not perform expression
  interpolation

  (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).

  '
properties:
  class:
    enum:
    - InlineJavascriptRequirement
    type: string
    x-jsonld-id: '@type'
  expressionLib:
    description: 'Additional code fragments that will also be inserted before executing
      the expression code.

      Allows for function definitions that may be called from CWL expressions.

      '
    items:
      oneOf:
      - type: string
      - additionalProperties: false
        properties:
          $include:
            type: string
        required:
        - $include
        type: object
      title: exp_lib
    title: InlineJavascriptLibraries
    type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#InlineJavascriptRequirement/expressionLib
required:
- expressionLib
title: InlineJavascriptRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/InlineJavascriptRequirement`

