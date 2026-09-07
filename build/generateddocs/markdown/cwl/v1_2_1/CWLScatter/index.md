
# CWLScatter (Schema)

`ogc.cwl.v1_2_1.CWLScatter` *v1.2.1*

One or more input identifier of an application step within a Workflow
were an array-based input to that Workflow should be scattered across multiple
instances of the step application.


[*Status*](http://www.opengis.net/def/status): Under development

## Description

To use scatter/gather, [ScatterFeatureRequirement](bblocks://ogc.cwl.v1_2_1.requirements.ScatterFeatureRequirement)
must be specified in the workflow or workflow step requirements.

A "scatter" operation specifies that the associated workflow step or subworkflow should execute
separately over a list of input elements. Each job making up a scatter operation is independent and
may be executed concurrently.

The `scatter` field specifies one or more input parameters which will be scattered. An input
parameter may be listed more than once. The declared type of each input parameter implicitly
becomes an array of items of the input parameter type. If a parameter is listed more than once, it
becomes a nested array. As a result, upstream parameters which are connected to scattered parameters
must be arrays.

All output parameter types are also implicitly wrapped in arrays. Each job in the scatter results in
an entry in the output array.

If any scattered parameter's runtime value is an empty array, all outputs are set to empty arrays and
no work is done for the step, according to applicable scattering rules.

If `scatter` declares more than one input parameter, [CWLScatterMethod](bblocks://ogc.cwl.v1_2_1.CWLScatterMethod)
describes how to decompose the input into a discrete set of jobs.

## Examples

### Scattering over a single input
A workflow step scatters over a single input parameter, running one job per
element of `file1`.

#### json
```json
"file1"

```


### Scattering over multiple inputs
A workflow step scatters over two input parameters at once. Combined with a
[CWLScatterMethod](bblocks://ogc.cwl.v1_2_1.CWLScatterMethod) of `dotproduct`, the two
arrays are aligned and one job is created per pair of elements.

#### json
```json
["echo_in1", "echo_in2"]

```

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

