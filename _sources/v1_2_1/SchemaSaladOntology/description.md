[Schema Salad](https://www.commonwl.org/v1.2/SchemaSalad.html) is the schema language the CWL
specification itself is written in — it is what lets a CWL document's `class` field, `$import`/`$include`
directives, and `jsonldPredicate`-annotated fields resolve the way they do. This block publishes its
metaschema vocabulary, distinct from the [CWL document vocabulary](bblocks://ogc.cwl.v1_2_1.CWLOntology)
(`cwl:`) that the rest of this register binds to: `sld:RecordSchema`, `sld:EnumSchema`,
`sld:JsonldPredicate`, `sld:NamedType`, and related classes/properties used to describe schema-salad
schemas themselves, rather than CWL documents that conform to such a schema.

Published upstream by the CWL project at `https://www.commonwl.org/v1.2/salad.ttl`, dereferenceable via
the persistent identifier `https://w3id.org/cwl/salad`. Like the
[CWL Ontology](bblocks://ogc.cwl.v1_2_1.CWLOntology) block's upstream file, the published Turtle has the
same `@prefix @base: ...` syntax defect; `ontology.ttl` in this block renames that prefix to `sld:` so it
parses.
