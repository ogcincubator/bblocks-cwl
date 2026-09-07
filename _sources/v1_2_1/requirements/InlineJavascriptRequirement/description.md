Indicates that the workflow platform must support inline Javascript expressions. If this requirement
is not present, the workflow platform must not perform expression interpolation
(see [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)).

## `expressionLib`

The `expressionLib` field lists additional code fragments that are inserted before executing any
expression code, allowing function definitions that may then be called from CWL expressions. Each
entry is either a literal string of Javascript source, or an object with a single `$include` field
naming an external file to be inlined verbatim.

See also: the
[CWL v1.2 CommandLineTool spec — InlineJavascriptRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#InlineJavascriptRequirement).
