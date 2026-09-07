
# CWLOutputStdOut (Schema)

`ogc.cwl.v1_2_1.CWLOutputStdOut` *v1.2.1*

Redirects the command's standard output stream to a CWL output (the 'stdout' shorthand or its equivalent 'type: stdout' object form).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This type is only valid for a `CommandLineTool` output that has no
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding) of its own — the glob pattern used to pick up
the captured stream is derived instead, either from the root document's `stdout` field or, if that is
absent, from a randomly generated filename.

```yaml
outputs:
  an_output_name:
    type: stdout

stdout: a_stdout_file
```

is equivalent to declaring the output as a `File` that is both marked `streamable` and whose
`outputBinding.glob` matches the root `stdout` filename:

```yaml
outputs:
  an_output_name:
    type: File
    streamable: true
    outputBinding:
      glob: a_stdout_file

stdout: a_stdout_file
```

If a `CommandLineTool` chains multiple commands (e.g. via `ShellCommandRequirement`), the file named by
`stdout` must capture the combined output of every command, not just the last one.

## Examples

### Shorthand string form
The `stdout` shorthand, as used for the `output_file` output of the CWL conformance test
[`cat3-tool-shortcut.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/cat3-tool-shortcut.cwl),
which captures the command's standard output stream into that output.

#### json
```json
"stdout"

```


### Object form
The equivalent explicit object form of the same `stdout` type declaration.

#### json
```json
{
  "type": "stdout"
}

```

## Schema

```yaml
description: 'Indicates that the data pushed to the standard output stream by the
  command will be redirected

  to this CWL output.


  Can be defined for only one output. If combined with ''stdout'' at the root of the
  CWL document,

  that definition will indicate the desired name of the output file where the output
  stream will

  be written to. A random name will be applied for the file of this output unless
  otherwise

  specified.

  '
oneOf:
- enum:
  - stdout
  type: string
- properties:
    type:
      enum:
      - stdout
      type: string
  required:
  - type
  type: object
title: CWLOutputStdOut

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdOut/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdOut/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputStdOut`

