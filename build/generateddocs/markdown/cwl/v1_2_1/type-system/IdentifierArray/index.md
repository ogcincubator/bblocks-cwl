
# IdentifierArray (Schema)

`ogc.cwl.v1_2_1.type-system.IdentifierArray` *v1.2.1*

An array of one or more CWL identifiers, used e.g. when
`scatter` lists more than one input parameter to fan a Workflow step out over.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Scattering over two input parameters
A `scatter` value listing two Workflow step input parameter names, causing the step to fan out
over both (combined per `scatterMethod`, e.g. `nested_crossproduct`).

#### json
```json
["echo_in1", "echo_in2"]

```


### Single-item identifier array
A `scatter` value with a single input parameter name. `IdentifierArray` requires at least one
item, so a single-element array is still valid (as opposed to using the bare
`CWLTextPatternID` alternative for that case).

#### json
```json
["scattered_message"]

```

## Schema

```yaml
items:
  $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml
minItems: 1
title: IdentifierArray
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/IdentifierArray/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/IdentifierArray/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/IdentifierArray`

