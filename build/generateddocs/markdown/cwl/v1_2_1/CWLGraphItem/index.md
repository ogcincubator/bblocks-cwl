
# CWLGraphItem (Schema)

`ogc.cwl.v1_2_1.CWLGraphItem` *v1.2.1*

A single process or workflow definition entry inside a `$graph`-form
CWL document (see `CWLGraph`): the `class`-discriminated CommandLineTool/ExpressionTool/Workflow
shape (inputs, outputs, requirements, hints, id, ...), combined with the shared metadata and
documentation fields.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

A single process object inside a [`$graph`](bblocks://ogc.cwl.v1_2_1.CWLGraph) array. Per the CWL
specification, every process object listed in a `$graph` document **must** carry an `id` — unlike a
process object embedded directly in a `Workflow` step's `run` field, or the single process object at
the root of a non-graph document (see [CWLAtomicBase](bblocks://ogc.cwl.v1_2_1.CWLAtomicBase)), where
`id` is optional. This `id` is what lets a `Workflow` step's `run` field, or a document reference's
fragment identifier, pick out this specific process object from among the others in the same `$graph`.

Otherwise the shape is the same [shared process fields](bblocks://ogc.cwl.v1_2_1.CWLProcessFields) used
by every packaging of a `class`-discriminated CommandLineTool/ExpressionTool/Workflow process object,
combined here with an extended `class` enum that allows `Workflow` (in addition to
`CommandLineTool`/`ExpressionTool`) since a `$graph` document commonly packages a workflow together with
the processes its steps reference.

## Examples

### CommandLineTool graph item
A `CommandLineTool` process object as it appears inside a `$graph` array — note the required
`id`, which lets other process objects in the same document reference it (e.g. from a
`Workflow` step's `run` field).

#### json
```json
{
  "id": "echo",
  "class": "CommandLineTool",
  "inputs": {
    "echo_in1": {
      "type": "string",
      "inputBinding": {}
    },
    "echo_in2": {
      "type": "string",
      "inputBinding": {}
    }
  },
  "outputs": {
    "echo_out": {
      "type": "string",
      "outputBinding": {
        "glob": "step1_out",
        "loadContents": true,
        "outputEval": "$(self[0].contents)"
      }
    }
  },
  "baseCommand": "echo",
  "arguments": ["-n", "foo"],
  "stdout": "step1_out"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/context.jsonld",
  "id": "echo",
  "class": "CommandLineTool",
  "inputs": {
    "echo_in1": {
      "type": "string",
      "inputBinding": {}
    },
    "echo_in2": {
      "type": "string",
      "inputBinding": {}
    }
  },
  "outputs": {
    "echo_out": {
      "type": "string",
      "outputBinding": {
        "glob": "step1_out",
        "loadContents": true,
        "outputEval": "$(self[0].contents)"
      }
    }
  },
  "baseCommand": "echo",
  "arguments": [
    "-n",
    "foo"
  ],
  "stdout": "step1_out"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/echo> a cwl:CommandLineTool ;
    cwl:arguments ( "-n" "foo" ) ;
    cwl:baseCommand ( "echo" ) ;
    cwl:inputs <https://example.org/echo_in1>,
        <https://example.org/echo_in2> ;
    cwl:outputs <https://example.org/echo_out> ;
    cwl:stdout "step1_out" .

<https://example.org/echo_in1> cwl:inputBinding [ ] ;
    sld:type xsd:string .

<https://example.org/echo_in2> cwl:inputBinding [ ] ;
    sld:type xsd:string .

<https://example.org/echo_out> cwl:outputBinding [ ns1:glob "step1_out" ] ;
    sld:type xsd:string .


```


### Workflow graph item referencing another graph item
A `Workflow` process object inside the same `$graph` array as the `echo` `CommandLineTool`
above, with a step that runs it by reference (`run: "#echo"`) and an output sourced from that
step.

#### json
```json
{
  "id": "main",
  "class": "Workflow",
  "inputs": {
    "inp1": "string[]",
    "inp2": "string[]"
  },
  "steps": {
    "step1": {
      "in": {
        "echo_in1": "inp1",
        "echo_in2": "inp2"
      },
      "out": ["echo_out"],
      "run": "#echo"
    }
  },
  "outputs": [
    {
      "id": "out",
      "outputSource": "step1/echo_out",
      "type": {
        "type": "array",
        "items": "string"
      }
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/context.jsonld",
  "id": "main",
  "class": "Workflow",
  "inputs": {
    "inp1": "string[]",
    "inp2": "string[]"
  },
  "steps": {
    "step1": {
      "in": {
        "echo_in1": "inp1",
        "echo_in2": "inp2"
      },
      "out": [
        "echo_out"
      ],
      "run": "#echo"
    }
  },
  "outputs": [
    {
      "id": "out",
      "outputSource": "step1/echo_out",
      "type": {
        "type": "array",
        "items": "string"
      }
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/main> a cwl:Workflow ;
    cwl:inputs "string[]" ;
    cwl:outputs <https://example.org/out> .

<https://example.org/out> sld:type [ sld:type <https://example.org/array> ] .


```

## Schema

```yaml
allOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml
- properties:
    class:
      description: CWL class specification. This is used to differentiate between
        single Application Package (AP)definitions and Workflow that chains multiple
        packages.
      enum:
      - CommandLineTool
      - ExpressionTool
      - Workflow
      title: Class
      type: string
      x-jsonld-id: '@type'
  required:
  - class
  - id
  type: object
additionalProperties: {}
title: CWLGraphItem
x-jsonld-extra-terms:
  CommandLineTool: https://w3id.org/cwl/cwl#CommandLineTool
  ExpressionTool: https://w3id.org/cwl/cwl#ExpressionTool
  Workflow: https://w3id.org/cwl/cwl#Workflow
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
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
    "id": "@id",
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
    "scatter": {
      "@id": "cwl:scatter",
      "@type": "@id",
      "@container": "@list"
    },
    "scatterMethod": {
      "@id": "cwl:scatterMethod",
      "@type": "@vocab"
    },
    "stderr": "cwl:stderr",
    "stdin": "cwl:stdin",
    "stdout": "cwl:stdout",
    "version": "cwl:SoftwarePackage/version",
    "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "class": "@type",
    "CommandLineTool": "cwl:CommandLineTool",
    "ExpressionTool": "cwl:ExpressionTool",
    "Workflow": "cwl:Workflow",
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
    "cwl": "https://w3id.org/cwl/cwl#",
    "cwltool": "http://commonwl.org/cwltool#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "s": "https://schema.org/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraphItem/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLGraphItem`

