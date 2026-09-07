
# CWLRequirementsItem (Schema)

`ogc.cwl.v1_2_1.requirements.CWLRequirementsItem` *v1.2.1*

A single entry of a process's `requirements` list: any one of
the requirement classes this register models — the standard CWL process requirements
(`DockerRequirement`, `ResourceRequirement`, `InitialWorkDirRequirement`, ...) plus the
`cwltool`-specific `CUDARequirement` extension. Kept as its own reusable, `$ref`-able union so
downstream profiles can narrow the set of accepted requirement classes without depending on
`extensionPoints`.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

For any new items added, ensure they are added under 'class' of 'UnknownRequirement' as well.
Otherwise, insufficiently restrictive classes could cause multiple matches, failing the 'oneOf' condition.

## Examples

### DockerRequirement item
A single `requirements` list entry declaring that the tool must run inside a
specific Docker image.

#### json
```json
{
  "class": "DockerRequirement",
  "dockerPull": "docker.io/debian:stable-slim"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/context.jsonld",
  "class": "DockerRequirement",
  "dockerPull": "docker.io/debian:stable-slim"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] a <https://example.org/DockerRequirement> ;
    ns1:dockerPull "docker.io/debian:stable-slim" .


```


### ResourceRequirement item
A single `requirements` list entry declaring the minimum and maximum number of
CPU cores the tool needs.

#### json
```json
{
  "class": "ResourceRequirement",
  "coresMin": 1.25,
  "coresMax": 1.75
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/context.jsonld",
  "class": "ResourceRequirement",
  "coresMin": 1.25,
  "coresMax": 1.75
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#ResourceRequirement/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/ResourceRequirement> ;
    ns1:coresMax 1.75e+00 ;
    ns1:coresMin 1.25e+00 .


```

## Schema

```yaml
$comment: 'For any new items added, ensure they are added under ''class'' of ''UnknownRequirement''
  as well.

  Otherwise, insufficiently restrictive classes could cause multiple matches, failing
  the ''oneOf'' condition.

  '
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/cwltool-CUDARequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ShellCommandRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SchemaDefRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InlineJavascriptRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InplaceUpdateRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ResourceRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ScatterFeatureRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ToolTimeLimitRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/WorkReuseRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/MultipleInputFeatureRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/StepInputExpressionRequirement/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SubworkflowFeatureRequirement/schema.yaml
title: CWLRequirementsItem

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/schema.yaml)


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
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirementsItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/CWLRequirementsItem`

