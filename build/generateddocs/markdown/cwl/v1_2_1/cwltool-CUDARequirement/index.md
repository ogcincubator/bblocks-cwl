
# cwltool:CUDARequirement (Schema)

`ogc.cwl.v1_2_1.cwltool-CUDARequirement` *v1.2.1*

cwltool:CUDARequirement

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - cwltool:CUDARequirement
    type: string
  cudaComputeCapability:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CUDAComputeCapability/schema.yaml
  cudaDeviceCountMax:
    default: 1
    description: The maximum amount of devices required.
    example: 8
    minimum: 1
    title: CUDA device count maximum
    type: integer
  cudaDeviceCountMin:
    default: 1
    description: The minimum amount of devices required.
    example: 1
    minimum: 1
    title: CUDA device count minimum
    type: integer
  cudaVersionMin:
    description: 'The minimum CUDA version required to run the software. This corresponds
      to a CUDA SDK release.


      When run in a container, the container image should provide the CUDA runtime,

      and the host driver is injected into the container.  In this case, because CUDA
      drivers

      are backwards compatible, it is possible to use an older SDK with a newer driver
      across major versions.


      See https://docs.nvidia.com/deploy/cuda-compatibility/ for details.

      '
    example: '11.4'
    pattern: ^\d+\.\d+$
    title: CUDA version minimum
    type: string
required:
- cudaVersionMin
- cudaComputeCapability
title: cwltool:CUDARequirement
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/cwltool-CUDARequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/cwltool-CUDARequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/cwltool-CUDARequirement`

