
# CWLAtomicBase (Schema)

`ogc.cwl.v1_2_1.CWLAtomicBase` *v1.2.1*

Direct CWL definition instead of the graph representation.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: Direct CWL definition instead of the graph representation.
properties:
  arguments:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/schema.yaml
  baseCommand:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.yaml
  class:
    description: CWL class specification. This is used to differentiate between single
      Application Package (AP)definitions and Workflow that chains multiple packages.
    enum:
    - CommandLineTool
    - ExpressionTool
    title: Class
    type: string
  hints:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/schema.yaml
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
  inputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.yaml
  intent:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIntent/schema.yaml
  outputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.yaml
  requirements:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirements/schema.yaml
  scatter:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatter/schema.yaml
  scatterMethod:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatterMethod/schema.yaml
  stderr:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: 'Destination of the error stream.

      Typically, an expression referring to a desired file name or provided by a CWL
      input reference.

      '
    x-jsonld-id: https://w3id.org/cwl/cwl#stderr
  stdin:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: "Source of the input stream. \nTypically, an expression referring
      to an existing file name or an input of the CWL document.\n"
    x-jsonld-id: https://w3id.org/cwl/cwl#stdin
  stdout:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: 'Destination of the output stream.

      Typically, an expression referring to a desired file name or provided by a CWL
      input reference.

      '
    x-jsonld-id: https://w3id.org/cwl/cwl#stdout
required:
- class
- inputs
- outputs
title: CWL atomic definition
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLAtomicBase/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLAtomicBase/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "stderr": "cwl:stderr",
    "stdin": "cwl:stdin",
    "stdout": "cwl:stdout",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLAtomicBase/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLAtomicBase`

