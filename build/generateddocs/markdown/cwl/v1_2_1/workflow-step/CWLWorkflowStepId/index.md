
# CWLWorkflowStepId (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepId` *v1.2.1*

The `id` field required on a Workflow step when `steps` is given
as a list rather than a map: identifies the step within the workflow.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Step identifier
The `id` field of a workflow step given in the list form of `steps`.

#### json
```json
{
  "id": "step1"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/context.jsonld",
  "id": "step1",
  "dct:identifier": "step1"
}
```

#### ttl
```ttl
@prefix dcterms: <http://purl.org/dc/terms/> .

<https://example.org/step1> dcterms:identifier "step1" .


```

## Schema

```yaml
properties:
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
    x-jsonld-id: '@id'
required:
- id
type: object
x-jsonld-prefixes:
  dct: http://purl.org/dc/terms/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/schema.yaml)


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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepId`

