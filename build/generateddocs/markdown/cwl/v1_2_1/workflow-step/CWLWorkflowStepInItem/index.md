
# CWLWorkflowStepInItem (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInItem` *v1.2.1*

A single entry of a Workflow step's `in` mapping, in its
list form: combines the step-input id, the common wiring fields (`source`, `linkMerge`,
`valueFrom`), and the optional `default` value used when a source produces no data.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Simple single-source input
A step input identified by `id`, wired to a single upstream parameter via `source`.

#### json
```json
{
  "id": "file1",
  "source": "input_file"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/context.jsonld",
  "id": "file1",
  "source": "input_file"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

<https://example.org/file1> cwl:source <https://example.org/input_file> .


```


### Merged multi-source input with a default
A step input fed by two upstream data links, flattened via `linkMerge`, with a `default`
value used when no data is produced by any source.

#### json
```json
{
  "id": "file2",
  "source": ["step_a/out", "step_b/out"],
  "linkMerge": "merge_flattened",
  "default": "fallback.txt"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/context.jsonld",
  "id": "file2",
  "source": [
    "step_a/out",
    "step_b/out"
  ],
  "linkMerge": "merge_flattened",
  "default": "fallback.txt"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/file2> cwl:linkMerge "merge_flattened" ;
    cwl:source <https://example.org/step_a/out>,
        <https://example.org/step_b/out> ;
    sld:default ( "fallback.txt" ) .


```

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "id": "@id",
    "linkMerge": "cwl:linkMerge",
    "source": {
      "@id": "cwl:source",
      "@type": "@id"
    },
    "valueFrom": "cwl:valueFrom",
    "default": {
      "@context": {
        "basename": "cwl:basename",
        "class": "@type",
        "location": "@id",
        "nameroot": "cwl:File/nameroot",
        "path": {
          "@id": "cwl:path",
          "@type": "@id"
        }
      },
      "@id": "sld:default",
      "@container": "@list"
    },
    "dct": "http://purl.org/dc/terms/",
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepInItem`

