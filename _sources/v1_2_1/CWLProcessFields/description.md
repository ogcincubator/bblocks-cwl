The process-definition fields common to every packaging shape a CWL CommandLineTool, ExpressionTool,
or Workflow can take: at the document root
([CWLAtomicBase](bblocks://ogc.cwl.v1_2_1.CWLAtomicBase)), embedded inline as a step's `run` value, or
as an entry of a `$graph` array ([CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)).

This block deliberately excludes `class` — the property that discriminates which kind of process a
document describes — because which `class` values are legal differs by packaging: a `$graph` entry
may declare `class: Workflow` alongside `CommandLineTool`/`ExpressionTool`, while a standalone atomic
document only allows the latter two. Each consumer of this block layers its own `class` property (with
its own enum) and its own `required` list on top via `allOf`, rather than this block hard-coding one
set of allowed values that every consumer would then be stuck with.

Factoring these fields out here, instead of each consumer repeating the same property list, keeps the
two shapes from drifting out of sync with each other as the schema evolves.
