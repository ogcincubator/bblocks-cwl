
# CWLExpression (Schema)

`ogc.cwl.v1_2_1.CWLExpression` *v1.2.1*

When combined with 'InlineJavascriptRequirement', this field allows runtime parameter references
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#Expression).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Parameter reference
A parameter reference resolving to the `basename` field of an input `File` parameter named
`myfile`. Since the reference is the field's entire value, the effective value preserves the
referenced value's original type rather than being converted to a string.

#### json
```json
"$(inputs.myfile.basename)"

```


### Inline JavaScript expression
A full JavaScript expression (requires `InlineJavascriptRequirement`) computing a value from
two input parameters.

#### json
```json
"$(inputs.a + inputs.b)"

```

## Schema

```yaml
$comment: 'Whenever this option is applicable for a parameter, any other ''normal''
  string should not be specified.

  For JSON schema validation, there is no easy way to distinguish them unless using
  complicated string patterns.

  '
description: 'When combined with ''InlineJavascriptRequirement'', this field allows
  runtime parameter references

  (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#Expression).

  '
title: CWLExpression
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLExpression`

