
# CWLDocumentation (Schema)

`ogc.cwl.v1_2_1.CWLDocumentation` *v1.2.1*

Shared human-readable documentation fields: a short `label` and a
longer free-text or multi-line `doc` description.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Label and single-string doc
A short `label` alongside a single-string `doc`, adapted from the CWL conformance test
`cat3-nodocker.cwl`.

#### json
```json
{
  "label": "cat3-nodocker.cwl",
  "doc": "Print the contents of a file to stdout using 'cat'."
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/context.jsonld",
  "label": "cat3-nodocker.cwl",
  "doc": "Print the contents of a file to stdout using 'cat'."
}
```

#### ttl
```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

[] rdfs:label "cat3-nodocker.cwl" ;
    rdfs:comment "Print the contents of a file to stdout using 'cat'." .


```


### Doc as an array of strings
`doc` may instead be given as an array of strings, rendered as separate paragraphs — useful
when documentation is authored in multiple parts.

#### json
```json
{
  "label": "align-and-sort",
  "doc": [
    "Aligns reads against a reference genome using bwa-mem.",
    "Sorts the resulting alignment with samtools sort before returning it."
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/context.jsonld",
  "label": "align-and-sort",
  "doc": [
    "Aligns reads against a reference genome using bwa-mem.",
    "Sorts the resulting alignment with samtools sort before returning it."
  ]
}
```

#### ttl
```ttl
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .

[] rdfs:label "align-and-sort" ;
    rdfs:comment "Aligns reads against a reference genome using bwa-mem.",
        "Sorts the resulting alignment with samtools sort before returning it." .


```

## Schema

```yaml
properties:
  doc:
    oneOf:
    - type: string
    - items:
        type: string
      type: array
    x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#comment
  label:
    type: string
    x-jsonld-id: http://www.w3.org/2000/01/rdf-schema#label
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLDocumentation`

