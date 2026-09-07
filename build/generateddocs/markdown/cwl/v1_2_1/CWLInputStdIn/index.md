
# CWLInputStdIn (Schema)

`ogc.cwl.v1_2_1.CWLInputStdIn` *v1.2.1*

Redirects the value of a CWL input to the command's standard input stream (the 'stdin' shorthand or its equivalent 'type: stdin' object form).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This type is only valid for a `CommandLineTool` input that has no
[InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding) of its own — `stdin` redirection and an explicit
`inputBinding` (positional argument, prefix, etc.) are mutually exclusive for the same input, since the
value cannot simultaneously be piped to the command's standard input stream and placed on its command
line.

```yaml
inputs:
  an_input_name:
    type: stdin
```

is equivalent to declaring the input as a `File` that is both marked `streamable` and wired to the root
`CommandLineTool`'s own `stdin` field:

```yaml
inputs:
  an_input_name:
    type: File
    streamable: true

stdin: $(inputs.an_input_name.path)
```

which is exactly the combination this type's schema forbids being declared explicitly (`stdin` must not
be set at the root of the document if it is already implied by an input of this type).

## Examples

### Shorthand string form
The `stdin` shorthand, as used for the `file1` input of the CWL conformance test
[`cat-tool-shortcut.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/cat-tool-shortcut.cwl),
which pipes the input file's contents into the command's standard input.

#### json
```json
"stdin"

```


### Object form
The equivalent explicit object form of the same `stdin` type declaration.

#### json
```json
{
  "type": "stdin"
}

```

## Schema

```yaml
description: 'Indicates that the value passed to this CWL input will be redirected
  to the standard input

  stream of the command.


  Can be defined for only one input and must not be combined with ''stdin'' at the
  root of the CWL

  document.

  '
oneOf:
- enum:
  - stdin
  type: string
- properties:
    type:
      enum:
      - stdin
      type: string
  required:
  - type
  type: object
title: CWLInputStdIn

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputStdIn/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLInputStdIn/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLInputStdIn`

