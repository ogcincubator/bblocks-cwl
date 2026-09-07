
# CWLHints (Schema)

`ogc.cwl.v1_2_1.requirements.CWLHints` *v1.2.1*

Non-failing additional hints that can help resolve extra requirements.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Declares hints applying to either the runtime environment or the workflow engine that may be
helpful in executing a process. Structurally, `hints` accepts the same shapes as
[CWLRequirements](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirements) — either a mapping keyed by `class`, or
a list of [CWLHintsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLHintsItem) entries (or `$import` directives)
each carrying an explicit `class` — but the two fields differ in what a workflow engine must do
with them.

`requirements` are mandatory: if an implementation cannot satisfy one, it must treat this as a
fatal error and must not run the process (unless overridden at user option). `hints`, by contrast,
are advisory: it is not an error if an implementation cannot satisfy all hints, though it may
report a warning. This makes `hints` the natural place to carry optional or non-standard,
implementation-specific extensions — such as this register's own
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement) and `WPS1Requirement`, which tell
an OGC-aware runner to delegate execution to a remote OGC API - Processes or WPS-1 provider —
without breaking engines that don't recognize them, since any unrecognized `class` still falls
back to `UnknownRequirement`.

## Examples

### Hints as a list
A `CommandLineTool`'s `hints` given as a list, adapted from the CWL conformance test
`bwa-mem-tool.cwl`. Each entry needs an explicit `class` because, unlike the mapping form,
nothing else identifies which hint it is. Since hints are advisory, an engine that cannot
honor `ResourceRequirement`'s `coresMin` should still attempt to run the tool.

#### json
```json
[
  {
    "class": "ResourceRequirement",
    "coresMin": 2
  },
  {
    "class": "DockerRequirement",
    "dockerPull": "docker.io/python:3-slim"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/context.jsonld",
  "@graph": [
    {
      "class": "ResourceRequirement",
      "coresMin": 2
    },
    {
      "class": "DockerRequirement",
      "dockerPull": "docker.io/python:3-slim"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .
@prefix ns2: <https://w3id.org/cwl/cwl#ResourceRequirement/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a cwl:ResourceRequirement ;
    ns2:coresMin 2 .

[] a cwl:DockerRequirement ;
    ns1:dockerPull "docker.io/python:3-slim" .


```


### Hints as a map with an OGC-specific hint
`hints` given as a mapping keyed by `class`, using this register's non-standard
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement) to hint that the process
should be delegated to a remote OGC API - Processes provider. Because it is a hint rather
than a requirement, an engine unaware of `OGCAPIRequirement` may ignore it instead of
rejecting the process outright.

#### json
```json
{
  "OGCAPIRequirement": {
    "process": "https://example.org/ogcapi/processes/reproject"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/context.jsonld",
  "@graph": [
    {
      "class": "OGCAPIRequirement",
      "process": "https://example.org/ogcapi/processes/reproject"
    }
  ]
}
```

#### ttl
```ttl
@prefix ogccwl: <https://w3id.org/ogc/cwl/> .

[] a ogccwl:OGCAPIRequirement .


```

## Schema

