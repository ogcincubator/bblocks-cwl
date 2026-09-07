
# WPS1Requirement (Schema)

`ogc.cwl.v1_2_1.requirements.WPS1Requirement` *v1.2.1*

Hint indicating that the Application Package corresponds to a
WPS-1 provider process that should be remotely executed and monitored by this
instance. (note: can only be an ''hint'' as it is unofficial CWL specification).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

`WPS1Requirement` is an OGC-specific extension to the CWL requirement/hint vocabulary; it has no
upstream CWL specification counterpart. It marks a workflow step whose actual computation is not run
by the CWL runner itself but delegated to a remote [WPS 1.0](https://www.ogc.org/standard/wps/) process,
identified by two properties: `provider` (the WPS endpoint URL, i.e. the base URL to which
`Execute`/`GetCapabilities`/`DescribeProcess` requests are sent) and `process` (the WPS process
identifier to invoke at that endpoint, as used in the `Identifier` element of a WPS `Execute` request).
The runner is expected to submit a WPS `Execute` request against that process and poll for completion,
rather than executing the step's `baseCommand`/`run` locally.

Because this class is not part of the official CWL v1.2.1 specification, it can only ever appear as a
*hint* — inside a [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLHintsItem) — never as a *requirement* (a
standards-conformant CWL processor is free to ignore hints it does not understand, but must reject a
document containing an unrecognized requirement). See also
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement) for the equivalent hint targeting a
modern OGC API - Processes provider instead.

## Examples

### WPS 1.0 backing for a workflow step
A `WPS1Requirement` hint attached to a workflow step, indicating that the step's
execution should be delegated to a remote WPS 1.0 provider, identifying both the
provider endpoint and the process identifier to invoke on it.

#### json
```json
{
  "class": "WPS1Requirement",
  "provider": "https://example.org/wps",
  "process": "FloodDetection"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/context.jsonld",
  "class": "WPS1Requirement",
  "provider": "https://example.org/wps",
  "process": "FloodDetection"
}
```

#### ttl
```ttl
@prefix ogccwl: <https://w3id.org/ogc/cwl/> .

[] a ogccwl:WPS1Requirement .


```

## Schema

```yaml
additionalProperties: false
description: 'Hint indicating that the Application Package corresponds to a

  WPS-1 provider process that should be remotely executed and monitored by this

  instance. (note: can only be an ''''hint'''' as it is unofficial CWL specification).

  '
properties:
  class:
    enum:
    - WPS1Requirement
    type: string
    x-jsonld-id: '@type'
  process:
    $comment: Process identifier of the remote WPS provider.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml
  provider:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ReferenceURL/schema.yaml
    description: WPS provider endpoint.
required:
- process
- provider
title: WPS1Requirement
type: object
x-jsonld-extra-terms:
  WPS1Requirement: https://w3id.org/ogc/cwl/WPS1Requirement
x-jsonld-prefixes:
  ogccwl: https://w3id.org/ogc/cwl/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "WPS1Requirement": "ogccwl:WPS1Requirement",
    "class": "@type",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/WPS1Requirement`

