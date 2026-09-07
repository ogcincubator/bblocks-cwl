
# CWL Ontology (Model)

`ogc.cwl.v1_2_1.CWLOntology` *v1.2.1*

The RDFS vocabulary/ontology for the Common Workflow Language (CWL) v1.2, published by the CWL
project at `https://w3id.org/cwl/cwl#` (`cwl:`). It defines an `rdfs:Class` for every CWL document
type (`Workflow`, `CommandLineTool`, `DockerRequirement`, ...) and their `rdfs:subClassOf` relations,
and is the vocabulary the rest of this register's blocks bind their properties to via `context.jsonld`.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### DockerRequirement's place in the class hierarchy
An excerpt of the ontology showing how `cwl:DockerRequirement` relates to the rest of the
vocabulary: it is one of several `rdfs:subClassOf cwl:ProcessRequirement`, the abstract class
shared by every `requirements`/`hints` entry.

#### turtle
```turtle
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

cwl:ProcessRequirement a rdfs:Class .

cwl:DockerRequirement a rdfs:Class ;
    rdfs:subClassOf cwl:ProcessRequirement .

cwl:EnvVarRequirement a rdfs:Class ;
    rdfs:subClassOf cwl:ProcessRequirement .

```


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOntology`

