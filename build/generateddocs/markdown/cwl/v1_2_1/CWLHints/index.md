
# CWLHints (Schema)

`ogc.cwl.v1_2_1.CWLHints` *v1.2.1*

Non-failing additional hints that can help resolve extra requirements.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: Non-failing additional hints that can help resolve extra requirements.
$defs:
  CWLHintsMap:
    anyOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirementsMap/schema.yaml
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHintsMapExtras/schema.yaml
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
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHintsItem/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLImport/schema.yaml
    title: CWLHintsList
    type: array
oneOf:
- $ref: '#/$defs/CWLHintsMap'
- $ref: '#/$defs/CWLHintsList'
title: CWLHints

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/schema.yaml)


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
    "dockerFile": "cwl:DockerRequirement/dockerFile",
    "dockerImageId": "cwl:DockerRequirement/dockerImageId",
    "dockerImport": "cwl:DockerRequirement/dockerImport",
    "dockerLoad": "cwl:DockerRequirement/dockerLoad",
    "dockerOutputDirectory": "cwl:DockerRequirement/dockerOutputDirectory",
    "dockerPull": "cwl:DockerRequirement/dockerPull",
    "package": "cwl:SoftwarePackage/package",
    "version": "cwl:SoftwarePackage/version",
    "envName": "cwl:EnvironmentDef/envName",
    "envValue": "cwl:EnvironmentDef/envValue",
    "types": "cwl:SchemaDefRequirement/types",
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
    "expressionLib": "cwl:InlineJavascriptRequirement/expressionLib",
    "inplaceUpdate": "cwl:InplaceUpdateRequirement/inplaceUpdate",
    "loadListing": "cwl:loadListing",
    "networkAccess": "cwl:NetworkAccess/networkAccess",
    "coresMax": "cwl:ResourceRequirement/coresMax",
    "coresMin": "cwl:ResourceRequirement/coresMin",
    "outdirMax": "cwl:ResourceRequirement/outdirMax",
    "outdirMin": "cwl:ResourceRequirement/outdirMin",
    "ramMax": "cwl:ResourceRequirement/ramMax",
    "ramMin": "cwl:ResourceRequirement/ramMin",
    "tmpdirMax": "cwl:ResourceRequirement/tmpdirMax",
    "tmpdirMin": "cwl:ResourceRequirement/tmpdirMin",
    "timelimit": "cwl:ToolTimeLimit/timelimit",
    "enableReuse": "cwl:WorkReuse/enableReuse",
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLHints`

