
# CWLOutputStdErr (Schema)

`ogc.cwl.v1_2_1.CWLOutputStdErr` *v1.2.1*

Redirects the command's standard error stream to a CWL output (the 'stderr' shorthand or its equivalent 'type: stderr' object form).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This type is only valid for a `CommandLineTool` output that has no
[OutputBinding](bblocks://ogc.cwl.v1_2_1.OutputBinding) of its own — the glob pattern used to pick up
the captured stream is derived instead, either from the root document's `stderr` field or, if that is
absent, from a randomly generated filename.

```yaml
outputs:
  an_output_name:
    type: stderr

stderr: a_stderr_file
```

is equivalent to declaring the output as a `File` that is both marked `streamable` and whose
`outputBinding.glob` matches the root `stderr` filename:

```yaml
outputs:
  an_output_name:
    type: File
    streamable: true
    outputBinding:
      glob: a_stderr_file

stderr: a_stderr_file
```

## Examples

### Shorthand string form
The `stderr` shorthand, as used for the `output_file` output of the CWL conformance test
[`stderr-shortcut.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/stderr-shortcut.cwl),
which captures the command's standard error stream into that output.

#### json
```json
"stderr"

```


### Object form
The equivalent explicit object form of the same `stderr` type declaration.

#### json
```json
{
  "type": "stderr"
}

```

## Schema

```yaml
description: 'Indicates that the data pushed to the standard error stream by the command
  will be redirected

  to this CWL output.


  Can be defined for only one output. If combined with ''stderr'' at the root of the
  CWL document,

  that definition will indicate the desired name of the output file where the error
  stream will

  be written to. A random name will be applied for the file of this output unless
  otherwise

  specified.

  '
oneOf:
- enum:
  - stderr
  type: string
- properties:
    type:
      enum:
      - stderr
      type: string
  required:
  - type
  type: object
title: CWLOutputStdErr

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLOutputStdErr/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLOutputStdErr`

