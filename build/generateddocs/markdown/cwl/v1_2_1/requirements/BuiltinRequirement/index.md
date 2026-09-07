
# BuiltinRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.BuiltinRequirement` *v1.2.1*

Hint indicating that the Application Package corresponds to a
builtin process of this instance. (note: can only be an 'hint'
as it is unofficial CWL specification).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

This is an OGC-specific extension hint, not part of the core CWL v1.2 specification. It marks a
workflow step's Application Package as corresponding to a process the executing instance already
implements natively — a "builtin" — rather than one that must be run from a container image
(see [DockerRequirement](bblocks://ogc.cwl.v1_2_1.requirements.DockerRequirement)) or delegated to a remote
execution backend. Because this is unofficial, `class: BuiltinRequirement` may only be used under
`hints`, never under `requirements` — a correct engine unaware of it must reject an unrecognized
class under `requirements` as fatal, but may safely ignore it under `hints` — see
[CWLHints](bblocks://ogc.cwl.v1_2_1.requirements.CWLHints).

`BuiltinRequirement` is one of three such OGC-specific hints an instance can use to say how a step's
Application Package should actually be executed, alongside
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement) (delegate to a remote OGC API -
Processes offering) and [WPS1Requirement](bblocks://ogc.cwl.v1_2_1.requirements.WPS1Requirement) (delegate to a
remote WPS-1 provider process). Unlike those two, `BuiltinRequirement` names a process already known
to the local instance rather than a remote one, so its `process` property is a plain identifier
(`CWLTextPatternID`) rather than a `ReferenceURL` to an external endpoint.

## Examples

### Builtin process hint for a natively-implemented step
A `BuiltinRequirement` hint indicating that a workflow step corresponds to a process
already implemented natively by this instance, identified by process ID, rather than
requiring a container image or delegation to a remote execution backend.

#### json
```json
{
  "class": "BuiltinRequirement",
  "process": "eoepca.processes.buffer"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/context.jsonld",
  "class": "BuiltinRequirement",
  "process": "eoepca.processes.buffer"
}
```

#### ttl
```ttl
@prefix ogccwl: <https://w3id.org/ogc/cwl/> .

[] a ogccwl:BuiltinRequirement .


```

## Schema

```yaml
additionalProperties: false
description: 'Hint indicating that the Application Package corresponds to a

  builtin process of this instance. (note: can only be an ''hint''

  as it is unofficial CWL specification).

  '
properties:
  class:
    enum:
    - BuiltinRequirement
    type: string
    x-jsonld-id: '@type'
  process:
    $comment: Builtin process identifier.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml
required:
- process
- class
title: BuiltinRequirement
type: object
x-jsonld-extra-terms:
  BuiltinRequirement: https://w3id.org/ogc/cwl/BuiltinRequirement
x-jsonld-prefixes:
  ogccwl: https://w3id.org/ogc/cwl/

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "BuiltinRequirement": "ogccwl:BuiltinRequirement",
    "class": "@type",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/BuiltinRequirement`

