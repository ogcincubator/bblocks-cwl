`OGCAPIRequirement` is an OGC-specific extension to the CWL requirement/hint vocabulary; it has no
upstream CWL specification counterpart. It marks a workflow step whose actual computation is not run
by the CWL runner itself but delegated to an external [OGC API - Processes](https://ogcapi.ogc.org/processes/)
`Process` resource, identified by the `process` property (a URL to the process's location, typically an
`https://.../processes/{processId}` endpoint per the OGC API - Processes conformance classes). The
runner is expected to submit an execution request to that endpoint (e.g. `POST /processes/{processId}/execution`)
and poll or subscribe for job status, rather than executing the step's `baseCommand`/`run` locally.

Because this class is not part of the official CWL v1.2.1 specification, it can only ever appear as a
*hint* — inside a [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLHintsItem) — never as a *requirement* (a
standards-conformant CWL processor is free to ignore hints it does not understand, but must reject a
document containing an unrecognized requirement). See also
[WPS1Requirement](bblocks://ogc.cwl.v1_2_1.requirements.WPS1Requirement) for the equivalent hint targeting a legacy
WPS 1.0 provider instead.
