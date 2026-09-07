
# InputBinding (Schema)

`ogc.cwl.v1_2_1.InputBinding` *v1.2.1*

Defines how to specify the input for the command.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

`InputBinding` (CWL's `CommandLineBinding`) controls how the value of an input parameter — or of an
entry in `CommandLineTool.arguments` — is turned into one or more command-line arguments.

When it is nested under an input parameter's `inputBinding`, the term "value" below refers to the
corresponding value in the input object. For a binding listed directly under `arguments`, "value"
instead refers to the result of evaluating `valueFrom`.

The binding behavior depends on the data type of the (effective) value:

- **string**: add `prefix` and the string to the command line.
- **number**: add `prefix` and the decimal representation to the command line.
- **boolean**: if `true`, add `prefix` to the command line; if `false`, add nothing.
- **File**: add `prefix` and the file's `path` to the command line.
- **Directory**: add `prefix` and the directory's `path` to the command line.
- **array**: if `itemSeparator` is given, join the array into a single string with `itemSeparator`
  and add `prefix` followed by that string; otherwise add `prefix` and then recursively process each
  element. An empty array adds nothing.
- **object**: add `prefix` only, then recursively add the object's fields that themselves carry an
  `inputBinding`.
- **null**: add nothing.

If there is a mismatch between the type declared by the input schema and the effective value — for
example because a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) evaluated to something
else — implementations must follow the data type of the effective value, not the declared schema
type.

## Fields

- **`position`** — the sort key used to order arguments on the assembled command line (default `0`).
  May itself be a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression); in that case `self` is the
  value of the bound input parameter (with any declared default already applied), and the expression
  must evaluate to an integer or `null`.
- **`prefix`** — a literal string prepended to the value, e.g. `-o`.
- **`itemSeparator`** — for array values, joins the items into a single command-line argument instead
  of emitting one argument per item.
- **`valueFrom`** — a constant string, or a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) that
  computes the actual value to bind. If the associated input parameter's value is `null`, `valueFrom`
  is not evaluated and nothing is added to the command line. This field is required when the binding
  appears under `arguments` rather than under an input parameter.
- **`shellQuote`** — only meaningful when
  [ShellCommandRequirement](bblocks://ogc.cwl.v1_2_1.requirements.ShellCommandRequirement) is in effect for the
  tool; controls whether the value is shell-quoted (default `true`). Set to `false` to deliberately
  inject shell metacharacters, e.g. for pipes and redirections.

Note that CWL also defines a `separate` field (default `true`, controlling whether `prefix` and the
value are emitted as separate command-line arguments or concatenated into one) which is not currently
part of this block's schema.

## Examples

### Fixed positional argument
Binds an input parameter as a positional command-line argument, using `position` to control
where it lands among the assembled arguments. This is the most common form, adapted from a CWL
conformance test that copies a file with `cat`.

#### json
```json
{
  "position": 1
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/context.jsonld",
  "position": 1
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] ns1:position 1 .


```


### Prefixed, array-valued argument with a computed position
Binds an array-valued input as a single argument by joining its items with `itemSeparator`, adds
a `prefix` before it, and computes the argument's `position` with a
[CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) instead of a literal integer.

#### json
```json
{
  "position": "$(inputs.priority)",
  "prefix": "-I",
  "itemSeparator": ",",
  "valueFrom": "$(self)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/context.jsonld",
  "position": "$(inputs.priority)",
  "prefix": "-I",
  "itemSeparator": ",",
  "valueFrom": "$(self)"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .

[] ns1:itemSeparator "," ;
    ns1:position "$(inputs.priority)" ;
    ns1:prefix "-I" ;
    cwl:valueFrom "$(self)" .


```

## Schema

```yaml
additionalProperties: false
description: Defines how to specify the input for the command.
properties:
  itemSeparator:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#CommandLineBinding/itemSeparator
  position:
    oneOf:
    - type: integer
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#CommandLineBinding/position
  prefix:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#CommandLineBinding/prefix
  shellQuote:
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#CommandLineBinding/shellQuote
  valueFrom:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#valueFrom
title: Input Binding
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
    "position": "cwl:CommandLineBinding/position",
    "prefix": "cwl:CommandLineBinding/prefix",
    "shellQuote": "cwl:CommandLineBinding/shellQuote",
    "valueFrom": "cwl:valueFrom",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/InputBinding`

