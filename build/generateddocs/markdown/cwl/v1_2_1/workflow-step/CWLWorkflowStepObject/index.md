
# CWLWorkflowStepObject (Schema)

`ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepObject` *v1.2.1*

The executable shape of a single Workflow step: how its
underlying process is invoked (`run`), how workflow parameters are wired to and from it (`in`,
`out`), an optional guard condition (`when`), and scatter/gather behavior (`scatter`,
`scatterMethod`) for fanning the step out over array inputs. Used directly as the value type when
`steps` is given as a map keyed by step id; see `CWLWorkflowStepItem` for the list form, where the
id is an explicit field instead.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

## Scatter/gather

To use scatter/gather, `ScatterFeatureRequirement` must be listed among the workflow's or workflow
step's [requirements](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsItem).

A scatter operation specifies that the step (or subworkflow) should execute separately over a list
of input elements. Each job making up a scatter operation is independent and may be executed
concurrently. `scatter` names one or more of the step's [`in`](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepIn)
parameters to scatter over; an input parameter may be listed more than once, in which case it
becomes a nested array. The declared type of each scattered input parameter implicitly becomes an
array of items of that type, so upstream parameters connected to it must themselves be arrays. All
[`out`](bblocks://ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepOut) parameter types are likewise implicitly wrapped
in arrays, with each scatter job contributing one entry. If a scattered parameter's runtime value is
an empty array, all outputs are set to empty arrays and no work is done for the step.

When `scatter` names more than one input parameter, `scatterMethod` says how to decompose the inputs
into a discrete set of jobs:

- **dotproduct** — the input arrays are aligned and one element is taken from each to construct each
  job. It is an error if the input arrays are not all the same length.
- **nested_crossproduct** — the Cartesian product of the inputs, producing a job for every
  combination of the scattered inputs. Output arrays are nested, one level per scattered input, in
  the order the inputs are listed in `scatter`.
- **flat_crossproduct** — the same Cartesian product as `nested_crossproduct`, but the output arrays
  are flattened to a single level, still listed in the order the inputs appear in `scatter`.

## Conditional execution

`when` makes execution of the step conditional on an [expression](bblocks://ogc.cwl.v1_2_1.CWLExpression)
that is evaluated with `inputs` bound to the step's input object (or, for a scattered step, to each
individual scatter job's input object) and must return a boolean value; it is an error for the
expression to return anything else. A step whose condition evaluates to `false` is *skipped* and
produces `null` for all of its output parameters. Because the condition is evaluated per scatter job,
some jobs in a scatter may run while others are skipped; when the results are gathered, skipped jobs
appear as `null` entries in the output arrays.

Conditionals are an optional CWL feature: an implementation that does not support them must return a
fatal error when asked to execute a workflow that relies on conditional constructs it does not
implement.

## Subworkflows

To nest a workflow as the `run` value of a step, `SubworkflowFeatureRequirement` must be listed among
the workflow's or workflow step's requirements. It is a fatal error for a workflow to directly or
indirectly invoke itself as a subworkflow.

## Examples

### Step referencing an external tool
A workflow step that runs an external `CommandLineTool` document (`run` given as a relative
file reference), wiring one workflow-level input to its `file1` input and exposing its
`output` parameter.

#### json
```json
{
  "in": {
    "file1": "file1"
  },
  "out": [
    "output"
  ],
  "run": "wc-tool.cwl"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/context.jsonld",
  "in": {
    "file1": "file1"
  },
  "out": [
    "output"
  ],
  "run": "wc-tool.cwl"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] cwl:in "file1" ;
    cwl:out <https://example.org/output> ;
    cwl:run <https://example.org/wc-tool.cwl> .


```


### Scattered step with dotproduct method
A step that scatters over two input parameters using the `dotproduct` method, pairing up
elements of `inp1` and `inp2` one job at a time, and running a nested tool referenced by a
document-fragment identifier.

#### json
```json
{
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
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/context.jsonld",
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

[] cwl:in "inp1",
        "inp2" ;
    cwl:out <https://example.org/echo_out> ;
    cwl:run <https://example.org/#echo> ;
    cwl:scatter ( <https://example.org/echo_in1> <https://example.org/echo_in2> ) ;
    cwl:scatterMethod <https://example.org/dotproduct> .


```

## Schema

```yaml
allOf:
- properties:
    in:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepIn/schema.yaml
      x-jsonld-id: https://w3id.org/cwl/cwl#in
      x-jsonld-container: '@id'
    out:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepOut/schema.yaml
      x-jsonld-id: https://w3id.org/cwl/cwl#out
      x-jsonld-type: '@id'
    run:
      description: Nested CWL definition to run as Workflow step.
      oneOf:
      - description: File or URL reference to a CWL tool definition.
        type: string
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLAtomicNested/schema.yaml
        description: Nested CWL tool definition for the step.
      - $comment: Same as 'CWLWorkflow', but 'cwlVersion' not repeated (only at root).
        allOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/schema.yaml
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDocumentation/schema.yaml
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowClass/schema.yaml
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowBase/schema.yaml
        description: Nested CWL Workflow definition for the step.
      x-jsonld-id: https://w3id.org/cwl/cwl#run
      x-jsonld-type: '@id'
    when:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      description: Condition to execute a step that must evaluate to a boolean-like
        value.
      x-jsonld-id: https://w3id.org/cwl/cwl#when
  required:
  - in
  - run
  - out
  type: object
- properties:
    scatter:
      description: 'The scatter field specifies one or more input parameters which
        will be scattered.


        An input parameter may be listed more than once. The declared type of each

        input parameter implicitly becomes an array of items of the input parameter
        type.

        If a parameter is listed more than once, it becomes a nested array. As a result,

        upstream parameters which are connected to scattered parameters must be arrays.


        All output parameter types are also implicitly wrapped in arrays. Each job

        in the scatter results in an entry in the output array.


        If any scattered parameter runtime value is an empty array, all outputs are

        set to empty arrays and no work is done for the step, according to applicable
        scattering rules.

        '
      oneOf:
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/IdentifierArray/schema.yaml
      title: Scatter
      x-jsonld-id: https://w3id.org/cwl/cwl#scatter
      x-jsonld-type: '@id'
      x-jsonld-container: '@list'
    scatterMethod:
      additionalProperties: false
      default: dotproduct
      description: "If 'scatter' declares more than one input parameter, 'scatterMethod'\ndescribes
        how to decompose the input into a discrete set of jobs.\n\n- dotproduct: specifies
        that each of the input arrays are aligned and\n  one element taken from each
        array to construct each job. It is an\n  error if all input arrays are not
        the same length.\n\n- nested_crossproduct: specifies the Cartesian product
        of the inputs, producing \n  a job for every combination of the scattered
        inputs. The output must be nested \n  arrays for each level of scattering,
        in the order that the input arrays\n  are listed in the 'scatter' field.\n\n-
        flat_crossproduct: specifies the Cartesian product of the inputs, producing
        a \n  job for every combination of the scattered inputs. The output arrays
        must be \n  flattened to a single level, but otherwise listed in the order
        that the input \n  arrays are listed in the 'scatter' field.\n"
      enum:
      - dotproduct
      - nested_crossproduct
      - flat_crossproduct
      required:
      - timelimit
      - class
      title: scatterMethod
      type: string
      x-jsonld-id: https://w3id.org/cwl/cwl#scatterMethod
      x-jsonld-type: '@vocab'
  type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/schema.yaml)


# JSON-LD Context

```jsonld
{
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
        },
        "id": "@id"
      },
      "@id": "cwl:in",
      "@container": "@id"
    },
    "out": {
      "@context": {
        "id": "@id"
      },
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
    "cwl": "https://w3id.org/cwl/cwl#",
    "sld": "https://w3id.org/cwl/salad#",
    "dct": "http://purl.org/dc/terms/",
    "s": "https://schema.org/",
    "cwltool": "http://commonwl.org/cwltool#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "ogccwl": "https://w3id.org/ogc/cwl/",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/workflow-step/CWLWorkflowStepObject/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/workflow-step/CWLWorkflowStepObject`

