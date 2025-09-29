
# CWLGraphList (Schema)

`ogc.cwl.v1_2_1.CWLGraphList` *v1.2.1*

Graph definition that defines *exactly one* CWL application package represented as list. Multiple definitions simultaneously deployed is NOT supported currently.

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
description: Graph definition that defines *exactly one* CWL application package represented
  as list. Multiple definitions simultaneously deployed is NOT supported currently.
items:
  $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/schema.yaml
maxItems: 1
minItems: 1
title: CWLGraphList
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphList/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphList/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "version": "cwl:SoftwarePackage/version",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
    "position": "cwl:CommandLineBinding/position",
    "prefix": "cwl:CommandLineBinding/prefix",
    "shellQuote": "cwl:CommandLineBinding/shellQuote",
    "valueFrom": "cwl:valueFrom",
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
    "inputBinding": "cwl:inputBinding",
    "loadContents": "cwl:loadContents",
    "pattern": "cwl:SecondaryFileSchema/pattern",
    "required": "cwl:SecondaryFileSchema/required",
    "streamable": "cwl:FieldBase/streamable",
    "basename": "cwl:basename",
    "nameroot": "cwl:File/nameroot",
    "outputBinding": {
      "@context": {
        "glob": "cwl:CommandOutputBinding/glob"
      },
      "@id": "cwl:outputBinding"
    },
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphList/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLGraphList`

