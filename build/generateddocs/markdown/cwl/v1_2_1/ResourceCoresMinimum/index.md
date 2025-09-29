
# ResourceCoresMinimum (Schema)

`ogc.cwl.v1_2_1.ResourceCoresMinimum` *v1.2.1*

Minimum reserved number of CPU cores.

May be a fractional value to indicate to a scheduling algorithm that one core can be allocated to
multiple jobs. For example, a value of 0.25 indicates that up to 4 jobs
may run in parallel on 1 core. A value of 1.25 means that up to 3 jobs
can run on a 4 core system (4/1.25 ~ 3).

Processes can only share a core allocation if the sum of each of their 'ramMax', 'tmpdirMax', and
'outdirMax' requests also do not exceed the capacity of the node.

Processes sharing a core must have the same level of isolation (typically a container
or VM) that they would normally have.

The reported number of CPU cores reserved for the process, which is available to expressions 
on the 'CommandLineTool' as 'runtime.cores', must be a non-zero integer, and may be calculated by
rounding up the cores request to the next whole number.

Scheduling systems may allocate fractional CPU resources by setting quotas or scheduling weights.
Scheduling systems that do not support fractional CPUs may round up the request to the next whole number.


[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
default: 1
description: "Minimum reserved number of CPU cores.\n\nMay be a fractional value to
  indicate to a scheduling algorithm that one core can be allocated to\nmultiple jobs.
  For example, a value of 0.25 indicates that up to 4 jobs\nmay run in parallel on
  1 core. A value of 1.25 means that up to 3 jobs\ncan run on a 4 core system (4/1.25
  ~ 3).\n\nProcesses can only share a core allocation if the sum of each of their
  'ramMax', 'tmpdirMax', and\n'outdirMax' requests also do not exceed the capacity
  of the node.\n\nProcesses sharing a core must have the same level of isolation (typically
  a container\nor VM) that they would normally have.\n\nThe reported number of CPU
  cores reserved for the process, which is available to expressions \non the 'CommandLineTool'
  as 'runtime.cores', must be a non-zero integer, and may be calculated by\nrounding
  up the cores request to the next whole number.\n\nScheduling systems may allocate
  fractional CPU resources by setting quotas or scheduling weights.\nScheduling systems
  that do not support fractional CPUs may round up the request to the next whole number.\n"
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
summary: Minimum reserved number of CPU cores.
title: ResourceCoresMinimum

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceCoresMinimum/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceCoresMinimum/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/ResourceCoresMinimum`

