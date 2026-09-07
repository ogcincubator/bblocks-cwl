
# InplaceUpdateRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.InplaceUpdateRequirement` *v1.2.1*

If 'inplaceUpdate' is true, then an implementation supporting this feature may permit tools to directly
update files with 'writable: true' in 'InitialWorkDirRequirement'. That is, as an optimization,
files may be destructively modified in place as opposed to copied and updated
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InplaceUpdateRequirement).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

If `inplaceUpdate` is true, then an implementation supporting this feature may permit tools to
directly update files with `writable: true` in
[InitialWorkDirRequirement](bblocks://ogc.cwl.v1_2_1.requirements.InitialWorkDirRequirement). That is, as an
optimization, files may be destructively modified in place as opposed to copied and updated.

An implementation must ensure that only one workflow step may access a writable file at a time. It is
an error if a file which is writable by one workflow step is accessed (for reading or writing) by any
other workflow step running independently. However, a file which has been updated in a previous
completed step may be used as input to multiple steps, provided it is read-only in every step.

Workflow steps which modify a file must produce the modified file as output. Downstream steps which
further process the file must use the output of previous steps, and not refer to a common input (this
is necessary for both ordering and correctness).

Workflow authors should provide this in the `hints` section. The intent of this feature is that
workflows produce the same results whether or not `InplaceUpdateRequirement` is supported by the
implementation, and this feature is primarily available as an optimization for particular
environments.

Users and implementers should be aware that workflows that destructively modify inputs may not be
repeatable or reproducible. In particular, enabling this feature implies that `WorkReuse` should not
be enabled.

See also: the
[CWL v1.2 CommandLineTool spec — InplaceUpdateRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#InplaceUpdateRequirement).

## Examples

### Enabling in-place updates
An `InplaceUpdateRequirement` enabling destructive, in-place modification of a writable file or
directory staged by `InitialWorkDirRequirement`, as an execution-time optimization
(adapted from the CWL conformance tests `updatedir_inplace.cwl` and `updateval_inplace.cwl`).

#### json
```json
{
  "class": "InplaceUpdateRequirement",
  "inplaceUpdate": true
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/context.jsonld",
  "class": "InplaceUpdateRequirement",
  "inplaceUpdate": true
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#InplaceUpdateRequirement/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/InplaceUpdateRequirement> ;
    ns1:inplaceUpdate true .


```

## Schema

```yaml
additionalProperties: false
description: 'If ''inplaceUpdate'' is true, then an implementation supporting this
  feature may permit tools to directly

  update files with ''writable: true'' in ''InitialWorkDirRequirement''. That is,
  as an optimization,

  files may be destructively modified in place as opposed to copied and updated

  (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InplaceUpdateRequirement).

  '
properties:
  class:
    enum:
    - InplaceUpdateRequirement
    type: string
    x-jsonld-id: '@type'
  inplaceUpdate:
    title: inplaceUpdate
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#InplaceUpdateRequirement/inplaceUpdate
required:
- inplaceUpdate
title: InplaceUpdateRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "inplaceUpdate": "cwl:InplaceUpdateRequirement/inplaceUpdate",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/InplaceUpdateRequirement`

