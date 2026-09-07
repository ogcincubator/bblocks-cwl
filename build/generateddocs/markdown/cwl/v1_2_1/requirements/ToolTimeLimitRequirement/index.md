
# ToolTimeLimitRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.ToolTimeLimitRequirement` *v1.2.1*

Set an upper limit on the execution time of a CommandLineTool.

A CommandLineTool whose execution duration exceeds the time limit may be preemptively
terminated and considered failed. May also be used by batch systems to make scheduling decisions.

The execution duration excludes external operations, such as staging of files,
pulling a docker image etc., and only counts wall-time for the execution of the command line itself.


[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Fixed time limit in seconds
A `CommandLineTool` requirement that terminates execution if it runs for more than 3 seconds
of wall-clock time.

#### json
```json
{
  "class": "ToolTimeLimit",
  "timelimit": 3
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/context.jsonld",
  "class": "ToolTimeLimit",
  "timelimit": 3
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#ToolTimeLimit/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/ToolTimeLimit> ;
    ns1:timelimit 3 .


```


### Time limit computed from a CWL expression
The `timelimit` field may also be set to a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression),
evaluated at runtime, instead of a fixed number of seconds. This requires
`InlineJavascriptRequirement` to also be present in the enclosing process.

#### json
```json
{
  "class": "ToolTimeLimit",
  "timelimit": "$(1 + 2)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/context.jsonld",
  "class": "ToolTimeLimit",
  "timelimit": "$(1 + 2)"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#ToolTimeLimit/> .

[] a <https://example.org/ToolTimeLimit> ;
    ns1:timelimit "$(1 + 2)" .


```

## Schema

```yaml
additionalProperties: false
description: 'Set an upper limit on the execution time of a CommandLineTool.


  A CommandLineTool whose execution duration exceeds the time limit may be preemptively

  terminated and considered failed. May also be used by batch systems to make scheduling
  decisions.


  The execution duration excludes external operations, such as staging of files,

  pulling a docker image etc., and only counts wall-time for the execution of the
  command line itself.

  '
properties:
  class:
    $comment: not 'ToolTimeLimitRequirement'
    enum:
    - ToolTimeLimit
    type: string
    x-jsonld-id: '@type'
  timelimit:
    description: 'The time limit, in seconds.


      A time limit of zero means no time limit.

      Negative time limits are an error.

      '
    oneOf:
    - minimum: 0.0
      type: number
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    title: TimeLimitValue
    x-jsonld-id: https://w3id.org/cwl/cwl#ToolTimeLimit/timelimit
required:
- timelimit
title: ToolTimeLimitRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "timelimit": "cwl:ToolTimeLimit/timelimit",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/ToolTimeLimitRequirement`

