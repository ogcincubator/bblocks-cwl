
# cwltool:CUDARequirement (Schema)

`ogc.cwl.v1_2_1.requirements.cwltool-CUDARequirement` *v1.2.1*

`cwltool` extension requirement declaring that a process
needs NVIDIA CUDA (GPU hardware acceleration): minimum CUDA SDK version, required compute
capability, and the minimum/maximum number of GPU devices to request.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This is a `cwltool`-specific extension, not part of the core CWL v1.2 specification: it lives in the
`http://commonwl.org/cwltool#` namespace, so a document using it must declare that namespace (typically
bound to the `cwltool:` prefix via `$namespaces`) for the `class` value `cwltool:CUDARequirement` to be
recognized. Other CWL implementations are not required to support it, and correct tools should treat an
unrecognized `class` under `requirements` as a fatal error unless the document lists it under `hints`
instead — see [CWLHints](bblocks://ogc.cwl.v1_2_1.requirements.CWLHints).

The device count fields work as a pair: if only `cudaDeviceCountMin` is given, it is also used as the
maximum; if only `cudaDeviceCountMax` is given, it is also used as the minimum; if neither is given, the
default is a single device.

`cudaComputeCapability` carries the actual GPU capability matching semantics: a single string value
(pattern `\d+\.\d+`) is a minimum bound — GPUs with a higher capability are also accepted — while an
array value is an explicit allow-list of exact capabilities, selecting only GPUs whose compute
capability appears in the array.

## Examples

### Explicit compute capability allow-list
A `CUDARequirement` that accepts only GPUs with one of three exact compute capabilities,
requesting a minimum number of devices bound to an input parameter — adapted from `cwltool`'s
own CUDA test workflows.

#### json
```json
{
  "class": "cwltool:CUDARequirement",
  "cudaVersionMin": "1.0",
  "cudaComputeCapability": ["1.0", "2.0", "3.0"],
  "cudaDeviceCountMin": 2
}

```


### Minimum compute capability with a device range
A `CUDARequirement` using a single `cudaComputeCapability` value (a minimum bound, accepting
any GPU with equal or higher capability) together with a device count range.

#### json
```json
{
  "class": "cwltool:CUDARequirement",
  "cudaVersionMin": "1.0",
  "cudaComputeCapability": "1.0",
  "cudaDeviceCountMin": 2,
  "cudaDeviceCountMax": 4
}

```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - cwltool:CUDARequirement
    type: string
  cudaComputeCapability:
    description: "The compute capability supported by the GPU hardware.\n\n* If this
      is a single value, it defines only the minimum compute capability.\n  GPUs with
      higher capability are also accepted.\n* If it is an array value, then only select
      GPUs with compute capabilities that explicitly\n  appear in the array.\n  See
      https://docs.nvidia.com/deploy/cuda-compatibility/#faq and\n  https://docs.nvidia.com/cuda/cuda-c-best-practices-guide/index.html#cuda-compute-capability\n
      \ for details.\n"
    oneOf:
    - description: The compute capability supported by the GPU hardware.
      pattern: ^\d+\.\d+$
      title: CUDA compute capability
      type: string
    - items:
        description: The compute capability supported by the GPU hardware.
        pattern: ^\d+\.\d+$
        title: CUDA compute capability
        type: string
      minItems: 1
      title: CUDAComputeCapabilityArray
      type: array
    title: CUDA compute capability
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

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/cwltool-CUDARequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/cwltool-CUDARequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/cwltool-CUDARequirement`

