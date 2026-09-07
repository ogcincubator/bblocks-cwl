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
