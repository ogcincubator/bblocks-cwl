This is a `cwltool`-specific extension, not part of the core CWL v1.2 specification: it lives in the
`http://commonwl.org/cwltool#` namespace, so a document using it must declare that namespace (typically
bound to the `cwltool:` prefix via `$namespaces`) for the `class` value `cwltool:CUDARequirement` to be
recognized. Other CWL implementations are not required to support it, and correct tools should treat an
unrecognized `class` under `requirements` as a fatal error unless the document lists it under `hints`
instead — see [CWLHints](bblocks://ogc.cwl.v1_2_1.CWLHints).

The device count fields work as a pair: if only `cudaDeviceCountMin` is given, it is also used as the
maximum; if only `cudaDeviceCountMax` is given, it is also used as the minimum; if neither is given, the
default is a single device.

`cudaComputeCapability` (see [CUDAComputeCapability](bblocks://ogc.cwl.v1_2_1.CUDAComputeCapability))
carries the actual GPU capability matching semantics: a single value is a minimum bound, while an array
value (see
[CUDAComputeCapabilityArray](bblocks://ogc.cwl.v1_2_1.CUDAComputeCapabilityArray)) is an explicit
allow-list of exact capabilities.
