
# CWLOutputStdErr (Schema)

`ogc.cwl.v1_2_1.CWLOutputStdErr` *v1.2.1*

CWLOutputStdErr

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
oneOf:
- description: 'Indicates that the data pushed to the standard error stream by the
    command will be redirected to this CWL output.

    Can be defined for only one output. If combined with ''stderr'' at the root of
    the CWL document, that definition

    will indicate the desired name of the output file where the error stream will
    be written to.  A random name will

    be applied for the file of this output unless otherwise specified.

    '
  enum:
  - stderr
  type: string
- properties:
    type:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErrDefinition/schema.yaml
  required:
  - type
  type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputStdErr`

