`WPS1Requirement` is an OGC-specific extension to the CWL requirement/hint vocabulary; it has no
upstream CWL specification counterpart. It marks a workflow step whose actual computation is not run
by the CWL runner itself but delegated to a remote [WPS 1.0](https://www.ogc.org/standard/wps/) process,
identified by two properties: `provider` (the WPS endpoint URL, i.e. the base URL to which
`Execute`/`GetCapabilities`/`DescribeProcess` requests are sent) and `process` (the WPS process
identifier to invoke at that endpoint, as used in the `Identifier` element of a WPS `Execute` request).
The runner is expected to submit a WPS `Execute` request against that process and poll for completion,
rather than executing the step's `baseCommand`/`run` locally.

Because this class is not part of the official CWL v1.2.1 specification, it can only ever appear as a
*hint* — inside a [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.CWLHintsItem) — never as a *requirement* (a
standards-conformant CWL processor is free to ignore hints it does not understand, but must reject a
document containing an unrecognized requirement). See also
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.OGCAPIRequirement) for the equivalent hint targeting a
modern OGC API - Processes provider instead.
