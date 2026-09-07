
# OGCAPIRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.OGCAPIRequirement` *v1.2.1*

Hint indicating that the Application Package corresponds to an
OGC API - Processes provider that should be remotely executed and monitored
by this instance. (note: can only be an 'hint' as it is unofficial CWL specification).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

`OGCAPIRequirement` is an OGC-specific extension to the CWL requirement/hint vocabulary; it has no
upstream CWL specification counterpart. It marks a workflow step whose actual computation is not run
by the CWL runner itself but delegated to an external [OGC API - Processes](https://ogcapi.ogc.org/processes/)
`Process` resource, identified by the `process` property (a URL to the process's location, typically an
`https://.../processes/{processId}` endpoint per the OGC API - Processes conformance classes). The
runner is expected to submit an execution request to that endpoint (e.g. `POST /processes/{processId}/execution`)
and poll or subscribe for job status, rather than executing the step's `baseCommand`/`run` locally.

Because this class is not part of the official CWL v1.2.1 specification, it can only ever appear as a
*hint* — inside a [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLHintsItem) — never as a *requirement* (a
standards-conformant CWL processor is free to ignore hints it does not understand, but must reject a
document containing an unrecognized requirement). See also
[WPS1Requirement](bblocks://ogc.cwl.v1_2_1.requirements.WPS1Requirement) for the equivalent hint targeting a legacy
WPS 1.0 provider instead.

## Examples

### OGC API - Processes backing for a workflow step
An `OGCAPIRequirement` hint attached to a workflow step, indicating that the step's
execution should be delegated to a remote OGC API - Processes process offering rather
than run locally.

#### json
```json
{
  "class": "OGCAPIRequirement",
  "process": "https://example.org/ogcapi/processes/flood-detection"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/context.jsonld",
  "class": "OGCAPIRequirement",
  "process": "https://example.org/ogcapi/processes/flood-detection"
}
```

#### ttl
```ttl
@prefix ogccwl: <https://w3id.org/ogc/cwl/> .

[] a ogccwl:OGCAPIRequirement .


```

## Schema

```yaml
additionalProperties: false
description: 'Hint indicating that the Application Package corresponds to an

  OGC API - Processes provider that should be remotely executed and monitored

  by this instance. (note: can only be an ''hint'' as it is unofficial CWL specification).

  '
properties:
  class:
    enum:
    - OGCAPIRequirement
    type: string
    x-jsonld-id: '@type'
  process:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ReferenceURL/schema.yaml
    description: Process location.
required:
- process
title: OGCAPIRequirement
type: object
x-jsonld-extra-terms:
  OGCAPIRequirement: https://w3id.org/ogc/cwl/OGCAPIRequirement
x-jsonld-prefixes:
  ogccwl: https://w3id.org/ogc/cwl/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "OGCAPIRequirement": "ogccwl:OGCAPIRequirement",
    "class": "@type",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/OGCAPIRequirement`

