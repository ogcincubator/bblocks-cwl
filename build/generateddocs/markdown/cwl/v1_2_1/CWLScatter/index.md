
# CWLScatter (Schema)

`ogc.cwl.v1_2_1.CWLScatter` *v1.2.1*

One or more input identifier of an application step within a Workflow
were an array-based input to that Workflow should be scattered across multiple
instances of the step application.


[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: 'One or more input identifier of an application step within a Workflow

  were an array-based input to that Workflow should be scattered across multiple

  instances of the step application.

  '
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
- items:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
  title: CWLScatterMulti
  type: array
title: CWLScatter

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatter/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatter/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLScatter`

