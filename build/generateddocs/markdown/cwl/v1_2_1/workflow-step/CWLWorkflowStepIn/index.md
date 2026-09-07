
# CWLWorkflowStepIn (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepIn` *v1.2.1*

Mapping of Workflow step inputs to nested CWL tool definitions inputs or outputs.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

A Workflow step's `in` field connects the step's input parameters to values coming from the
workflow's own inputs, from other steps' outputs, or from literal defaults. CWL allows `in` to be
written in two equivalent forms, captured here as a `oneOf`:

- **Map form** (`CWLWorkflowStepInMap`): an object keyed by input parameter name, where each value
  is either a bare `source` string, a list of `source` strings, or a full input object (see
  [CWLWorkflowStepInputBase](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase) and
  [CWLWorkflowStepInputDefault](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputDefault)).
- **List form** (`CWLWorkflowStepInList`): an array of
  [CWLWorkflowStepInItem](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInItem) objects, each of which
  carries its own `id` alongside the same wiring fields.

## Merging multiple inbound data links

If a step input's `source` names more than one upstream parameter, the values are combined
according to `linkMerge`
(see [LinkMergeMethod](bblocks://ogc.cwl.v1_2_1.LinkMergeMethod)): `merge_nested` (the default)
wraps each linked value into one entry of a result list, while `merge_flattened` concatenates
array-valued sources and appends scalar-valued sources into a single flat list. If `linkMerge` is
not specified and `source` has only one entry, the input takes that entry's value directly, without
being wrapped in a list.

CWL also defines a `pickValue` field for this purpose — evaluated after `linkMerge` and before
`scatter`/`valueFrom` — to select non-null values among several inbound links
(`first_non_null`, `the_only_non_null`, `all_non_null`); this is particularly useful alongside
conditional (`when`) steps, whose skipped runs produce `null`. This register's schema does not
currently model `pickValue` as a validated property.

## Other wiring fields

- `valueFrom` (see [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)): overrides or computes
  the final input value, optionally as a CWL parameter-reference expression evaluated against the
  `source` value (`self`) once `MultipleInputFeatureRequirement`/`StepInputExpressionRequirement`
  requirements are satisfied.
- `default` (see [CWLDefault](bblocks://ogc.cwl.v1_2_1.CWLDefault)): the value used when `source` is
  absent, or when the value it produces is `null`; applied before scattering or evaluating
  `valueFrom`.

## Examples

### Map form, with plain and object-valued sources
A step's `in` written as a map: `file1` is wired with a bare `source` string, while `file2`
and `file3` are wired with full input objects that also request how multiple inbound links
are merged. Adapted from CWL's `count-lines12-wf.cwl` and `conflict-wf.cwl` test fixtures.

#### json
```json
{
  "file1": "input_file",
  "file2": {
    "source": ["step_a/out", "step_b/out"],
    "linkMerge": "merge_flattened"
  },
  "file3": {
    "source": "step_c/out",
    "valueFrom": "$(self.basename)"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/context.jsonld",
  "@graph": [
    {
      "id": "file1",
      "source": "input_file"
    },
    {
      "id": "file2",
      "source": [
        "step_a/out",
        "step_b/out"
      ],
      "linkMerge": "merge_flattened"
    },
    {
      "id": "file3",
      "source": "step_c/out",
      "valueFrom": "$(self.basename)"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

<https://example.org/file1> cwl:source <https://example.org/input_file> .

<https://example.org/file2> cwl:linkMerge "merge_flattened" ;
    cwl:source <https://example.org/step_a/out>,
        <https://example.org/step_b/out> .

<https://example.org/file3> cwl:source <https://example.org/step_c/out> ;
    cwl:valueFrom "$(self.basename)" .


```


### List form, one entry per step input
The same kind of wiring expressed as a list, where each entry supplies its own `id` alongside
`source`/`linkMerge`/`default`.

#### json
```json
[
  {
    "id": "file1",
    "source": "input_file"
  },
  {
    "id": "file2",
    "source": ["step_a/out", "step_b/out"],
    "linkMerge": "merge_flattened",
    "default": "fallback.txt"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/context.jsonld",
  "@graph": [
    {
      "id": "file1",
      "source": "input_file"
    },
    {
      "id": "file2",
      "source": [
        "step_a/out",
        "step_b/out"
      ],
      "linkMerge": "merge_flattened",
      "default": "fallback.txt"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/file1> cwl:source <https://example.org/input_file> .

<https://example.org/file2> cwl:linkMerge "merge_flattened" ;
    cwl:source <https://example.org/step_a/out>,
        <https://example.org/step_b/out> ;
    sld:default ( "fallback.txt" ) .


```

## Schema

```yaml
description: Mapping of Workflow step inputs to nested CWL tool definitions inputs
  or outputs.
$defs:
  CWLWorkflowStepInMap:
    additionalProperties:
      oneOf:
      - type: string
      - items:
          type: string
        type: array
      - allOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputBase/schema.yaml
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInputDefault/schema.yaml
    type: object
  CWLWorkflowStepInList:
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepInItem/schema.yaml
    type: array
oneOf:
- $ref: '#/$defs/CWLWorkflowStepInMap'
- $ref: '#/$defs/CWLWorkflowStepInList'

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/schema.yaml)


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
    "id": "@id",
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "dct": "http://purl.org/dc/terms/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepIn`

