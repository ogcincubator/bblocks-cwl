
# CWLCommand (Schema)

`ogc.cwl.v1_2_1.CWLCommand` *v1.2.1*

Command called in the docker image or on shell according to requirements
and hints specifications. Can be omitted if already defined in the docker
image.


[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: 'Command called in the docker image or on shell according to requirements

  and hints specifications. Can be omitted if already defined in the docker

  image.

  '
oneOf:
- title: String command.
  type: string
- additionalProperties: false
  items:
    title: cmd
    type: string
  title: Command Parts
  type: array
title: CWLCommand

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLCommand`

