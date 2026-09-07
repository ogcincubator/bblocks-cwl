A `CWLExpression` is a string value that embeds a **parameter reference** (`$(...)`) or, when
[InlineJavascriptRequirement](bblocks://ogc.cwl.v1_2_1.requirements.InlineJavascriptRequirement) is declared, a full
**expression** (`$(...)` or `${...}`), to be resolved by the workflow platform at runtime rather than
taken as a literal string.

Any field documented as accepting the pseudo-type `Expression` — for example `valueFrom` in an input
binding, or an argument on a `CommandLineTool` — accepts a `CWLExpression` string.

## Parameter references

Parameter references (`$(...)`) are supported unconditionally, without needing
`InlineJavascriptRequirement`. They use a small, JavaScript-like syntax restricted to symbol lookups,
dotted/bracketed field access, and array indexing (e.g. `$(inputs.myfile.basename)`,
`$(inputs.d.listing[0].path)`), and are designed so implementations can resolve them without embedding a
full JavaScript engine. The root namespace always provides `inputs` (the current process's input
object), `self` (a field-specific contextual value), and `runtime` (execution configuration details).

## Expressions

Expressions (`$(...)` or `${...}`) are arbitrary ECMAScript 5.1 code — an expression or a function body,
respectively — evaluated in a sandboxed context that must return a JSON-compatible value (`null`,
string, number, boolean, array, or object). They are an optional CWL feature: a document may only use
them if it declares [InlineJavascriptRequirement](bblocks://ogc.cwl.v1_2_1.requirements.InlineJavascriptRequirement),
which is also where any shared `expressionLib` helper code is declared.

## String interpolation

If a reference or expression is embedded within surrounding non-whitespace text (rather than being the
field's entire value), the field's effective value becomes a string: the surrounding text with each
`$(...)`/`${...}` replaced by the textual JSON representation of its result. If the reference or
expression *is* the field's entire value (no other non-whitespace characters), the field's effective
value is the referenced/computed value itself, preserving its original type (e.g. a boolean or object,
not just a string).

See also: [Parameter references](https://www.commonwl.org/v1.2/Workflow.html#Parameter_references) and
[Expressions](https://www.commonwl.org/v1.2/Workflow.html#Expressions) in the CWL specification.