```yaml
description: Non-failing additional hints that can help resolve extra requirements.
$defs:
  CWLHintsMap:
    anyOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/schema.yaml
    - additionalProperties:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/UnknownRequirement/schema.yaml
      properties:
        BuiltinRequirement:
          $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/schema.yaml
        OGCAPIRequirement:
          $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/schema.yaml
        WPS1Requirement:
          $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/schema.yaml
      type: object
    title: CWLHintsMap
  CWLHintsList:
    items:
      oneOf:
      - allOf:
        - $comment: 'When using the list representation, ''class'' is required to
            indicate which one is being represented.

            When using the mapping representation, ''class'' is optional since it''s
            the key, but it must match by name.

            '
          required:
          - class
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    title: CWLHintsList
    type: array
oneOf:
- $ref: '#/$defs/CWLHintsMap'
- $ref: '#/$defs/CWLHintsList'
title: CWLHints

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "DockerRequirement": "cwl:DockerRequirement",
    "EnvVarRequirement": "cwl:EnvVarRequirement",
    "InitialWorkDirRequirement": "cwl:InitialWorkDirRequirement",
    "InlineJavascriptRequirement": "cwl:InlineJavascriptRequirement",
    "InplaceUpdateRequirement": "cwl:InplaceUpdateRequirement",
    "LoadListingRequirement": "cwl:LoadListingRequirement",
    "MultipleInputFeatureRequirement": "cwl:MultipleInputFeatureRequirement",
    "NetworkAccess": "cwl:NetworkAccess",
    "ResourceRequirement": "cwl:ResourceRequirement",
    "ScatterFeatureRequirement": "cwl:ScatterFeatureRequirement",
    "SchemaDefRequirement": "cwl:SchemaDefRequirement",
    "ShellCommandRequirement": "cwl:ShellCommandRequirement",
    "SoftwareRequirement": "cwl:SoftwareRequirement",
    "StepInputExpressionRequirement": "cwl:StepInputExpressionRequirement",
    "SubworkflowFeatureRequirement": "cwl:SubworkflowFeatureRequirement",
    "ToolTimeLimit": "cwl:ToolTimeLimit",
    "WorkReuse": "cwl:WorkReuse",
    "class": "@type",
    "BuiltinRequirement": "ogccwl:BuiltinRequirement",
    "OGCAPIRequirement": "ogccwl:OGCAPIRequirement",
    "WPS1Requirement": "ogccwl:WPS1Requirement",
    "dockerFile": "cwl:DockerRequirement/dockerFile",
    "dockerImageId": "cwl:DockerRequirement/dockerImageId",
    "dockerImport": "cwl:DockerRequirement/dockerImport",
    "dockerLoad": "cwl:DockerRequirement/dockerLoad",
    "dockerOutputDirectory": "cwl:DockerRequirement/dockerOutputDirectory",
    "dockerPull": "cwl:DockerRequirement/dockerPull",
    "packages": {
      "@context": {
        "package": "cwl:SoftwarePackage/package",
        "specs": {
          "@id": "cwl:SoftwarePackage/specs",
          "@type": "@id"
        },
        "version": "cwl:SoftwarePackage/version"
      },
      "@id": "cwl:SoftwareRequirement/packages",
      "@container": "@id"
    },
    "envDef": {
      "@context": {
        "envName": "cwl:EnvironmentDef/envName",
        "envValue": "cwl:EnvironmentDef/envValue"
      },
      "@id": "cwl:EnvVarRequirement/envDef",
      "@container": "@id"
    },
    "types": {
      "@context": {
        "type": {
          "@id": "sld:type",
          "@type": "@vocab"
        },
        "fields": {
          "@context": {
            "format": {
              "@id": "cwl:format",
              "@type": "@id"
            },
            "loadContents": "cwl:loadContents",
            "secondaryFiles": "cwl:secondaryFiles",
            "streamable": "cwl:FieldBase/streamable"
          },
          "@id": "sld:fields",
          "@container": "@id"
        },
        "name": "@id",
        "items": {
          "@id": "sld:items",
          "@type": "@vocab"
        }
      },
      "@id": "cwl:SchemaDefRequirement/types"
    },
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
    "listing": "cwl:listing",
    "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib",
    "inplaceUpdate": "cwl:InplaceUpdateRequirement/inplaceUpdate",
    "loadListing": "cwl:loadListing",
    "networkAccess": "cwl:NetworkAccess/networkAccess",
    "coresMin": "cwl:ResourceRequirement/coresMin",
    "coresMax": "cwl:ResourceRequirement/coresMax",
    "ramMin": "cwl:ResourceRequirement/ramMin",
    "ramMax": "cwl:ResourceRequirement/ramMax",
    "outdirMin": "cwl:ResourceRequirement/outdirMin",
    "outdirMax": "cwl:ResourceRequirement/outdirMax",
    "tmpdirMin": "cwl:ResourceRequirement/tmpdirMin",
    "tmpdirMax": "cwl:ResourceRequirement/tmpdirMax",
    "timelimit": "cwl:ToolTimeLimit/timelimit",
    "enableReuse": "cwl:WorkReuse/enableReuse",
    "null": "sld:null",
    "boolean": "xsd:boolean",
    "int": "xsd:int",
    "integer": "xsd:int",
    "long": "xsd:long",
    "float": "xsd:float",
    "double": "xsd:double",
    "string": "xsd:string",
    "File": "cwl:File",
    "Directory": "cwl:Directory",
    "cwl": "https://w3id.org/cwl/cwl#",
    "cwltool": "http://commonwl.org/cwltool#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/CWLHints`

