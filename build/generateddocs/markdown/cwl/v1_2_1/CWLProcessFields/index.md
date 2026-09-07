
# CWLProcessFields (Schema)

`ogc.cwl.v1_2_1.CWLProcessFields` *v1.2.1*

The process-definition fields (`inputs`, `outputs`, `requirements`, `hints`,
`baseCommand`, `arguments`, `stdin`/`stdout`/`stderr`, `scatter`, `scatterMethod`, `intent`, `id`)
shared by every packaging shape a CWL CommandLineTool/ExpressionTool/Workflow can take, excluding
`class` itself since the legal `class` values differ by packaging. Not typically profiled on its
own.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The process-definition fields common to every packaging shape a CWL CommandLineTool, ExpressionTool,
or Workflow can take: at the document root
([CWLAtomicBase](bblocks://ogc.cwl.v1_2_1.CWLAtomicBase)), embedded inline as a step's `run` value, or
as an entry of a `$graph` array ([CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)).

This block deliberately excludes `class` — the property that discriminates which kind of process a
document describes — because which `class` values are legal differs by packaging: a `$graph` entry
may declare `class: Workflow` alongside `CommandLineTool`/`ExpressionTool`, while a standalone atomic
document only allows the latter two. Each consumer of this block layers its own `class` property (with
its own enum) and its own `required` list on top via `allOf`, rather than this block hard-coding one
set of allowed values that every consumer would then be stuck with.

Factoring these fields out here, instead of each consumer repeating the same property list, keeps the
two shapes from drifting out of sync with each other as the schema evolves.

## Examples

### Fields of a command-line process
The shared fields as they appear on a `CommandLineTool`-shaped process, regardless of whether
it ends up validated as a root document, a nested step `run`, or a `$graph` entry — `class` is
added separately by whichever of those wraps this block.

#### json
```json
{
  "baseCommand": ["echo", "first"],
  "arguments": ["-n", "foo"],
  "inputs": {
    "in": {
      "type": "Any"
    }
  },
  "outputs": {
    "out": {
      "type": "string",
      "outputBinding": {
        "glob": "out.txt",
        "loadContents": true,
        "outputEval": "$(self[0].contents)"
      }
    }
  },
  "stdout": "out.txt"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/context.jsonld",
  "baseCommand": [
    "echo",
    "first"
  ],
  "arguments": [
    "-n",
    "foo"
  ],
  "inputs": {
    "in": {
      "type": "Any"
    }
  },
  "outputs": {
    "out": {
      "type": "string",
      "outputBinding": {
        "glob": "out.txt",
        "loadContents": true,
        "outputEval": "$(self[0].contents)"
      }
    }
  },
  "stdout": "out.txt"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/in> sld:type <https://example.org/Any> .

<https://example.org/out> cwl:outputBinding [ ns1:glob "out.txt" ] ;
    sld:type xsd:string .

[] cwl:arguments ( "-n" "foo" ) ;
    cwl:baseCommand ( "echo" "first" ) ;
    cwl:inputs <https://example.org/in> ;
    cwl:outputs <https://example.org/out> ;
    cwl:stdout "out.txt" .


```


### Fields of a $graph-only process, referenced by id
A minimal fragment showing the fields that matter most for a process meant to be referenced by
`id` from elsewhere in the same document (e.g. a `Workflow` step's `run: "#tool-id"`), such as
inside a [CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem).

#### json
```json
{
  "id": "tool-id",
  "inputs": {
    "in": {
      "type": "string"
    }
  },
  "outputs": {
    "out": {
      "type": "string"
    }
  },
  "hints": {
    "DockerRequirement": {
      "dockerPull": "python:3.11-slim"
    }
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/context.jsonld",
  "id": "tool-id",
  "inputs": {
    "in": {
      "type": "string"
    }
  },
  "outputs": {
    "out": {
      "type": "string"
    }
  },
  "hints": {
    "DockerRequirement": {
      "dockerPull": "python:3.11-slim"
    }
  }
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/tool-id> cwl:hints [ a cwl:DockerRequirement ;
            ns1:dockerPull "python:3.11-slim" ] ;
    cwl:inputs <https://example.org/in> ;
    cwl:outputs <https://example.org/out> .

<https://example.org/in> sld:type xsd:string .

<https://example.org/out> sld:type xsd:string .


```

## Schema

```yaml
description: "The process-definition fields shared by every shape a CWL CommandLineTool/ExpressionTool/Workflow\ndocument
  can take, regardless of how the document is packaged (directly at the root, embedded
  as a\nstep's inline `run`, or as an entry of a `$graph` array) \u2014 everything
  except `class` itself, since\nwhich `class` values are legal differs by packaging
  (a `$graph` entry additionally allows\n`Workflow`, which a standalone atomic document
  does not).\n"
properties:
  arguments:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#arguments
    x-jsonld-container: '@list'
  baseCommand:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#baseCommand
    x-jsonld-container: '@list'
  hints:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLHints/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#hints
    x-jsonld-container: '@type'
  id:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIdentifier/schema.yaml
    x-jsonld-id: '@id'
  inputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputsDefinition/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#inputs
    x-jsonld-container: '@id'
  intent:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLIntent/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#Process/intent
    x-jsonld-type: '@id'
  outputs:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputsDefinition/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#outputs
    x-jsonld-container: '@id'
  requirements:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/CWLRequirements/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#requirements
    x-jsonld-container: '@type'
  scatter:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatter/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#scatter
    x-jsonld-type: '@id'
    x-jsonld-container: '@list'
  scatterMethod:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLScatterMethod/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#scatterMethod
    x-jsonld-type: '@vocab'
  stderr:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: 'Destination of the error stream.

      Typically, an expression referring to a desired file name or provided by a CWL
      input reference.

      '
    x-jsonld-id: https://w3id.org/cwl/cwl#stderr
  stdin:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: "Source of the input stream. \nTypically, an expression referring
      to an existing file name or an input of the CWL document.\n"
    x-jsonld-id: https://w3id.org/cwl/cwl#stdin
  stdout:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    description: 'Destination of the output stream.

      Typically, an expression referring to a desired file name or provided by a CWL
      input reference.

      '
    x-jsonld-id: https://w3id.org/cwl/cwl#stdout
required:
- inputs
- outputs
title: CWL process fields
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/schema.yaml)


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
            "class": "@type",
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
        "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
        "label": "http://www.w3.org/2000/01/rdf-schema#label",
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
        },
        "doc": "http://www.w3.org/2000/01/rdf-schema#comment",
        "label": "http://www.w3.org/2000/01/rdf-schema#label"
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
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLProcessFields/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLProcessFields`

