
# CWLHintsItem (Schema)

`ogc.cwl.v1_2_1.requirements.CWLHintsItem` *v1.2.1*

A single entry of a process's `hints` list: any one of the
requirement/hint classes this register models (the standard CWL requirements, plus the
OGC-AP/WPS1/builtin hint classes), or `UnknownRequirement` as a fallback for any other
`class`-discriminated hint not otherwise recognized. Unlike `requirements`, an unsatisfied hint
must not cause a workflow engine to reject the process. Kept as its own reusable, `$ref`-able union
so downstream profiles can narrow the set of accepted hint classes without depending on
`extensionPoints`.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

For any new items added, ensure they are added under 'class' of 'UnknownRequirement' as well.
Otherwise, insufficiently restrictive classes could cause multiple matches, failing the 'oneOf' condition.

## Examples

### A standard requirement class used as a hint
Any of the standard [CWLRequirements](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirements) classes —
here `DockerRequirement` — can also appear as a `hints` entry, in which case an
implementation that cannot satisfy it should warn rather than fail the process.

#### json
```json
{
  "class": "DockerRequirement",
  "dockerPull": "docker.io/python:3-slim"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/context.jsonld",
  "class": "DockerRequirement",
  "dockerPull": "docker.io/python:3-slim"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] a <https://example.org/DockerRequirement> ;
    ns1:dockerPull "docker.io/python:3-slim" .


```


### An unrecognized hint class
A vendor- or implementation-specific hint whose `class` this register does not model
explicitly falls back to `UnknownRequirement`, which accepts any `class` not already claimed
by one of the other alternatives (the standard requirement classes, or this register's
`BuiltinRequirement`/[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement)/`WPS1Requirement`
hints).

#### json
```json
{
  "class": "acme:GPUAcceleration",
  "gpuCount": 1
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/context.jsonld",
  "class": "acme:GPUAcceleration",
  "gpuCount": 1
}
```

#### ttl
```ttl

[] a <acme:GPUAcceleration> .


```

## Schema

```yaml
$comment: 'For any new items added, ensure they are added under ''class'' of ''UnknownRequirement''
  as well.

  Otherwise, insufficiently restrictive classes could cause multiple matches, failing
  the ''oneOf'' condition.

  '
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/BuiltinRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/OGCAPIRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WPS1Requirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/UnknownRequirement/schema.yaml
title: CWLHintsItem

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
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
    "BuiltinRequirement": "ogccwl:BuiltinRequirement",
    "OGCAPIRequirement": "ogccwl:OGCAPIRequirement",
    "WPS1Requirement": "ogccwl:WPS1Requirement",
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
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHintsItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/CWLHintsItem`

