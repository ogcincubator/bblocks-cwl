
# CWL (Schema)

`ogc.cwl.v1_2_1.CWL` *v1.2.1*

The root of the register: a Common Workflow Language v1.2.1 Application Package document.

A CWL document is one of three top-level forms: a single CommandLineTool/ExpressionTool/Workflow
definition (`CWLAtomic`), the same wrapped as a nested `run` definition inside a Workflow step
(`CWLAtomicNested`), or a `$graph`-wrapped document (`CWLGraph`).

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Atomic CommandLineTool document
A complete, top-level CWL document describing a single `CommandLineTool` — one of the
three top-level forms a `CWL` document can take
([CWLAtomic](bblocks://ogc.cwl.v1_2_1.CWLAtomic)). Adapted from the CWL v1.2 conformance
test suite.

#### json
```json
{
  "cwlVersion": "v1.2",
  "class": "CommandLineTool",
  "baseCommand": ["cat"],
  "inputs": [
    {
      "id": "file1",
      "type": "File"
    }
  ],
  "outputs": [
    {
      "id": "output",
      "type": "File",
      "outputBinding": { "glob": "output" }
    }
  ],
  "stdin": "$(inputs.file1.path)",
  "stdout": "output"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWL/context.jsonld",
  "cwlVersion": "v1.2",
  "class": "CommandLineTool",
  "baseCommand": [
    "cat"
  ],
  "inputs": [
    {
      "id": "file1",
      "type": "File"
    }
  ],
  "outputs": [
    {
      "id": "output",
      "type": "File",
      "outputBinding": {
        "glob": "output"
      }
    }
  ],
  "stdin": "$(inputs.file1.path)",
  "stdout": "output"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix sld: <https://w3id.org/cwl/salad#> .

<https://example.org/file1> sld:type cwl:File .

<https://example.org/output> cwl:outputBinding [ ns1:glob "output" ] ;
    sld:type cwl:File .

[] a cwl:CommandLineTool ;
    cwl:baseCommand ( "cat" ) ;
    cwl:inputs <https://example.org/file1> ;
    cwl:outputs <https://example.org/output> ;
    cwl:stdin "$(inputs.file1.path)" ;
    cwl:stdout "output" .


```


### Workflow document with an embedded step
A top-level `Workflow` document ([CWLWorkflow](bblocks://ogc.cwl.v1_2_1.CWLWorkflow)) with
a single step whose `run` value is a `CommandLineTool` inlined directly in place
([CWLAtomicNested](bblocks://ogc.cwl.v1_2_1.CWLAtomicNested)), rather than referenced by
file or URL.

#### json
```json
{
  "cwlVersion": "v1.2",
  "class": "Workflow",
  "label": "Count lines in a file",
  "inputs": [
    {
      "id": "input_file",
      "type": "File"
    }
  ],
  "outputs": [
    {
      "id": "count_output",
      "type": "File",
      "outputSource": "count_lines/output"
    }
  ],
  "steps": {
    "count_lines": {
      "in": {
        "file1": "input_file"
      },
      "out": ["output"],
      "run": {
        "class": "CommandLineTool",
        "baseCommand": ["wc", "-l"],
        "inputs": [
          {
            "id": "file1",
            "type": "File",
            "inputBinding": { "position": 1 }
          }
        ],
        "outputs": [
          {
            "id": "output",
            "type": "File",
            "outputBinding": { "glob": "output.txt" }
          }
        ],
        "stdout": "output.txt"
      }
    }
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWL/context.jsonld",
  "cwlVersion": "v1.2",
  "class": "Workflow",
  "label": "Count lines in a file",
  "inputs": [
    {
      "id": "input_file",
      "type": "File"
    }
  ],
  "outputs": [
    {
      "id": "count_output",
      "type": "File",
      "outputSource": "count_lines/output"
    }
  ],
  "steps": {
    "count_lines": {
      "in": {
        "file1": "input_file"
      },
      "out": [
        "output"
      ],
      "run": {
        "class": "CommandLineTool",
        "baseCommand": [
          "wc",
          "-l"
        ],
        "inputs": [
          {
            "id": "file1",
            "type": "File",
            "inputBinding": {
              "position": 1
            }
          }
        ],
        "outputs": [
          {
            "id": "output",
            "type": "File",
            "outputBinding": {
              "glob": "output.txt"
            }
          }
        ],
        "stdout": "output.txt"
      }
    }
  }
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#Workflow/> .
@prefix ns2: <https://w3id.org/cwl/cwl#CommandOutputBinding/> .
@prefix ns3: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix sld: <https://w3id.org/cwl/salad#> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

<https://example.org/count_lines> cwl:in "input_file" ;
    cwl:out <https://example.org/output> ;
    cwl:run [ a cwl:CommandLineTool ;
            cwl:baseCommand ( "wc" "-l" ) ;
            cwl:inputs <https://example.org/file1> ;
            cwl:outputs <https://example.org/output> ;
            cwl:stdout "output.txt" ] .

<https://example.org/count_output> sld:type cwl:File .

<https://example.org/file1> cwl:inputBinding [ ns3:position 1 ] ;
    sld:type cwl:File .

<https://example.org/input_file> sld:type cwl:File .

<https://example.org/output> cwl:outputBinding [ ns2:glob "output.txt" ] ;
    sld:type cwl:File .

[] a cwl:Workflow ;
    rdfs:label "Count lines in a file" ;
    ns1:steps <https://example.org/count_lines> ;
    cwl:inputs <https://example.org/input_file> ;
    cwl:outputs <https://example.org/count_output> .


```

## Schema

```yaml
oneOf:
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLAtomic/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLGraph/schema.yaml
- $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflow/schema.yaml

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWL/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWL/schema.yaml)


# JSON-LD Context

```jsonld
{
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
    "class": "@type",
    "CommandLineTool": "cwl:CommandLineTool",
    "ExpressionTool": "cwl:ExpressionTool",
    "Workflow": "cwl:Workflow",
    "$graph": "@graph",
    "steps": {
      "@context": {
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
          "@id": "cwl:run",
          "@type": "@id"
        },
        "when": "cwl:when"
      },
      "@id": "cwl:Workflow/steps",
      "@container": "@id"
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
    "s": "https://schema.org/",
    "cwl": "https://w3id.org/cwl/cwl#",
    "cwltool": "http://commonwl.org/cwltool#",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "dct": "http://purl.org/dc/terms/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWL/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWL`

