This is the vocabulary that every other block in this register binds its schema properties and
`class`-discriminated types to, via `context.jsonld` — the `cwl:` prefix used throughout this register's
JSON-LD contexts (e.g. `cwl:DockerRequirement`, `cwl:Workflow`) resolves to `https://w3id.org/cwl/cwl#`,
the namespace this block declares.

The ontology only asserts `rdfs:Class`/`rdfs:subClassOf` triples — it does not declare `rdf:Property`
axioms for CWL's fields, since schema-salad does not generate them for CWL's own vocabulary (unlike
[Schema Salad's own metaschema](bblocks://ogc.cwl.v1_2_1.SchemaSaladOntology), which does declare
properties for its `JsonldPredicate` and `NamedType` classes).

Published upstream by the CWL project at `https://www.commonwl.org/v1.2/cwl.ttl`, dereferenceable via
the persistent identifier `https://w3id.org/cwl/cwl`. That upstream file has a syntax defect — schema-salad's
Turtle serializer emits `@prefix @base: <https://w3id.org/cwl/cwl#> .`, and `@base` is a reserved Turtle
keyword, not a legal prefix name, so the file as published does not parse as valid Turtle. `ontology.ttl`
in this block is the same content with that prefix renamed to `cwl:`.
