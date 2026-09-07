
# WorkReuseRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.WorkReuseRequirement` *v1.2.1*

For implementations that support reusing output from past work
(on the assumption that same code and same input produce same results),
control whether to enable or disable the reuse behavior for a particular tool
or step (to accommodate situations where that assumption is incorrect).

A reused step is not executed but instead returns the same output as the original execution.

If 'WorkReuse' is not specified, correct tools should assume it is enabled by default.


[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Disabling work reuse
A `CommandLineTool` that disables output reuse, forcing re-execution on every run — adapted
from the CWL v1.2 conformance test suite, where this is combined with a `ToolTimeLimit` to
test that a re-run is not skipped by reuse of a previous (successful) execution.

#### json
```json
{
  "class": "WorkReuse",
  "enableReuse": false
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/context.jsonld",
  "class": "WorkReuse",
  "enableReuse": false
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#WorkReuse/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/WorkReuse> ;
    ns1:enableReuse false .


```


### Work reuse controlled by an expression
`enableReuse` may also be a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression), evaluated
at runtime, when combined with `InlineJavascriptRequirement`.

#### json
```json
{
  "class": "WorkReuse",
  "enableReuse": "$(inputs.allowCaching)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/context.jsonld",
  "class": "WorkReuse",
  "enableReuse": "$(inputs.allowCaching)"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#WorkReuse/> .

[] a <https://example.org/WorkReuse> ;
    ns1:enableReuse "$(inputs.allowCaching)" .


```

## Schema

```yaml
additionalProperties: false
description: 'For implementations that support reusing output from past work

  (on the assumption that same code and same input produce same results),

  control whether to enable or disable the reuse behavior for a particular tool

  or step (to accommodate situations where that assumption is incorrect).


  A reused step is not executed but instead returns the same output as the original
  execution.


  If ''WorkReuse'' is not specified, correct tools should assume it is enabled by
  default.

  '
properties:
  class:
    $comment: Not 'WorkReuseRequirement'.
    enum:
    - WorkReuse
    type: string
    x-jsonld-id: '@type'
  enableReuse:
    description: 'Indicates if reuse is enabled for this tool.


      Can be an expression when combined with ''InlineJavascriptRequirement''

      (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#Expression).

      '
    oneOf:
    - type: boolean
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    title: EnableReuseValue
    x-jsonld-id: https://w3id.org/cwl/cwl#WorkReuse/enableReuse
required:
- enableReuse
title: WorkReuseRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "enableReuse": "cwl:WorkReuse/enableReuse",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/WorkReuseRequirement`

