`ShellCommandRequirement` changes how a `CommandLineTool`'s command line is assembled from
[`CWLCommand`](bblocks://ogc.cwl.v1_2_1.CWLCommand) and
[`CWLArguments`](bblocks://ogc.cwl.v1_2_1.CWLArguments): instead of invoking the tool as a plain
argument vector, the implementation joins every item into a single shell command-line string.

By default, each argument is shell-quoted before being joined, so shell metacharacters in an
argument's value (`|`, `>`, `&&`, etc.) are treated as literal text and cannot affect how the
command is parsed. Setting `shellQuote: false` on an individual argument's `CommandLineBinding`
opts that argument out of quoting, so its literal text is spliced unquoted into the command
line — the mechanism CWL uses to express shell constructs such as pipes (`echo foo | wc -l`) or
redirection between otherwise-independent commands.

Because unquoted arguments are interpreted by the shell, `shellQuote: false` should only be used
for metacharacters under the tool author's control, not for untrusted or dynamically computed
values.
