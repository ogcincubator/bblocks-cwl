
# CWLWorkflowStepInputDefault (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputDefault` *v1.2.1*

The 'default' property for a workflow step input, shared by the step input's list and map representations; not typically profiled on its own.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

CWL 'type' is not specified at this level for step inputs
(it is provided by the mapped input of the nested tool instead).
Therefore, cannot validate against 'CWLDefaultTypedConditional'.

## Examples

### Literal default value
A workflow step input that falls back to a literal string value when no
`source` is connected or the connected source produces `null`.

#### json
```json
{
  "default": "step1dir"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/context.jsonld",
  "default": "step1dir"
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] sld:default ( "step1dir" ) .


```


### Default value as a list
A workflow step input defaulting to a list of literal values.

#### json
```json
{
  "default": ["a", "b", "c"]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/context.jsonld",
  "default": [
    "a",
    "b",
    "c"
  ]
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

[] sld:default ( "a" "b" "c" ) .


```

## Schema

```yaml
$comment: 'CWL ''type'' is not specified at this level for step inputs

  (it is provided by the mapped input of the nested tool instead).

  Therefore, cannot validate against ''CWLDefaultTypedConditional''.

  '
properties:
  default:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefault/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/salad#default
    x-jsonld-container: '@list'
type: object
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
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
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepInputDefault`

