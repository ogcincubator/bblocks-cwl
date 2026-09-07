Declares requirements that apply to either the runtime environment or the workflow engine
that **must** be met in order to execute a `CommandLineTool` or `Workflow`. If an
implementation cannot satisfy all requirements, or a requirement is listed which is not
recognized by the implementation, it is a fatal error and the implementation must not
attempt to run the process, unless overridden at user option.

This is CWL's principal extension mechanism: any of the 18 requirement classes covered by
[CWLRequirementsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsItem) — `DockerRequirement`,
`ResourceRequirement`, `InitialWorkDirRequirement`, and so on — can be listed here to opt a
process in to that behavior. `requirements` is contrasted with
[CWLHints](bblocks://ogc.cwl.v1_2_1.requirements.CWLHints), which declares the same kind of information
but non-fatally: an implementation that does not recognize or cannot satisfy a hint is free
to ignore it and proceed.

Requirements can be written in two equivalent forms:

- a **list**, where each entry carries its own `class` field naming the requirement type, and
  may alternatively be an [`$import`](bblocks://ogc.cwl.v1_2_1.CWLImport) directive pulling
  requirements in from another file; or
- a **map** ([CWLRequirementsMap](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsMap)) keyed by
  requirement class name, where `class` is implied by the key and does not need to be
  repeated.

Requirements are inherited from any enclosing `Workflow` down to nested steps, and
requirements on a step or a `CommandLineTool` override an inherited requirement of the same
`class`.
