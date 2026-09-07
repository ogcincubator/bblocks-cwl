A mixin of the two human-readable documentation fields that CWL attaches to processes, workflow
steps, inputs, and outputs alike:

- `label` — a short, single-line, human-readable name for the object it annotates. Maps to
  `rdfs:label`.
- `doc` — a longer free-text description, either a single string or an array of strings (rendered as
  separate paragraphs) for documentation split across multiple entries.

Both fields are purely descriptive: they carry no execution semantics and do not affect how a CWL
document runs. This block is reused across the process types
([CWLAtomic](bblocks://ogc.cwl.v1_2_1.CWLAtomic), [CWLWorkflow](bblocks://ogc.cwl.v1_2_1.CWLWorkflow),
[CWLAtomicNested](bblocks://ogc.cwl.v1_2_1.CWLAtomicNested),
[CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)) as well as individual
[CWLInputObject](bblocks://ogc.cwl.v1_2_1.CWLInputObject) and
[CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject) entries, so every documentable element of
a CWL document uses the same `label`/`doc` shape.
