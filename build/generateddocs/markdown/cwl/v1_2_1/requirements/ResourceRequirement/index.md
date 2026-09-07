
# ResourceRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.ResourceRequirement` *v1.2.1*

Specify basic hardware resource requirements for a CommandLineTool: minimum/maximum CPU cores, RAM, and output/temporary directory storage.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Specify basic hardware resource requirements.

"min" is the minimum amount of a resource that must be reserved to schedule a job. If "min"
cannot be satisfied, the job should not be run.

"max" is the maximum amount of a resource that the job shall be allocated. If a node has
sufficient resources, multiple jobs may be scheduled on a single node provided each job's "max"
resource requirements are met. If a job attempts to exceed its resource allocation, an
implementation may deny additional resources, which may result in job failure.

If both "min" and "max" are specified, an implementation may choose to allocate any amount
between "min" and "max", with the actual allocation provided in the `runtime` object.

If "min" is specified but "max" is not, then "max" == "min". If "max" is specified but "min" is
not, then "min" == "max".

It is an error if max < min. It is an error if the value of any of these fields is negative.

If neither "min" nor "max" is specified for a resource, the defaults are: 1 core, 256 MiB RAM,
1024 MiB output directory storage, 1024 MiB temporary directory storage.

See also: [CWL v1.2 CommandLineTool spec — ResourceRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#ResourceRequirement).

## Examples

### Fixed numeric resource limits
A `ResourceRequirement` reserving between 2 and 4 CPU cores, at least 512 MiB of RAM, and up
to 1 GiB of temporary directory storage, adapted from the CWL conformance tests
`bwa-mem-tool.cwl` and `storage_float.cwl`.

#### json
```json
{
  "class": "ResourceRequirement",
  "coresMin": 2,
  "coresMax": 4,
  "ramMin": 512,
  "tmpdirMax": 1024
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/context.jsonld",
  "class": "ResourceRequirement",
  "coresMin": 2,
  "coresMax": 4,
  "ramMin": 512,
  "tmpdirMax": 1024
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#ResourceRequirement/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/ResourceRequirement> ;
    ns1:coresMax 4 ;
    ns1:coresMin 2 ;
    ns1:ramMin 512 ;
    ns1:tmpdirMax 1024 .


```


### Resource limits computed from an expression
Adapted from the CWL conformance test `dynresreq.cwl`. `coresMin` and `coresMax` are
computed at runtime with a parameter reference expression instead of a fixed number, here
sizing the reservation to the size of an input file (requires
`InlineJavascriptRequirement` to be in effect for expression evaluation).

#### json
```json
{
  "class": "ResourceRequirement",
  "coresMin": "$(inputs.special_file.size)",
  "coresMax": "$(inputs.special_file.size)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/context.jsonld",
  "class": "ResourceRequirement",
  "coresMin": "$(inputs.special_file.size)",
  "coresMax": "$(inputs.special_file.size)"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#ResourceRequirement/> .

[] a <https://example.org/ResourceRequirement> ;
    ns1:coresMax "$(inputs.special_file.size)" ;
    ns1:coresMin "$(inputs.special_file.size)" .


```

## Schema

```yaml
additionalProperties: false
description: 'Specify basic hardware resource requirements.


  "min" is the minimum amount of a resource that must be reserved to

  schedule a job. If "min" cannot be satisfied, the job should not

  be run.


  "max" is the maximum amount of a resource that the job shall be

  allocated. If a node has sufficient resources, multiple jobs may

  be scheduled on a single node provided each job''s "max" resource

  requirements are met. If a job attempts to exceed its resource

  allocation, an implementation may deny additional resources, which

  may result in job failure.


  If both "min" and "max" are specified, an implementation may

  choose to allocate any amount between "min" and "max", with the

  actual allocation provided in the `runtime` object.


  If "min" is specified but "max" is not, then "max" == "min"

  If "max" is specified by "min" is not, then "min" == "max".


  It is an error if max < min.


  It is an error if the value of any of these fields is negative.


  If neither "min" nor "max" is specified for a resource, use the default values below

  (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#ResourceRequirement).

  '
properties:
  class:
    enum:
    - ResourceRequirement
    type: string
    x-jsonld-id: '@type'
  coresMin:
    default: 1
    description: 'Minimum reserved number of CPU cores (default is 1).


      May be a fractional value to indicate to a scheduling algorithm that one core
      can be allocated to

      multiple jobs. For example, a value of 0.25 indicates that up to 4 jobs

      may run in parallel on 1 core. A value of 1.25 means that up to 3 jobs

      can run on a 4 core system (4/1.25 ~ 3).


      Processes can only share a core allocation if the sum of each of their ''ramMax'',
      ''tmpdirMax'', and

      ''outdirMax'' requests also do not exceed the capacity of the node.


      Processes sharing a core must have the same level of isolation (typically a
      container

      or VM) that they would normally have.


      The reported number of CPU cores reserved for the process, which is available
      to expressions

      on the ''CommandLineTool'' as ''runtime.cores'', must be a non-zero integer,
      and may be calculated by

      rounding up the cores request to the next whole number.


      Scheduling systems may allocate fractional CPU resources by setting quotas or
      scheduling weights.

      Scheduling systems that do not support fractional CPUs may round up the request
      to the next whole number.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/coresMin
  coresMax:
    description: 'Maximum reserved number of CPU cores.

      See ''coresMin'' for discussion about fractional CPU requests.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/coresMax
  ramMin:
    default: 256
    description: 'Minimum reserved RAM in mebibytes (2**20) (default is 256).


      May be a fractional value. If so, the actual RAM request must be rounded up

      to the next whole number.


      The reported amount of RAM reserved for the process, which is available to

      expressions on the ''CommandLineTool'' as ''runtime.ram'', must be a non-zero
      integer.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/ramMin
  ramMax:
    description: 'Maximum reserved RAM in mebibytes (2**20).

      See ''ramMin'' for discussion about fractional RAM requests.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/ramMax
  outdirMin:
    default: 1024
    description: 'Minimum reserved filesystem based storage for the designated output

      directory in mebibytes (2**20).


      May be a fractional value. If so, the actual storage request must be rounded

      up to the next whole number.


      The reported amount of storage reserved for the process, which is available

      to expressions on the ''CommandLineTool'' as ''runtime.outdirSize'', must be
      a non-zero integer.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/outdirMin
  outdirMax:
    description: 'Maximum reserved filesystem based storage for the designated output

      directory in mebibytes (2**20).

      See ''outdirMin'' for discussion about fractional storage requests.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/outdirMax
  tmpdirMin:
    default: 1024
    description: 'Minimum reserved filesystem based storage for the designated temporary

      directory in mebibytes (2**20).


      May be a fractional value. If so, the actual storage request must be rounded

      up to the next whole number.


      The reported amount of storage reserved for the process, which is available

      to expressions on the ''CommandLineTool'' as ''runtime.tmpdirSize'', must be
      a non-zero integer.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/tmpdirMin
  tmpdirMax:
    description: 'Maximum reserved filesystem based storage for the designated temporary

      directory in mebibytes (2**20).

      See ''tmpdirMin'' for discussion about fractional storage requests.

      '
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceQuantityOrFractional/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement/tmpdirMax
title: ResourceRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "coresMin": "cwl:ResourceRequirement/coresMin",
    "coresMax": "cwl:ResourceRequirement/coresMax",
    "ramMin": "cwl:ResourceRequirement/ramMin",
    "ramMax": "cwl:ResourceRequirement/ramMax",
    "outdirMin": "cwl:ResourceRequirement/outdirMin",
    "outdirMax": "cwl:ResourceRequirement/outdirMax",
    "tmpdirMin": "cwl:ResourceRequirement/tmpdirMin",
    "tmpdirMax": "cwl:ResourceRequirement/tmpdirMax",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/ResourceRequirement`

