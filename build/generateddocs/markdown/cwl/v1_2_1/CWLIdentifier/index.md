
# CWLIdentifier (Schema)

`ogc.cwl.v1_2_1.CWLIdentifier` *v1.2.1*

Reference to the process identifier.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### UUID-form identifier
A process identifier expressed as a standard UUID.

#### json
```json
"550e8400-e29b-41d4-a716-446655440000"

```


### Text-pattern identifier with fragment reference
A process identifier following the [CWLTextPatternID](bblocks://ogc.cwl.v1_2_1.CWLTextPatternID)
pattern, referencing a sub-part definition inside a CWL document (as used, for example, by
`SchemaDefRequirement`).

#### json
```json
"sub/part#ref"

```

## Schema

```yaml
anyOf:
- description: Unique identifier.
  format: uuid
  pattern: ^[a-f0-9]{8}(?:-?[a-f0-9]{4}){3}-?[a-f0-9]{12}$
  title: UUID
  type: string
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml
description: Reference to the process identifier.
title: CWLIdentifier

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLIdentifier`

