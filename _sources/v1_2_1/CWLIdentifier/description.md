A CWL process identifier accepts exactly two syntactic forms:

- a standard **UUID** (e.g. `550e8400-e29b-41d4-a716-446655440000`), or
- a string matching the [CWLTextPatternID](bblocks://ogc.cwl.v1_2_1.CWLTextPatternID) pattern, which
  covers the plain names, dotted names, and `#`/`sub/part#ref`-style fragment references that CWL
  documents actually use for `id` fields (e.g. `main`, `touch.cwl#name`, `sub/part#ref`).

This block is kept independent from the generic [`ogc.ogc-utils.iri-or-curie`](bblocks://ogc.ogc-utils.iri-or-curie)
block used elsewhere in this register (e.g. by [ReferenceURL](bblocks://ogc.cwl.v1_2_1.ReferenceURL)):
CWL process identifiers are not IRIs or CURIEs — they are local, often fragment-based names scoped to
a single CWL document (or to a packed document made up of several), and the UUID/text-pattern
alternation here matches exactly what the upstream CWL schema allows, no more and no less.
