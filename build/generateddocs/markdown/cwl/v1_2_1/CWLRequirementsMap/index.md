
# CWLRequirementsMap (Schema)

`ogc.cwl.v1_2_1.CWLRequirementsMap` *v1.2.1*

CWLRequirementsMap

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
additionalProperties: false
properties:
  DockerRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/DockerRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement
  EnvVarRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/EnvVarRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#EnvVarRequirement
  InitialWorkDirRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InitialWorkDirRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InitialWorkDirRequirement
  InlineJavascriptRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InlineJavascriptRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InlineJavascriptRequirement
  InplaceUpdateRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InplaceUpdateRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#InplaceUpdateRequirement
  LoadListingRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LoadListingRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#LoadListingRequirement
  MultipleInputFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/MultipleInputFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#MultipleInputFeatureRequirement
  NetworkAccess:
    $comment: Not 'NetworkAccessRequirement'
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/NetworkAccessRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#NetworkAccess
  ResourceRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ResourceRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ResourceRequirement
  ScatterFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ScatterFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ScatterFeatureRequirement
  SchemaDefRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SchemaDefRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SchemaDefRequirement
  ShellCommandRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ShellCommandRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ShellCommandRequirement
  SoftwareRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwareRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwareRequirement
  StepInputExpressionRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/StepInputExpressionRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#StepInputExpressionRequirement
  SubworkflowFeatureRequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SubworkflowFeatureRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#SubworkflowFeatureRequirement
  ToolTimeLimit:
    $comment: Not 'ToolTimeLimitRequirement'.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ToolTimeLimitRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#ToolTimeLimit
  WorkReuse:
    $comment: Not 'WorkReuseRequirement'.
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/WorkReuseRequirement/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#WorkReuse
  cwltool:CUDARequirement:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/cwltool-CUDARequirement/schema.yaml
title: CWLRequirementsMap
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirementsMap/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirementsMap/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "DockerRequirement": {
      "@context": {
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
        "envName": "cwl:EnvironmentDef/envName",
        "envValue": "cwl:EnvironmentDef/envValue"
      },
      "@id": "cwl:EnvVarRequirement"
    },
    "InitialWorkDirRequirement": {
      "@context": {
        "writable": "cwl:Dirent/writable",
        "checksum": "cwl:File/checksum",
        "size": "cwl:File/size"
      },
      "@id": "cwl:InitialWorkDirRequirement"
    },
    "InlineJavascriptRequirement": {
      "@context": {
        "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib"
      },
      "@id": "cwl:InlineJavascriptRequirement"
    },
    "InplaceUpdateRequirement": {
      "@context": {
        "inplaceUpdate": "cwl:InplaceUpdateRequirement/inplaceUpdate"
      },
      "@id": "cwl:InplaceUpdateRequirement"
    },
    "LoadListingRequirement": "cwl:LoadListingRequirement",
    "MultipleInputFeatureRequirement": "cwl:MultipleInputFeatureRequirement",
    "NetworkAccess": {
      "@context": {
        "networkAccess": "cwl:NetworkAccess/networkAccess"
      },
      "@id": "cwl:NetworkAccess"
    },
    "ResourceRequirement": {
      "@context": {
        "coresMax": "cwl:ResourceRequirement/coresMax",
        "coresMin": "cwl:ResourceRequirement/coresMin",
        "outdirMax": "cwl:ResourceRequirement/outdirMax",
        "outdirMin": "cwl:ResourceRequirement/outdirMin",
        "ramMax": "cwl:ResourceRequirement/ramMax",
        "ramMin": "cwl:ResourceRequirement/ramMin",
        "tmpdirMax": "cwl:ResourceRequirement/tmpdirMax",
        "tmpdirMin": "cwl:ResourceRequirement/tmpdirMin"
      },
      "@id": "cwl:ResourceRequirement"
    },
    "ScatterFeatureRequirement": "cwl:ScatterFeatureRequirement",
    "SchemaDefRequirement": {
      "@context": {
        "types": "cwl:SchemaDefRequirement/types"
      },
      "@id": "cwl:SchemaDefRequirement"
    },
    "ShellCommandRequirement": "cwl:ShellCommandRequirement",
    "SoftwareRequirement": {
      "@context": {
        "package": "cwl:SoftwarePackage/package",
        "version": "cwl:SoftwarePackage/version"
      },
      "@id": "cwl:SoftwareRequirement"
    },
    "StepInputExpressionRequirement": "cwl:StepInputExpressionRequirement",
    "SubworkflowFeatureRequirement": "cwl:SubworkflowFeatureRequirement",
    "ToolTimeLimit": {
      "@context": {
        "timelimit": "cwl:ToolTimeLimit/timelimit"
      },
      "@id": "cwl:ToolTimeLimit"
    },
    "WorkReuse": {
      "@context": {
        "enableReuse": "cwl:WorkReuse/enableReuse"
      },
      "@id": "cwl:WorkReuse"
    },
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "loadListing": "cwl:loadListing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirementsMap/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLRequirementsMap`

