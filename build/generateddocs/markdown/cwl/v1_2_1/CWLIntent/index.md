
# CWLIntent (Schema)

`ogc.cwl.v1_2_1.CWLIntent` *v1.2.1*

An identifier for the type of computational operation a process
performs, especially useful for `Operation` but also usable on `CommandLineTool`, `Workflow`, or
`ExpressionTool`. If provided, must be an IRI of a concept node representing the operation type,
preferably defined within an ontology — for example an EDAM Ontology operation concept such as
`http://edamontology.org/operation_2928` (Alignment).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Intent expressed with EDAM Ontology operation concepts
A `CommandLineTool` that performs sequence alignment could declare its intent using an
[EDAM Ontology](http://edamontology.org/) operation concept IRI.

#### json
```json
[
  "http://edamontology.org/operation_2928"
]

```


### Multiple intents
A process may declare more than one operation type if it performs several distinct
computational operations.

#### json
```json
[
  "http://edamontology.org/operation_3199",
  "http://edamontology.org/operation_3432"
]

```

## Schema

```yaml
items:
  description: 'Identifier URL to a concept for the type of computational operation
    accomplished by this process

    (see example operations: http://edamontology.org/operation_0004).

    '
  format: url
  pattern: ^((?:http|ftp)s?://)?(?!.*//.*$)(?:(?:[A-Za-z0-9](?:[A-Za-z0-9-]{0,61}[A-Za-z0-9])?\.)+(?:[A-Za-z]{2,6}\.?|[A-Za-z0-9-]{2,}\.?)|localhost|\[[a-f0-9:]+\]|\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})(?::\d+)?(?:/?|[/?]\S+)$
  title: item
  type: string
title: CWLIntent
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIntent/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIntent/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLIntent`

