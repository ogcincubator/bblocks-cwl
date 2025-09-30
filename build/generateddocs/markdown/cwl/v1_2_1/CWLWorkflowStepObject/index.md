
# CWLWorkflowStepObject (Schema)

`ogc.cwl.v1_2_1.CWLWorkflowStepObject` *v1.2.1*

CWLWorkflowStepObject

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
allOf:
- properties:
    in:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepIn/schema.yaml
    out:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepOut/schema.yaml
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
      - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/IdentifierArray/schema.yaml
      title: Scatter
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
  type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepObject/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepObject/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "linkMerge": "cwl:linkMerge",
    "valueFrom": "cwl:valueFrom",
    "basename": "cwl:basename",
    "nameroot": "cwl:File/nameroot",
    "version": "cwl:SoftwarePackage/version",
    "label": "http://www.w3.org/2000/01/rdf-schema#label",
    "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
    "position": "cwl:CommandLineBinding/position",
    "prefix": "cwl:CommandLineBinding/prefix",
    "shellQuote": "cwl:CommandLineBinding/shellQuote",
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
    "outputBinding": {
      "@context": {
        "glob": "cwl:CommandOutputBinding/glob"
      },
      "@id": "cwl:outputBinding"
    },
    "stderr": "cwl:stderr",
    "stdin": "cwl:stdin",
    "stdout": "cwl:stdout",
    "when": "cwl:when",
    "loadContents": "cwl:loadContents",
    "streamable": "cwl:FieldBase/streamable",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLWorkflowStepObject/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLWorkflowStepObject`

