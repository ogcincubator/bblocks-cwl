A mixin of document-level metadata fields shared by CWL's top-level process types
([CommandLineTool](bblocks://ogc.cwl.v1_2_1.CWLAtomic), [Workflow](bblocks://ogc.cwl.v1_2_1.CWLWorkflow),
[ExpressionTool](bblocks://ogc.cwl.v1_2_1.CWLAtomic)) and their nested/graph-embedded counterparts
([CWLAtomicNested](bblocks://ogc.cwl.v1_2_1.CWLAtomicNested),
[CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)). It groups:

- `s:keywords` — an array of non-empty, free-text terms used for search and categorization, drawn
  from the schema.org `Thing/keywords` property that `CommonWorkflowLanguage.yml` mixes into every
  process.
- `version` — the process/document's own version string, distinct from
  [CWLVersion](bblocks://ogc.cwl.v1_2_1.CWLVersion)'s `cwlVersion` (which declares which version of
  the *CWL standard itself* a document conforms to). This `version` is the process author's own
  release identifier for the tool or workflow being described.

Keeping these fields in one reusable block avoids repeating the same two properties across every
place a CWL document can declare a process, and lets a profile constrain both fields uniformly.
