This is an OGC-specific extension hint, not part of the core CWL v1.2 specification. It marks a
workflow step's Application Package as corresponding to a process the executing instance already
implements natively — a "builtin" — rather than one that must be run from a container image
(see [DockerRequirement](bblocks://ogc.cwl.v1_2_1.DockerRequirement)) or delegated to a remote
execution backend. Because this is unofficial, `class: BuiltinRequirement` may only be used under
`hints`, never under `requirements` — a correct engine unaware of it must reject an unrecognized
class under `requirements` as fatal, but may safely ignore it under `hints` — see
[CWLHints](bblocks://ogc.cwl.v1_2_1.CWLHints).

`BuiltinRequirement` is one of three such OGC-specific hints an instance can use to say how a step's
Application Package should actually be executed, alongside
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.OGCAPIRequirement) (delegate to a remote OGC API -
Processes offering) and [WPS1Requirement](bblocks://ogc.cwl.v1_2_1.WPS1Requirement) (delegate to a
remote WPS-1 provider process). Unlike those two, `BuiltinRequirement` names a process already known
to the local instance rather than a remote one, so its `process` property is a plain identifier
(`CWLTextPatternID`) rather than a `ReferenceURL` to an external endpoint.
