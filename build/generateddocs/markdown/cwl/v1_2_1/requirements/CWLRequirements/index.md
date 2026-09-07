
# CWLRequirements (Schema)

`ogc.cwl.v1_2_1.requirements.CWLRequirements` *v1.2.1*

Explicit requirement to execute the application package.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Declares requirements that apply to either the runtime environment or the workflow engine
that **must** be met in order to execute a `CommandLineTool` or `Workflow`. If an
implementation cannot satisfy all requirements, or a requirement is listed which is not
recognized by the implementation, it is a fatal error and the implementation must not
attempt to run the process, unless overridden at user option.

This is CWL's principal extension mechanism: any of the 18 requirement classes covered by
[CWLRequirementsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsItem) — `DockerRequirement`,
`ResourceRequirement`, `InitialWorkDirRequirement`, and so on — can be listed here to opt a
process in to that behavior. `requirements` is contrasted with
[CWLHints](bblocks://ogc.cwl.v1_2_1.requirements.CWLHints), which declares the same kind of information
but non-fatally: an implementation that does not recognize or cannot satisfy a hint is free
to ignore it and proceed.

Requirements can be written in two equivalent forms:

- a **list**, where each entry carries its own `class` field naming the requirement type, and
  may alternatively be an [`$import`](bblocks://ogc.cwl.v1_2_1.CWLImport) directive pulling
  requirements in from another file; or
- a **map** ([CWLRequirementsMap](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsMap)) keyed by
  requirement class name, where `class` is implied by the key and does not need to be
  repeated.

Requirements are inherited from any enclosing `Workflow` down to nested steps, and
requirements on a step or a `CommandLineTool` override an inherited requirement of the same
`class`.

## Examples

### Requirements as a list
A `CommandLineTool` running inside a Docker container, with inline Javascript
expressions enabled. Each list item names its own `class`.

#### json
```json
[
  {
    "class": "DockerRequirement",
    "dockerPull": "docker.io/debian:stable-slim"
  },
  {
    "class": "InlineJavascriptRequirement",
    "expressionLib": [
      "function foo() { return 1; }"
    ]
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/context.jsonld",
  "@graph": [
    {
      "class": "DockerRequirement",
      "dockerPull": "docker.io/debian:stable-slim"
    },
    {
      "class": "InlineJavascriptRequirement",
      "expressionLib": [
        "function foo() { return 1; }"
      ]
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#InlineJavascriptRequirement/> .
@prefix ns2: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] a cwl:InlineJavascriptRequirement ;
    ns1:expressionLib "function foo() { return 1; }" .

[] a cwl:DockerRequirement ;
    ns2:dockerPull "docker.io/debian:stable-slim" .


```


### Requirements as a map
The same kind of declaration, using the equivalent map form: the requirement
class name becomes the property key, so `class` does not need to be repeated.

#### json
```json
{
  "DockerRequirement": {
    "dockerPull": "docker.io/debian:stable-slim"
  },
  "ResourceRequirement": {
    "coresMin": 1.25,
    "coresMax": 1.75
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/context.jsonld",
  "DockerRequirement": {
    "dockerPull": "docker.io/debian:stable-slim"
  },
  "ResourceRequirement": {
    "coresMin": 1.25,
    "coresMax": 1.75
  }
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#ResourceRequirement/> .
@prefix ns2: <https://w3id.org/cwl/cwl#DockerRequirement/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] cwl:DockerRequirement [ ns2:dockerPull "docker.io/debian:stable-slim" ] ;
    cwl:ResourceRequirement [ ns1:coresMax 1.75e+00 ;
            ns1:coresMin 1.25e+00 ] .


```

## Schema

```yaml
$defs:
  CWLRequirementsList:
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
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    title: CWLRequirementsList
    type: array
description: Explicit requirement to execute the application package.
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/schema.yaml
- $ref: '#/$defs/CWLRequirementsList'
title: CWLRequirements

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/schema.yaml)


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
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/CWLRequirements`

