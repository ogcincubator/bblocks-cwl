
# CWLScatterMethod (Schema)

`ogc.cwl.v1_2_1.CWLScatterMethod` *v1.2.1*

Describes how to decompose the scattered input into a discrete
set of jobs. When 'dotproduct', specifies that each of the input arrays
are aligned and one element taken from each array to construct each job.
It is an error if all input arrays are of different length. When 'nested_crossproduct',
specifies the Cartesian product of the inputs, producing a job for every
combination of the scattered inputs. The output must be nested arrays
for each level of scattering, in the order that the input arrays are listed
in the scatter field. When 'flat_crossproduct', specifies the Cartesian
product of the inputs, producing a job for every combination of the scattered
inputs. The output arrays must be flattened to a single level, but otherwise
listed in the order that the input arrays are listed in the scatter field.


[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Cartesian product over two scattered inputs
A `WorkflowStep` scatters over two input arrays using `flat_crossproduct`, so a job is run
for every combination of the two inputs, with the results flattened to a single-level array.

#### json
```json
"flat_crossproduct"

```


### Aligned inputs (dotproduct)
When scattered input arrays are already aligned element-by-element, `dotproduct` takes one
element from each array per job instead of computing every combination.

#### json
```json
"dotproduct"

```

## Schema

```yaml
description: 'Describes how to decompose the scattered input into a discrete

  set of jobs. When ''dotproduct'', specifies that each of the input arrays

  are aligned and one element taken from each array to construct each job.

  It is an error if all input arrays are of different length. When ''nested_crossproduct'',

  specifies the Cartesian product of the inputs, producing a job for every

  combination of the scattered inputs. The output must be nested arrays

  for each level of scattering, in the order that the input arrays are listed

  in the scatter field. When ''flat_crossproduct'', specifies the Cartesian

  product of the inputs, producing a job for every combination of the scattered

  inputs. The output arrays must be flattened to a single level, but otherwise

  listed in the order that the input arrays are listed in the scatter field.

  '
enum:
- dotproduct
- nested_crossproduct
- flat_crossproduct
title: scatterMethod
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatterMethod/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatterMethod/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLScatterMethod`

