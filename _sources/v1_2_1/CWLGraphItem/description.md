A single process object inside a [`$graph`](bblocks://ogc.cwl.v1_2_1.CWLGraph) array. Per the CWL
specification, every process object listed in a `$graph` document **must** carry an `id` — unlike a
process object embedded directly in a `Workflow` step's `run` field, or the single process object at
the root of a non-graph document (see [CWLAtomicBase](bblocks://ogc.cwl.v1_2_1.CWLAtomicBase)), where
`id` is optional. This `id` is what lets a `Workflow` step's `run` field, or a document reference's
fragment identifier, pick out this specific process object from among the others in the same `$graph`.

Otherwise the shape is the same `class`-discriminated CommandLineTool/ExpressionTool/Workflow process
object used throughout CWL, extended here with `Workflow` as a possible `class` value (in addition to
`CommandLineTool`/`ExpressionTool`) since a `$graph` document commonly packages a workflow together with
the processes its steps reference.
