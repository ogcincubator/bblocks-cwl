
# CWLImport (Schema)

`ogc.cwl.v1_2_1.CWLImport` *v1.2.1*

Represents an '$import' directive that should point toward another compatible CWL file to import where specified.
The contents of the imported file should be relevant contextually where it is being imported.


[*Status*](http://www.opengis.net/def/status): Under development

## Description

The schema validation of the CWL will not itself perform the '$import' to resolve and validate its contents.
Therefore, the complete schema will not be validated entirely, and could still be partially malformed.
To ensure proper and exhaustive validation of a CWL definition with this schema, all '$import' directives
should be resolved and extended beforehand.

## Examples

### Importing a schema definition file
A `CommandLineTool` requirement that imports an external schema definition document, as
used in practice to share custom type definitions across CWL files (e.g. via
[SchemaDefRequirement](bblocks://ogc.cwl.v1_2_1.requirements.SchemaDefRequirement)).

#### json
```json
{
  "$import": "schemadef-type.yml"
}

```


### Importing a set of output parameters
An `outputs` section can itself be replaced wholesale by an `$import` directive, pulling
in a document fragment defined elsewhere.

#### json
```json
{
  "$import": "params_inc.yml"
}

```

## Schema

```yaml
$comment: 'The schema validation of the CWL will not itself perform the ''$import''
  to resolve and validate its contents.

  Therefore, the complete schema will not be validated entirely, and could still be
  partially malformed.

  To ensure proper and exhaustive validation of a CWL definition with this schema,
  all ''$import'' directives

  should be resolved and extended beforehand.

  '
additionalProperties: false
description: 'Represents an ''$import'' directive that should point toward another
  compatible CWL file to import where specified.

  The contents of the imported file should be relevant contextually where it is being
  imported.

  '
properties:
  $import:
    type: string
required:
- $import
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLImport`

