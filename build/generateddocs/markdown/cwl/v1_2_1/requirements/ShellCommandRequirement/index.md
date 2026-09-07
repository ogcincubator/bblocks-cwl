
# ShellCommandRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.ShellCommandRequirement` *v1.2.1*

Modifies CommandLineTool execution to generate a single
shell command-line string: each item in `arguments` is joined with spaces and shell-quoted, unless
its `CommandLineBinding` sets `shellQuote: false` — in which case it is joined unquoted, allowing
shell metacharacters such as `|` for pipes.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Enabling ShellCommandRequirement on a CommandLineTool
A `CommandLineTool` requirements entry that enables shell command-line generation,
allowing individual `arguments` items to opt out of quoting via `shellQuote: false`
(e.g. to inject a pipe `|` between two commands).

#### json
```json
{
  "class": "ShellCommandRequirement"
}

```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - ShellCommandRequirement
    type: string
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ShellCommandRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/ShellCommandRequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/ShellCommandRequirement`

