A `$graph` document is one of the two ways the CWL specification defines for "packing" a workflow
together with the processes of each of its steps into a single file (the other being embedding, where
each step's process object is copied directly into its `run` field). A `$graph` document has no process
object at its root; instead the root carries a [`$graph`](https://www.commonwl.org/v1.2/SchemaSalad.html#Document_graph)
array of process objects (see [CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)), each of which
**must** carry an `id`, alongside the shared `cwlVersion` and document-level metadata/documentation
fields that apply to every process object in the array (all of them validate and execute as the
`cwlVersion` declared at this top level).

Within the array, a `Workflow` step's `run` field cross-references another process object elsewhere in
the same `$graph` by its `id`, rather than embedding it inline. When a packed document is executed
without a fragment identifier picking out a specific process, the runner falls back to the process
object with `id` `#main` (or `main`).

This register constrains the array to exactly one entry (`minItems`/`maxItems`: 1), reflecting the
common convention where a `$graph` document packages a single `Workflow` alongside no other
cross-referenced processes, or a single standalone `CommandLineTool`/`ExpressionTool` wrapped in `$graph`
form rather than declared at the document root. See [CWL](bblocks://ogc.cwl.v1_2_1.CWL) for the
document-root schema that chooses between this `$graph` form and a direct, non-graph process
definition.
