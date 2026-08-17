Each item in this list is expected to be the IRI of a concept node from an ontology of computational
operation types, rather than free text. The intent behind the `intent` property is to make it possible
to search or classify processes by *what kind of operation they perform*, independently of how the
process is named or documented.

This is especially useful for an `Operation` (CWL's abstract, no-op stand-in for representing an
unimplemented computational step — not currently modeled as its own block in this register), but the
same mechanism can be applied to a [`CWLAtomic`](bblocks://ogc.cwl.v1_2_1.CWLAtomic) or
[`CWLWorkflow`](bblocks://ogc.cwl.v1_2_1.CWLWorkflow).

A widely used source of such concept IRIs is the [EDAM Ontology](http://edamontology.org/)'s
`Operation` branch, for example:

- `http://edamontology.org/operation_2928` (Alignment)
- `http://edamontology.org/operation_3432` (Clustering)
- `http://edamontology.org/operation_3199` (Split read mapping)

Nothing in this schema ties `intent` to EDAM specifically — any dereferenceable IRI identifying an
operation concept in some ontology is valid — but consumers that want to reason over intents in a
consistent way will typically agree on a shared ontology (such as EDAM) rather than mixing arbitrary
vocabularies.
