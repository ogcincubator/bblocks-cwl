The `outputs` field of a CWL `Process` (a `CommandLineTool`, `Workflow`, or `ExpressionTool`),
defining the parameters representing the output of the process. It is used both to generate the
process's output object and to validate it. CWL allows this field to be written in either of two
equivalent shapes, plus an `$import` escape hatch:

- **List form** (`CWLOutputList`) — an array of
  [CWLOutputItem](bblocks://ogc.cwl.v1_2_1.CWLOutputItem) objects, each carrying its own `id`
  alongside `type` and the other output properties. This is the more verbose but unambiguous form.
- **Map form** (`CWLOutputMap`) — an object whose keys are the output identifiers and whose values
  are either a bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) shorthand (e.g. `"File"`), a full
  [CWLOutputObject](bblocks://ogc.cwl.v1_2_1.CWLOutputObject), or a `stdout`/`stderr` shorthand (see
  [CWLOutputStdOut](bblocks://ogc.cwl.v1_2_1.CWLOutputStdOut) /
  [CWLOutputStdErr](bblocks://ogc.cwl.v1_2_1.CWLOutputStdErr)). This is the more compact form
  typically seen in hand-written CWL documents.
- An `$import` directive (see [CWLImport](bblocks://ogc.cwl.v1_2_1.CWLImport)), pointing to an
  external file that supplies the outputs definition. The schema explicitly excludes documents that
  would otherwise also match the map form from matching as a plain map, to avoid the two branches
  overlapping on a generic `$import`-only mapping key.

Only one of these three shapes may be used for a given `outputs` field; a CWL processor accepts
whichever the document uses and treats them as equivalent.
