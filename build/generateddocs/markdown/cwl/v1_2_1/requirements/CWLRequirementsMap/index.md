
# CWLRequirementsMap (Schema)

`ogc.cwl.v1_2_1.requirements.CWLRequirementsMap` *v1.2.1*

Map-form (keyed by requirement class name) of the requirement types accepted by 'requirements'/'hints', shared between CWLRequirements and CWLHints; not typically profiled on its own.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Docker and shell command requirements
Map-form `requirements`/`hints` declaring both a Docker image to run the tool in
and that the tool relies on shell features (redirection, pipes) in its command
line.

#### json
```json
{
  "DockerRequirement": {
    "dockerPull": "docker.io/debian:stable-slim"
  },
  "ShellCommandRequirement": {}
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/context.jsonld",
  "DockerRequirement": {
    "dockerPull": "docker.io/debian:stable-slim"
  },
  "ShellCommandRequirement": {}
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] cwl:DockerRequirement [ ns1:dockerPull "docker.io/debian:stable-slim" ] ;
    cwl:ShellCommandRequirement [ ] .


```

## Schema

```yaml
additionalProperties: false
properties:
  DockerRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement
  EnvVarRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#EnvVarRequirement
  InitialWorkDirRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InitialWorkDirRequirement
  InlineJavascriptRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InlineJavascriptRequirement
  InplaceUpdateRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InplaceUpdateRequirement
  LoadListingRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#LoadListingRequirement
  MultipleInputFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/MultipleInputFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#MultipleInputFeatureRequirement
  NetworkAccess:
    $comment: Not 'NetworkAccessRequirement'
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#NetworkAccess
  ResourceRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement
  ScatterFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ScatterFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ScatterFeatureRequirement
  SchemaDefRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SchemaDefRequirement
  ShellCommandRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ShellCommandRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ShellCommandRequirement
  SoftwareRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwareRequirement
  StepInputExpressionRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/StepInputExpressionRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#StepInputExpressionRequirement
  SubworkflowFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SubworkflowFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SubworkflowFeatureRequirement
  ToolTimeLimit:
    $comment: Not 'ToolTimeLimitRequirement'.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ToolTimeLimit
  WorkReuse:
    $comment: Not 'WorkReuseRequirement'.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#WorkReuse
  cwltool:CUDARequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/cwltool-CUDARequirement/schema.yaml
    x-jsonld-id: http://commonwl.org/cwltool#CUDARequirement
title: CWLRequirementsMap
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#
  cwltool: http://commonwl.org/cwltool#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "DockerRequirement": {
      "@context": {
        "class": "@type",
        "dockerFile": "cwl:DockerRequirement/dockerFile",
        "dockerImageId": "cwl:DockerRequirement/dockerImageId",
        "dockerImport": "cwl:DockerRequirement/dockerImport",
        "dockerLoad": "cwl:DockerRequirement/dockerLoad",
        "dockerOutputDirectory": "cwl:DockerRequirement/dockerOutputDirectory",
        "dockerPull": "cwl:DockerRequirement/dockerPull"
      },
      "@id": "cwl:DockerRequirement"
    },
    "EnvVarRequirement": {
      "@context": {
        "class": "@type",
        "envDef": {
          "@context": {
            "envName": "cwl:EnvironmentDef/envName",
            "envValue": "cwl:EnvironmentDef/envValue"
          },
          "@id": "cwl:EnvVarRequirement/envDef",
          "@container": "@id"
        }
      },
      "@id": "cwl:EnvVarRequirement"
    },
    "InitialWorkDirRequirement": {
      "@context": {
        "class": "@type",
        "listing": "cwl:listing"
      },
      "@id": "cwl:InitialWorkDirRequirement"
    },
    "InlineJavascriptRequirement": {
      "@context": {
        "class": "@type",
        "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib"
      },
      "@id": "cwl:InlineJavascriptRequirement"
    },
    "InplaceUpdateRequirement": {
      "@context": {
        "class": "@type",
        "inplaceUpdate": "cwl:InplaceUpdateRequirement/inplaceUpdate"
      },
      "@id": "cwl:InplaceUpdateRequirement"
    },
    "LoadListingRequirement": {
      "@context": {
        "class": "@type",
        "loadListing": "cwl:loadListing"
      },
      "@id": "cwl:LoadListingRequirement"
    },
    "MultipleInputFeatureRequirement": "cwl:MultipleInputFeatureRequirement",
    "NetworkAccess": {
      "@context": {
        "class": "@type",
        "networkAccess": "cwl:NetworkAccess/networkAccess"
      },
      "@id": "cwl:NetworkAccess"
    },
    "ResourceRequirement": {
      "@context": {
        "class": "@type",
        "coresMin": "cwl:ResourceRequirement/coresMin",
        "coresMax": "cwl:ResourceRequirement/coresMax",
        "ramMin": "cwl:ResourceRequirement/ramMin",
        "ramMax": "cwl:ResourceRequirement/ramMax",
        "outdirMin": "cwl:ResourceRequirement/outdirMin",
        "outdirMax": "cwl:ResourceRequirement/outdirMax",
        "tmpdirMin": "cwl:ResourceRequirement/tmpdirMin",
        "tmpdirMax": "cwl:ResourceRequirement/tmpdirMax"
      },
      "@id": "cwl:ResourceRequirement"
    },
    "ScatterFeatureRequirement": "cwl:ScatterFeatureRequirement",
    "SchemaDefRequirement": {
      "@context": {
        "class": "@type",
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
                "streamable": "cwl:FieldBase/streamable",
                "loadListing": "cwl:loadListing"
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
        }
      },
      "@id": "cwl:SchemaDefRequirement"
    },
    "ShellCommandRequirement": "cwl:ShellCommandRequirement",
    "SoftwareRequirement": {
      "@context": {
        "class": "@type",
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
        }
      },
      "@id": "cwl:SoftwareRequirement"
    },
    "StepInputExpressionRequirement": "cwl:StepInputExpressionRequirement",
    "SubworkflowFeatureRequirement": "cwl:SubworkflowFeatureRequirement",
    "ToolTimeLimit": {
      "@context": {
        "class": "@type",
        "timelimit": "cwl:ToolTimeLimit/timelimit"
      },
      "@id": "cwl:ToolTimeLimit"
    },
    "WorkReuse": {
      "@context": {
        "class": "@type",
        "enableReuse": "cwl:WorkReuse/enableReuse"
      },
      "@id": "cwl:WorkReuse"
    },
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
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
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsMap/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/CWLRequirementsMap`

