The item shape used when a [CWLOutputsDefinition](bblocks://ogc.cwl.v1_2_1.CWLOutputsDefinition) is
written in list form: one entry per output parameter, each carrying its own `id` explicitly. This is
the counterpart to [CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject), which is used instead
when outputs are written as a map keyed by identifier — there, the identifier is the map key rather
than a property, so `id` does not appear on the value itself.

Both `id` and `type` are required. `type` may be a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType), or the
`stdout`/`stderr` shorthand (see [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) /
[CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)) for capturing a process's standard
streams. The optional `outputBinding` describes how to extract the output's value — see
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding).
