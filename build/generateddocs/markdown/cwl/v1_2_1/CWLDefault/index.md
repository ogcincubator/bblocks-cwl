
# CWLDefault (Schema)

`ogc.cwl.v1_2_1.CWLDefault` *v1.2.1*

Default value of input if not provided for task execution.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
$defs:
  AnyLiteralList:
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/AnyLiteralType/schema.yaml
    title: AnyLiteralList
    type: array
description: Default value of input if not provided for task execution.
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/AnyLiteralType/schema.yaml
- $ref: '#/$defs/AnyLiteralList'
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultObject/schema.yaml
- items:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultObject/schema.yaml
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
    "nameroot": "cwl:File/nameroot",
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

