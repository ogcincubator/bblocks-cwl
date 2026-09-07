
# CWLWorkflowClass (Schema)

`ogc.cwl.v1_2_1.CWLWorkflowClass` *v1.2.1*

The 'class: Workflow' discriminator, shared by the root Workflow document and its nested-in-step form; not typically profiled on its own.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Workflow class discriminator
The `class` field that identifies a document, or a nested step definition, as a CWL
[Workflow](bblocks://ogc.cwl.v1_2_1.CWLWorkflow).

#### json
```json
{
  "class": "Workflow"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowClass/context.jsonld",
  "class": "Workflow"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] a cwl:Workflow .


```

## Schema

```yaml
properties:
  class:
    enum:
    - Workflow
    type: string
    x-jsonld-id: '@type'
type: object
x-jsonld-extra-terms:
  Workflow: https://w3id.org/cwl/cwl#Workflow
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowClass/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowClass/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "Workflow": "cwl:Workflow",
    "class": "@type",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowClass/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLWorkflowClass`

