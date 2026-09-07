# Common Workflow Language building blocks

Common Workflow Language (CWL) is an open standard for describing how to run command line tools and connect them to create workflows.


Tools and workflows described using CWL are portable across a variety of platforms that support the CWL standards. 
Using CWL, it is easy to scale complex data analysis and machine learning workflows from a single
developer's laptop up to massively parallel cluster, cloud and high performance computing environments.

More information at [the Common Workflow Language website](https://www.commonwl.org/).


## Building Blocks

### `ogc.cwl.v1_2_1.CWLVersion` — CWLVersion

**Type:** schema

The `cwlVersion` field: declares which published version of the CWL
standard a document conforms to. Required once at the root of every CWL document.

### `ogc.cwl.v1_2_1.CWLDocumentation` — CWLDocumentation

**Type:** schema

Shared human-readable documentation fields: a short `label` and a
longer free-text or multi-line `doc` description.

### `ogc.cwl.v1_2_1.CWLOntology` — CWL Ontology

**Type:** model

The RDFS vocabulary/ontology for the Common Workflow Language (CWL) v1.2, published by the CWL
project at `https://w3id.org/cwl/cwl#` (`cwl:`). It defines an `rdfs:Class` for every CWL document
type (`Workflow`, `CommandLineTool`, `DockerRequirement`, ...) and their `rdfs:subClassOf` relations,
and is the vocabulary the rest of this register's blocks bind their properties to via `context.jsonld`.

### `ogc.cwl.v1_2_1.CWLCommand` — CWLCommand

**Type:** schema

Command called in the docker image or on shell according to requirements
and hints specifications. Can be omitted if already defined in the docker
image.


### `ogc.cwl.v1_2_1.SchemaSaladOntology` — Schema Salad Ontology

**Type:** model

The RDFS vocabulary/ontology for Schema Salad, the schema language CWL is defined in, published
alongside CWL v1.2 at `https://w3id.org/cwl/salad#` (`sld:`). It defines the metaschema classes used
to describe CWL's own record/enum/array schemas (`RecordSchema`, `EnumSchema`, `JsonldPredicate`, ...),
distinct from the CWL document vocabulary itself (see [CWL Ontology](bblocks://ogc.cwl.v1_2_1.CWLOntology)).

### `ogc.cwl.v1_2_1.type-system.CWLTypeSymbolValues` — CWLTypeSymbolValues

**Type:** schema

A single allowed value of an `enum` type's
`symbols` list: a string or number literal.

### `ogc.cwl.v1_2_1.LoadListingEnum` — LoadListingEnum

**Type:** schema

The allowed values for `loadListing`, controlling how deeply a
Directory's contents are enumerated for use in expressions: `no_listing` (don't load it),
`shallow_listing` (top level only), or `deep_listing` (recurse into subdirectories).

### `ogc.cwl.v1_2_1.CWLExpression` — CWLExpression

**Type:** schema

When combined with 'InlineJavascriptRequirement', this field allows runtime parameter references
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#Expression).


### `ogc.cwl.v1_2_1.CWLTextPatternID` — CWLTextPatternID

**Type:** schema

Generic identifier name pattern.

### `ogc.cwl.v1_2_1.CWLImport` — CWLImport

**Type:** schema

Represents an '$import' directive that should point toward another compatible CWL file to import where specified.
The contents of the imported file should be relevant contextually where it is being imported.


### `ogc.cwl.v1_2_1.CWLInputStdIn` — CWLInputStdIn

**Type:** schema

Redirects the value of a CWL input to the command's standard input stream (the 'stdin' shorthand or its equivalent 'type: stdin' object form).

### `ogc.cwl.v1_2_1.CWLIntent` — CWLIntent

**Type:** schema

An identifier for the type of computational operation a process
performs, especially useful for `Operation` but also usable on `CommandLineTool`, `Workflow`, or
`ExpressionTool`. If provided, must be an IRI of a concept node representing the operation type,
preferably defined within an ontology — for example an EDAM Ontology operation concept such as
`http://edamontology.org/operation_2928` (Alignment).

### `ogc.cwl.v1_2_1.CWLOutputStdErr` — CWLOutputStdErr

**Type:** schema

Redirects the command's standard error stream to a CWL output (the 'stderr' shorthand or its equivalent 'type: stderr' object form).

### `ogc.cwl.v1_2_1.CWLOutputStdOut` — CWLOutputStdOut

**Type:** schema

Redirects the command's standard output stream to a CWL output (the 'stdout' shorthand or its equivalent 'type: stdout' object form).

### `ogc.cwl.v1_2_1.CWLScatterMethod` — CWLScatterMethod

**Type:** schema

Describes how to decompose the scattered input into a discrete
set of jobs. When 'dotproduct', specifies that each of the input arrays
are aligned and one element taken from each array to construct each job.
It is an error if all input arrays are of different length. When 'nested_crossproduct',
specifies the Cartesian product of the inputs, producing a job for every
combination of the scattered inputs. The output must be nested arrays
for each level of scattering, in the order that the input arrays are listed
in the scatter field. When 'flat_crossproduct', specifies the Cartesian
product of the inputs, producing a job for every combination of the scattered
inputs. The output arrays must be flattened to a single level, but otherwise
listed in the order that the input arrays are listed in the scatter field.


### `ogc.cwl.v1_2_1.Checksum` — Checksum

**Type:** schema

An optional hash code for validating file integrity. Currently must be in
the form `sha1$<hexadecimal string>`, using the SHA-1 algorithm.

### `ogc.cwl.v1_2_1.LinkMergeMethod` — LinkMergeMethod

**Type:** schema

How multiple inbound data links into the same Workflow step input
are combined: `merge_nested` (default; wraps each source's value, producing a list with one entry
per link) or `merge_flattened` (concatenates/appends array-valued sources into a single flat list).

### `ogc.cwl.v1_2_1.ResourceQuantityOrFractional` — ResourceQuantityOrFractional

**Type:** schema

An item quantity that can also represent a proportion of use by resources.

### `ogc.cwl.v1_2_1.requirements.UnknownRequirement` — UnknownRequirement

**Type:** schema

Generic schema to allow alternative CWL requirements/hints not explicitly defined in schemas.

### `ogc.cwl.v1_2_1.requirements.cwltool-CUDARequirement` — cwltool:CUDARequirement

**Type:** schema

`cwltool` extension requirement declaring that a process
needs NVIDIA CUDA (GPU hardware acceleration): minimum CUDA SDK version, required compute
capability, and the minimum/maximum number of GPU devices to request.

### `ogc.cwl.v1_2_1.requirements.ShellCommandRequirement` — ShellCommandRequirement

**Type:** schema

Modifies CommandLineTool execution to generate a single
shell command-line string: each item in `arguments` is joined with spaces and shell-quoted, unless
its `CommandLineBinding` sets `shellQuote: false` — in which case it is joined unquoted, allowing
shell metacharacters such as `|` for pipes.

### `ogc.cwl.v1_2_1.requirements.StepInputExpressionRequirement` — StepInputExpressionRequirement

**Type:** schema

Indicates that the 'Workflow' must support the 'valueFrom' field of 'WorkflowStepInput'.

### `ogc.cwl.v1_2_1.requirements.ScatterFeatureRequirement` — ScatterFeatureRequirement

**Type:** schema

A 'scatter' operation specifies that the associated Workflow step should execute separately over a list of
input elements. Each job making up a scatter operation is independent and may be executed concurrently
(see also: https://www.commonwl.org/v1.2/Workflow.html#WorkflowStep).


### `ogc.cwl.v1_2_1.requirements.SubworkflowFeatureRequirement` — SubworkflowFeatureRequirement

**Type:** schema

Indicates that the 'Workflow' must support nested workflows in the 'run' field of 'WorkflowStep'.

### `ogc.cwl.v1_2_1.requirements.MultipleInputFeatureRequirement` — MultipleInputFeatureRequirement

**Type:** schema

Indicates that the 'Workflow' must support multiple inbound data links listed in the 'source'
field of 'WorkflowStepInput'.


### `ogc.cwl.v1_2_1.type-system.CWLTypeRecordRefPattern` — CWLTypeRecordRefPattern

**Type:** schema

The URL/fragment syntax for referencing a named
record type by IRI: an optional URL/local path prefix followed by a `#RecordName` fragment
identifier, resolved per [CWL's identifier resolution rules](https://www.commonwl.org/v1.2/SchemaSalad.html#Identifier_resolution).

### `ogc.cwl.v1_2_1.ReferenceURL` — ReferenceURL

**Type:** schema

A web-resolvable reference URL (http(s) or ftp) pointing to
documentation, a package repository, or similar external resource associated with a requirement or
software package.

### `ogc.cwl.v1_2_1.CWLDefaultLocation` — CWLDefaultLocation

**Type:** schema

The shape of a `default` value for a File- or Directory-typed
input: a literal File or Directory object, identified by a `path` or `location` and optionally
`basename`/`nameroot`, used when no value is provided for the input at execution time.

### `ogc.cwl.v1_2_1.CWLMetadata` — CWLMetadata

**Type:** schema

Shared document-level metadata fields: `s:keywords` (for search and
categorization) and the process/document `version`.

### `ogc.cwl.v1_2_1.CWLWorkflowClass` — CWLWorkflowClass

**Type:** schema

The 'class: Workflow' discriminator, shared by the root Workflow document and its nested-in-step form; not typically profiled on its own.

### `ogc.cwl.v1_2_1.requirements.DockerRequirement` — DockerRequirement

**Type:** schema

Indicates that a CommandLineTool or ExpressionTool should be run
in a Docker or Docker-compatible (e.g. Singularity, udocker) container, and specifies how to fetch
or build the image (`dockerPull`, `dockerImport`, `dockerLoad`, or `dockerFile`). If listed under
`hints`, the platform may run the tool in the container; if listed under `requirements`, it must.
See the [CWL v1.2 CommandLineTool spec — DockerRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#DockerRequirement)
for the full behavior, including bind-mount and entrypoint handling.

### `ogc.cwl.v1_2_1.requirements.InlineJavascriptRequirement` — InlineJavascriptRequirement

**Type:** schema

Indicates that the workflow platform must support inline Javascript expressions.

If this requirement is not present, the workflow platform must not perform expression interpolation
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).


### `ogc.cwl.v1_2_1.requirements.InplaceUpdateRequirement` — InplaceUpdateRequirement

**Type:** schema

If 'inplaceUpdate' is true, then an implementation supporting this feature may permit tools to directly
update files with 'writable: true' in 'InitialWorkDirRequirement'. That is, as an optimization,
files may be destructively modified in place as opposed to copied and updated
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#InplaceUpdateRequirement).


### `ogc.cwl.v1_2_1.CWLTypeDefinition` — CWLTypeDefinition

**Type:** schema

Field type definition.

### `ogc.cwl.v1_2_1.type-system.CWLTypeSymbols` — CWLTypeSymbols

**Type:** schema

The `symbols` list of an `enum` type: the set of allowed
values composing the enum.

### `ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters` — CWLDirectoryOnlyParameters

**Type:** schema

Parameters that only apply to Directory-typed (or
Directory-array-typed) inputs/outputs: `loadListing`, controlling whether/how deeply the directory's
contents are enumerated for use in expressions.

### `ogc.cwl.v1_2_1.requirements.LoadListingRequirement` — LoadListingRequirement

**Type:** schema

Specify the desired behavior for loading the listing field of a 'Directory' object for use by expressions
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#LoadListingRequirement).


### `ogc.cwl.v1_2_1.CWLFileOnlyParameters` — CWLFileOnlyParameters

**Type:** schema

Parameters that only apply to File-typed (or File-array-typed)
inputs/outputs: `format` (the file's content format/media type, as an IRI or CWL expression),
`streamable`, `loadContents` (whether to load the first 64 KiB of file content for use in
expressions), and `secondaryFiles` (associated files expected alongside the primary one).

### `ogc.cwl.v1_2_1.InputBinding` — InputBinding

**Type:** schema

Defines how to specify the input for the command.

### `ogc.cwl.v1_2_1.OutputBinding` — OutputBinding

**Type:** schema

Defines how to retrieve the output result from the command.

### `ogc.cwl.v1_2_1.requirements.EnvVarRequirement` — EnvVarRequirement

**Type:** schema

Defines a list of environment variables to set in the tool's
execution environment.

### `ogc.cwl.v1_2_1.requirements.NetworkAccessRequirement` — NetworkAccessRequirement

**Type:** schema

`cwltool` extension hint/requirement indicating whether a
process needs outgoing network access. If not specified or false, tools must not assume network
access beyond localhost; if true, the tool may make outgoing connections, though implementations may
still apply their own security policies. Does not imply a publicly routable address or inbound
connections.

### `ogc.cwl.v1_2_1.requirements.ToolTimeLimitRequirement` — ToolTimeLimitRequirement

**Type:** schema

Set an upper limit on the execution time of a CommandLineTool.

A CommandLineTool whose execution duration exceeds the time limit may be preemptively
terminated and considered failed. May also be used by batch systems to make scheduling decisions.

The execution duration excludes external operations, such as staging of files,
pulling a docker image etc., and only counts wall-time for the execution of the command line itself.


### `ogc.cwl.v1_2_1.requirements.WorkReuseRequirement` — WorkReuseRequirement

**Type:** schema

For implementations that support reusing output from past work
(on the assumption that same code and same input produce same results),
control whether to enable or disable the reuse behavior for a particular tool
or step (to accommodate situations where that assumption is incorrect).

A reused step is not executed but instead returns the same output as the original execution.

If 'WorkReuse' is not specified, correct tools should assume it is enabled by default.


### `ogc.cwl.v1_2_1.CWLIdentifier` — CWLIdentifier

**Type:** schema

Reference to the process identifier.

### `ogc.cwl.v1_2_1.requirements.BuiltinRequirement` — BuiltinRequirement

**Type:** schema

Hint indicating that the Application Package corresponds to a
builtin process of this instance. (note: can only be an 'hint'
as it is unofficial CWL specification).


### `ogc.cwl.v1_2_1.type-system.IdentifierArray` — IdentifierArray

**Type:** schema

An array of one or more CWL identifiers, used e.g. when
`scatter` lists more than one input parameter to fan a Workflow step out over.

### `ogc.cwl.v1_2_1.requirements.InitialWorkDirRequirement` — InitialWorkDirRequirement

**Type:** schema

Defines a list of files and subdirectories that must be
staged by the workflow platform prior to executing the command line tool, normally within the
designated output directory (though containers may stage them elsewhere).

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputBase` — CWLWorkflowStepInputBase

**Type:** schema

Common workflow step input properties (source, linkMerge, valueFrom), shared by the step input's list and map representations; not typically profiled on its own.

### `ogc.cwl.v1_2_1.requirements.ResourceRequirement` — ResourceRequirement

**Type:** schema

Specify basic hardware resource requirements for a CommandLineTool: minimum/maximum CPU cores, RAM, and output/temporary directory storage.

### `ogc.cwl.v1_2_1.SoftwarePackage` — SoftwarePackage

**Type:** schema

A single software package entry within a `SoftwareRequirement`:
the package name, optionally the compatible version(s), and optionally one or more IRIs identifying
resources for installing or enabling it (e.g. a Debian or Conda package page), which implementations
may resolve to a concrete install action.

### `ogc.cwl.v1_2_1.requirements.OGCAPIRequirement` — OGCAPIRequirement

**Type:** schema

Hint indicating that the Application Package corresponds to an
OGC API - Processes provider that should be remotely executed and monitored
by this instance. (note: can only be an 'hint' as it is unofficial CWL specification).


### `ogc.cwl.v1_2_1.requirements.WPS1Requirement` — WPS1Requirement

**Type:** schema

Hint indicating that the Application Package corresponds to a
WPS-1 provider process that should be remotely executed and monitored by this
instance. (note: can only be an ''hint'' as it is unofficial CWL specification).


### `ogc.cwl.v1_2_1.CWLDefault` — CWLDefault

**Type:** schema

Default value of input if not provided for task execution.

### `ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef` — CWLTypeRecordRef

**Type:** schema

An IRI with minimally a '{Record}' identifier to look for a schema definition locally or remotely.

The identifier resolution is performed accordingly to the specified reference and as described in
https://www.commonwl.org/v1.2/SchemaSalad.html#Identifier_resolution.


### `ogc.cwl.v1_2_1.CWLDefaultTypedConditional` — CWLDefaultTypedConditional

**Type:** schema

Validates that a `default` value, if given alongside a
`type`, actually matches that declared type (e.g. a `default` for `type: boolean` must be a JSON
boolean, one for an `enum` type must be one of its `symbols`, one for `File`/`Directory` must be a
literal file/directory object). Limits itself to data literals and arrays; nested or multi-type
`type` definitions validate against `Any` instead of being over-constrained.

### `ogc.cwl.v1_2_1.type-system.CWLTypeEnum` — CWLTypeEnum

**Type:** schema

An inline CWL `enum` type definition: `type: enum` plus its
allowed `symbols`.

### `ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef` — CWLTypeRecordFieldDef

**Type:** schema

The definition of a single field within an
inline CWL `record` type: its `type` and, for the list form of `fields`, its `name`. Also carries
the file-only and directory-only parameters (`format`, `secondaryFiles`, `loadListing`, ...), since a
record field's type can itself be File- or Directory-typed.

### `ogc.cwl.v1_2_1.CWLArguments` — CWLArguments

**Type:** schema

Base arguments passed to the command.

### `ogc.cwl.v1_2_1.CWLScatter` — CWLScatter

**Type:** schema

One or more input identifier of an application step within a Workflow
were an array-based input to that Workflow should be scattered across multiple
instances of the step application.


### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepId` — CWLWorkflowStepId

**Type:** schema

The `id` field required on a Workflow step when `steps` is given
as a list rather than a map: identifies the step within the workflow.

### `ogc.cwl.v1_2_1.requirements.SoftwareRequirement` — SoftwareRequirement

**Type:** schema

A list of software packages that should be configured in the
process's execution environment.

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInputDefault` — CWLWorkflowStepInputDefault

**Type:** schema

The 'default' property for a workflow step input, shared by the step input's list and map representations; not typically profiled on its own.

### `ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema` — CWLTypeRecordSchema

**Type:** schema

An inline CWL `record` type definition: `type:
record`, an optional `name`, and its `fields`, given either as a map keyed by field name or as a
list of field definitions (each of which must then carry its own `name`).

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepOut` — CWLWorkflowStepOut

**Type:** schema

Mapping of Workflow step inputs to nested CWL tool definitions inputs or outputs.

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepInItem` — CWLWorkflowStepInItem

**Type:** schema

A single entry of a Workflow step's `in` mapping, in its
list form: combines the step-input id, the common wiring fields (`source`, `linkMerge`,
`valueFrom`), and the optional `default` value used when a source produces no data.

### `ogc.cwl.v1_2_1.CWLType` — CWLType

**Type:** schema

The set of types a CWL input or output parameter may declare: the CWL
primitive/File/Directory types, an inline enum, an inline record, a reference to a named type
(record or enum) defined elsewhere, an array of one of these, or an array combining several of
these (a type union).

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepIn` — CWLWorkflowStepIn

**Type:** schema

Mapping of Workflow step inputs to nested CWL tool definitions inputs or outputs.

### `ogc.cwl.v1_2_1.CWLInputItem` — CWLInputItem

**Type:** schema

Input specification. Note that multiple formats are supported and
not all specification variants or parameters are presented here. Please refer
to official CWL documentation for more details (https://www.commonwl.org).


### `ogc.cwl.v1_2_1.CWLInputObject` — CWLInputObject

**Type:** schema

The type/parameter definition of a single CWL input when expressed
as a nested object (as opposed to a bare type shorthand): `type`, an optional `inputBinding`, plus
the shared default-type-consistency and documentation fields.

### `ogc.cwl.v1_2_1.CWLOutputItem` — CWLOutputItem

**Type:** schema

Output specification. Note that multiple formats are supported
and not all specification variants or parameters are presented here. Please
refer to official CWL documentation for more details (https://www.commonwl.org).


### `ogc.cwl.v1_2_1.CWLOutputObject` — CWLOutputObject

**Type:** schema

The type/parameter definition of a single CWL output when
expressed as a nested object (as opposed to a bare type shorthand): `type`, an optional
`outputBinding`, plus the shared documentation fields.

### `ogc.cwl.v1_2_1.type-system.CWLTypeRecordArray` — CWLTypeRecordArray

**Type:** schema

A CWL type definition for an array whose elements
are all of the same, further-specified CWL type: `type: array` plus an `items` type.

### `ogc.cwl.v1_2_1.CWLInputsDefinition` — CWLInputsDefinition

**Type:** schema

All inputs available to the Application Package.

### `ogc.cwl.v1_2_1.CWLOutputsDefinition` — CWLOutputsDefinition

**Type:** schema

All outputs produced by the Application Package.

### `ogc.cwl.v1_2_1.requirements.SchemaDefRequirement` — SchemaDefRequirement

**Type:** schema

An array of named `enum`/`record` type definitions available
for reuse via IRI reference from `inputs`/`outputs` type fields. Definitions are processed in the
order listed, so later definitions may refer to earlier ones.

### `ogc.cwl.v1_2_1.requirements.CWLRequirementsItem` — CWLRequirementsItem

**Type:** schema

A single entry of a process's `requirements` list: any one of
the requirement classes this register models — the standard CWL process requirements
(`DockerRequirement`, `ResourceRequirement`, `InitialWorkDirRequirement`, ...) plus the
`cwltool`-specific `CUDARequirement` extension. Kept as its own reusable, `$ref`-able union so
downstream profiles can narrow the set of accepted requirement classes without depending on
`extensionPoints`.

### `ogc.cwl.v1_2_1.requirements.CWLRequirementsMap` — CWLRequirementsMap

**Type:** schema

Map-form (keyed by requirement class name) of the requirement types accepted by 'requirements'/'hints', shared between CWLRequirements and CWLHints; not typically profiled on its own.

### `ogc.cwl.v1_2_1.requirements.CWLHintsItem` — CWLHintsItem

**Type:** schema

A single entry of a process's `hints` list: any one of the
requirement/hint classes this register models (the standard CWL requirements, plus the
OGC-AP/WPS1/builtin hint classes), or `UnknownRequirement` as a fallback for any other
`class`-discriminated hint not otherwise recognized. Unlike `requirements`, an unsatisfied hint
must not cause a workflow engine to reject the process. Kept as its own reusable, `$ref`-able union
so downstream profiles can narrow the set of accepted hint classes without depending on
`extensionPoints`.

### `ogc.cwl.v1_2_1.requirements.CWLRequirements` — CWLRequirements

**Type:** schema

Explicit requirement to execute the application package.

### `ogc.cwl.v1_2_1.requirements.CWLHints` — CWLHints

**Type:** schema

Non-failing additional hints that can help resolve extra requirements.

### `ogc.cwl.v1_2_1.CWLProcessFields` — CWLProcessFields

**Type:** schema

The process-definition fields (`inputs`, `outputs`, `requirements`, `hints`,
`baseCommand`, `arguments`, `stdin`/`stdout`/`stderr`, `scatter`, `scatterMethod`, `intent`, `id`)
shared by every packaging shape a CWL CommandLineTool/ExpressionTool/Workflow can take, excluding
`class` itself since the legal `class` values differ by packaging. Not typically profiled on its
own.

### `ogc.cwl.v1_2_1.CWLAtomicBase` — CWLAtomicBase

**Type:** schema

Direct CWL definition instead of the graph representation. Shared by the root CommandLineTool/ExpressionTool document and its nested-in-step form; not typically profiled on its own.

### `ogc.cwl.v1_2_1.CWLGraphItem` — CWLGraphItem

**Type:** schema

A single process or workflow definition entry inside a `$graph`-form
CWL document (see `CWLGraph`): the `class`-discriminated CommandLineTool/ExpressionTool/Workflow
shape (inputs, outputs, requirements, hints, id, ...), combined with the shared metadata and
documentation fields.

### `ogc.cwl.v1_2_1.CWLAtomic` — CWLAtomic

**Type:** schema

A complete, top-level CWL document describing a single CommandLineTool,
ExpressionTool, or Workflow. Combines the process/workflow-specific fields (class, inputs, outputs,
requirements, hints, ...) with the document-level fields that only apply at the root of a CWL file:
`cwlVersion`, `s:keywords`/authorship-style metadata, and `label`/`doc`.

### `ogc.cwl.v1_2_1.CWLAtomicNested` — CWLAtomicNested

**Type:** schema

Same shape as `CWLAtomic`, for use when a CommandLineTool,
ExpressionTool, or Workflow definition is embedded inline as the `run` value of a Workflow step,
instead of being referenced by file or URL. `cwlVersion` is not repeated here, since it is only
declared once at the document root.

### `ogc.cwl.v1_2_1.CWLGraph` — CWLGraph

**Type:** schema

A CWL document using the `$graph` form: instead of a single process or
workflow definition at the document root, the root carries a `$graph` array (in this register,
constrained to exactly one entry) of process/workflow definitions, plus the shared `cwlVersion` and
document-level metadata/documentation fields.

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepObject` — CWLWorkflowStepObject

**Type:** schema

The executable shape of a single Workflow step: how its
underlying process is invoked (`run`), how workflow parameters are wired to and from it (`in`,
`out`), an optional guard condition (`when`), and scatter/gather behavior (`scatter`,
`scatterMethod`) for fanning the step out over array inputs. Used directly as the value type when
`steps` is given as a map keyed by step id; see `CWLWorkflowStepItem` for the list form, where the
id is an explicit field instead.

### `ogc.cwl.v1_2_1.workflow-step.CWLWorkflowStepItem` — CWLWorkflowStepItem

**Type:** schema

A single Workflow step given in the list form of `steps`, where the step's `id` is
carried as an explicit field alongside `run`/`in`/`out`/`when`/`scatter` rather than being the map
key; see `CWLWorkflowStepObject` for the shape shared with the map form.

### `ogc.cwl.v1_2_1.CWLWorkflowBase` — CWLWorkflowBase

**Type:** schema

Workflow-specific properties (inputs, outputs, steps, requirements, hints), shared by the root Workflow document and its nested-in-step form; not typically profiled on its own.

### `ogc.cwl.v1_2_1.CWLWorkflow` — CWLWorkflow

**Type:** schema

A complete, top-level CWL Workflow document (`class: Workflow`).
Combines the `Workflow`-specific structure (steps, inputs, outputs, requirements, hints) with the
document-level fields that only apply at the root of a CWL file: `cwlVersion`, metadata, and
documentation.

### `ogc.cwl.v1_2_1.CWL` — CWL

**Type:** schema

The root of the register: a Common Workflow Language v1.2.1 Application Package document.

A CWL document is one of three top-level forms: a single CommandLineTool/ExpressionTool/Workflow
definition (`CWLAtomic`), the same wrapped as a nested `run` definition inside a Workflow step
(`CWLAtomicNested`), or a `$graph`-wrapped document (`CWLGraph`).

