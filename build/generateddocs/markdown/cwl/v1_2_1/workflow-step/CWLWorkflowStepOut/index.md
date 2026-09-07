
# CWLWorkflowStepOut (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepOut` *v1.2.1*

Mapping of Workflow step inputs to nested CWL tool definitions inputs or outputs.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Output identifiers as plain strings
The most common form: each entry names an output parameter of the underlying
process, using it directly as the step's output identifier.

#### json
```json
["count_output", "fileout"]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": {
    "@list": [
      "count_output",
      "fileout"
    ]
  }
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value ( "count_output" "fileout" ) .


```


### Output identifier as an object
Instead of a bare string, an output entry may be given as an object carrying an
`id` field, allowing further properties to be attached to it.

#### json
```json
[{"id": "count_output"}]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/context.jsonld",
  "@graph": [
    {
      "id": "count_output",
      "dct:identifier": "count_output"
    }
  ]
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .

<https://example.org/count_output> dcterms:identifier "count_output" .


```

## Schema

```yaml
description: Mapping of Workflow step inputs to nested CWL tool definitions inputs
  or outputs.
items:
  oneOf:
  - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
  - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/schema.yaml
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "id": "@id",
    "dct": "http://purl.org/dc/terms/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepOut`

