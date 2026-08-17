Declares hints applying to either the runtime environment or the workflow engine that may be
helpful in executing a process. Structurally, `hints` accepts the same shapes as
[CWLRequirements](bblocks://ogc.cwl.v1_2_1.CWLRequirements) — either a mapping keyed by `class`, or
a list of [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.CWLHintsItem) entries (or `$import` directives)
each carrying an explicit `class` — but the two fields differ in what a workflow engine must do
with them.

`requirements` are mandatory: if an implementation cannot satisfy one, it must treat this as a
fatal error and must not run the process (unless overridden at user option). `hints`, by contrast,
are advisory: it is not an error if an implementation cannot satisfy all hints, though it may
report a warning. This makes `hints` the natural place to carry optional or non-standard,
implementation-specific extensions — such as this register's own
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.OGCAPIRequirement) and `WPS1Requirement`, which tell
an OGC-aware runner to delegate execution to a remote OGC API - Processes or WPS-1 provider —
without breaking engines that don't recognize them, since any unrecognized `class` still falls
back to `UnknownRequirement`.
