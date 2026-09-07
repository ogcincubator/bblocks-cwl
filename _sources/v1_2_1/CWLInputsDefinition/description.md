Defines the input parameters of a `CommandLineTool` or `Workflow`. A process is ready to run when all
of its required input parameters are associated with concrete values; the schema declared for each
parameter is used both to validate a submitted input object and to build a user interface for
constructing one. If an input parameter is missing from the input object it must be treated as `null`
(or as the parameter's `default`, if one is provided) for the purposes of validation and expression
evaluation.

CWL accepts two equivalent notations for this field, reflected in this schema as a `oneOf`:

- a **list** of [CWLInputItem](bblocks://ogc.cwl.v1_2_1.CWLInputItem) objects, each carrying its own
  `id`; or
- a **map** keyed by input identifier, whose values are either a bare
  [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand, a nested
  [CWLInputObject](bblocks://ogc.cwl.v1_2_1.CWLInputObject), an input redirected from standard input
  (`CWLInputStdIn`), or an `$import` directive (`CWLImport`) pulling in externally-defined inputs.

The map form is additionally constrained to not itself look like an `$import` directive, since a
generic mapping of identifier strings to values could otherwise be ambiguous with the `$import` key.
