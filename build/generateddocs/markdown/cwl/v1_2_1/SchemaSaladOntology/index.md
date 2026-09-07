
# Schema Salad Ontology (Model)

`ogc.cwl.v1_2_1.SchemaSaladOntology` *v1.2.1*

The RDFS vocabulary/ontology for Schema Salad, the schema language CWL is defined in, published
alongside CWL v1.2 at `https://w3id.org/cwl/salad#` (`sld:`). It defines the metaschema classes used
to describe CWL's own record/enum/array schemas (`RecordSchema`, `EnumSchema`, `JsonldPredicate`, ...),
distinct from the CWL document vocabulary itself (see [CWL Ontology](bblocks://ogc.cwl.v1_2_1.CWLOntology)).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### RecordSchema and its named-field subtype
An excerpt of the metaschema vocabulary: `sld:SaladRecordSchema`, the schema-salad construct
used to define CWL's record types (e.g. `DockerRequirement`), is a subclass of the more general
`sld:RecordSchema`, and carries an `sld:abstract` property used to mark mixin base types.

#### turtle
```turtle
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

sld:RecordSchema a rdfs:Class .

sld:SaladRecordSchema a rdfs:Class ;
    rdfs:subClassOf sld:RecordSchema,
        sld:NamedType .

<https://w3id.org/cwl/salad#SaladRecordSchema/abstract> a rdf:Property ;
    rdfs:domain sld:SaladRecordSchema .

```


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/SchemaSaladOntology`

