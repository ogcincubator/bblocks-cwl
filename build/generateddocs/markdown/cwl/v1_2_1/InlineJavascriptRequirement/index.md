
# InlineJavascriptRequirement (Schema)

`ogc.cwl.v1_2_1.InlineJavascriptRequirement` *v1.2.1*

Indicates that the workflow platform must support inline Javascript expressions.

If this requirement is not present, the workflow platform must not perform expression interpolation
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).


[*Status*](http://www.opengis.net/def/status): Under development

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

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InlineJavascriptRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InlineJavascriptRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InlineJavascriptRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/InlineJavascriptRequirement`

