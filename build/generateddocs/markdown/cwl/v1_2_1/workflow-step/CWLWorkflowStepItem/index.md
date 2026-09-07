
# CWLWorkflowStepItem (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepItem` *v1.2.1*

A single Workflow step given in the list form of `steps`, where the step's `id` is
carried as an explicit field alongside `run`/`in`/`out`/`when`/`scatter` rather than being the map
key; see `CWLWorkflowStepObject` for the shape shared with the map form.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Step in list form
The same kind of scattered step as in [CWLWorkflowStepObject](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepObject),
but written as an entry of a `steps` list, so the step's `id` is carried as an explicit field
rather than being the map key.

#### json
```json
{
  "id": "step1",
  "in": {
    "echo_in1": "inp1",
    "echo_in2": "inp2"
  },
  "out": [
    "echo_out"
  ],
  "scatter": [
    "echo_in1",
    "echo_in2"
  ],
  "scatterMethod": "dotproduct",
  "run": "#echo"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepItem/context.jsonld",
  "id": "step1",
  "in": {
    "echo_in1": "inp1",
    "echo_in2": "inp2"
  },
  "out": [
    "echo_out"
  ],
  "scatter": [
    "echo_in1",
    "echo_in2"
  ],
  "scatterMethod": "dotproduct",
  "run": "#echo"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<https://example.org/step1> cwl:in "inp1",
        "inp2" ;
    cwl:out <https://example.org/echo_out> ;
    cwl:run <https://example.org/#echo> ;
    cwl:scatter ( <https://example.org/echo_in1> <https://example.org/echo_in2> ) ;
    cwl:scatterMethod <https://example.org/dotproduct> .


```

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepId/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepItem/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "id": "@id",
    "in": {
      "@context": {
        "linkMerge": "cwl:linkMerge",
        "source": {
          "@id": "cwl:source",
          "@type": "@id"
        },
        "valueFrom": "cwl:valueFrom",
        "default": {
          "@context": {
            "basename": "cwl:basename",
            "class": "@type",
            "location": "@id",
            "nameroot": "cwl:File/nameroot",
            "path": {
              "@id": "cwl:path",
              "@type": "@id"
            }
          },
          "@id": "sld:default",
          "@container": "@list"
        }
      },
      "@id": "cwl:in",
      "@container": "@id"
    },
    "out": {
      "@id": "cwl:out",
      "@type": "@id"
    },
    "run": {
      "@context": {
        "version": "cwl:SoftwarePackage/version",
        "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
        "label": "http://www.w3.org/2000/01/rdf-schema#label",
        "arguments": {
          "@context": {
            "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
            "position": "cwl:CommandLineBinding/position",
            "prefix": "cwl:CommandLineBinding/prefix",
            "shellQuote": "cwl:CommandLineBinding/shellQuote",
            "valueFrom": "cwl:valueFrom"
          },
          "@id": "cwl:arguments",
          "@container": "@list"
        },
        "baseCommand": {
          "@id": "cwl:baseCommand",
          "@container": "@list"
        },
        "hints": {
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
            "packages": {
              "@context": {
                "package": "cwl:SoftwarePackage/package",
                "specs": {
                  "@id": "cwl:SoftwarePackage/specs",
                  "@type": "@id"
                }
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
            "enableReuse": "cwl:WorkReuse/enableReuse"
          },
          "@id": "cwl:hints",
          "@container": "@type"
        },
        "inputs": {
          "@context": {
            "default": {
              "@context": {
                "basename": "cwl:basename",
                "location": "@id",
                "nameroot": "cwl:File/nameroot",
                "path": {
                  "@id": "cwl:path",
                  "@type": "@id"
                }
              },
              "@id": "sld:default"
            },
            "type": {
              "@id": "sld:type",
              "@type": "@vocab"
            },
            "inputBinding": {
              "@context": {
                "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
                "position": "cwl:CommandLineBinding/position",
                "prefix": "cwl:CommandLineBinding/prefix",
                "shellQuote": "cwl:CommandLineBinding/shellQuote",
                "valueFrom": "cwl:valueFrom"
              },
              "@id": "cwl:inputBinding"
            }
          },
          "@id": "cwl:inputs",
          "@container": "@id"
        },
        "intent": {
          "@id": "cwl:Process/intent",
          "@type": "@id"
        },
        "outputs": {
          "@context": {
            "outputBinding": {
              "@context": {
                "glob": "cwl:CommandOutputBinding/glob"
              },
              "@id": "cwl:outputBinding"
            },
            "type": {
              "@id": "sld:type",
              "@type": "@vocab"
            }
          },
          "@id": "cwl:outputs",
          "@container": "@id"
        },
        "requirements": {
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
            "packages": {
              "@context": {
                "package": "cwl:SoftwarePackage/package",
                "specs": {
                  "@id": "cwl:SoftwarePackage/specs",
                  "@type": "@id"
                }
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
            "enableReuse": "cwl:WorkReuse/enableReuse"
          },
          "@id": "cwl:requirements",
          "@container": "@type"
        },
        "stderr": "cwl:stderr",
        "stdin": "cwl:stdin",
        "stdout": "cwl:stdout",
        "class": "@type",
        "steps": {
          "@id": "cwl:Workflow/steps",
          "@container": "@id"
        }
      },
      "@id": "cwl:run",
      "@type": "@id"
    },
    "when": "cwl:when",
    "scatter": {
      "@id": "cwl:scatter",
      "@type": "@id",
      "@container": "@list"
    },
    "scatterMethod": {
      "@id": "cwl:scatterMethod",
      "@type": "@vocab"
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
    "BuiltinRequirement": "ogccwl:BuiltinRequirement",
    "OGCAPIRequirement": "ogccwl:OGCAPIRequirement",
    "WPS1Requirement": "ogccwl:WPS1Requirement",
    "CommandLineTool": "cwl:CommandLineTool",
    "ExpressionTool": "cwl:ExpressionTool",
    "Workflow": "cwl:Workflow",
    "dct": "http://purl.org/dc/terms/",
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "s": "https://schema.org/",
    "cwltool": "http://commonwl.org/cwltool#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepItem`

