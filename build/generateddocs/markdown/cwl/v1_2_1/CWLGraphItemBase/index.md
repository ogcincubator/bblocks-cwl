
# CWLGraphItemBase (Schema)

`ogc.cwl.v1_2_1.CWLGraphItemBase` *v1.2.1*

CWLGraphItemBase

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
additionalProperties: {}
properties:
  arguments:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/schema.yaml
  baseCommand:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.yaml
  class:
    description: CWL class specification. This is used to differentiate between single
      Application Package (AP)definitions and Workflow that chains multiple packages.
    enum:
    - CommandLineTool
    - ExpressionTool
    - Workflow
    title: Class
    type: string
  hints:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLHints/schema.yaml
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
  inputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.yaml
  intent:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIntent/schema.yaml
  outputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.yaml
  requirements:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLRequirements/schema.yaml
  scatter:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatter/schema.yaml
  scatterMethod:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatterMethod/schema.yaml
required:
- class
- id
- inputs
- outputs
title: CWLGraphItem
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItemBase/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItemBase/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
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
    "inputBinding": "cwl:inputBinding",
    "basename": "cwl:basename",
    "nameroot": "cwl:File/nameroot",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "outputBinding": "cwl:outputBinding",
    "glob": "cwl:CommandOutputBinding/glob",
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItemBase/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLGraphItemBase`

