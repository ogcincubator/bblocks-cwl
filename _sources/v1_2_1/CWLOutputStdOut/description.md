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
