Command line bindings that are not directly associated with an input parameter. Each item is either
a plain string, used verbatim as a literal argument, or an [InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding)
object, which additionally lets an argument declare a `prefix`, a `position`, and a `valueFrom`
expression to compute its value.

Together with any `inputBinding` declared on the tool's inputs, these bindings are sorted by their
numeric `position` (lower values first, default `0`; ties broken by the input's declaration order)
to build the final command line, after the leading elements from
[CWLCommand](bblocks://ogc.cwl.v1_2_1.CWLCommand). When a value needs shell metacharacters or
quoting beyond a plain literal, see [ShellCommandRequirement](bblocks://ogc.cwl.v1_2_1.ShellCommandRequirement).
