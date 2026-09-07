
# CWLWorkflowStepInputBase (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase` *v1.2.1*

Common workflow step input properties (source, linkMerge, valueFrom), shared by the step input's list and map representations; not typically profiled on its own.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Single source
Wiring a step input to one upstream parameter.

#### json
```json
{
  "source": "step_a/out"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/context.jsonld",
  "source": "step_a/out"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] cwl:source <https://example.org/step_a/out> .


```


### Multiple sources with link merging and a value expression
Wiring a step input to several upstream parameters, flattening them via `linkMerge`, and
post-processing the merged value with `valueFrom`.

#### json
```json
{
  "source": ["step_a/out", "step_b/out"],
  "linkMerge": "merge_flattened",
  "valueFrom": "$(self.length)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/context.jsonld",
  "source": [
    "step_a/out",
    "step_b/out"
  ],
  "linkMerge": "merge_flattened",
  "valueFrom": "$(self.length)"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] cwl:linkMerge "merge_flattened" ;
    cwl:source <https://example.org/step_a/out>,
        <https://example.org/step_b/out> ;
    cwl:valueFrom "$(self.length)" .


```

## Schema

```yaml
properties:
  linkMerge:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LinkMergeMethod/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#linkMerge
  source:
    oneOf:
    - type: string
    - items:
        type: string
      type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#source
    x-jsonld-type: '@id'
  valueFrom:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#valueFrom
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "linkMerge": "cwl:linkMerge",
    "source": {
      "@id": "cwl:source",
      "@type": "@id"
    },
    "valueFrom": "cwl:valueFrom",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepInputBase`

