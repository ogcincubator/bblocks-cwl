Define a list of environment variables which will be set in the execution environment of the tool.
Each entry is an [`EnvironmentDef`](#EnvironmentDef): an `envName` (the variable name) paired with an
`envValue`, which may be a literal string or a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)
evaluated at runtime — for example, to forward the value of an input parameter, or the result of
executing an expression such as building a configuration value from a template. Expression evaluation
requires `InlineJavascriptRequirement` to also be in effect.

`envDef` accepts two equivalent representations:

- An array of `EnvironmentDef` objects, each with explicit `envName`/`envValue` properties.
- A mapping of `envName` to `envValue` (either the value directly, or a nested `EnvironmentDef`-like
  object) — a shorthand JSON-LD map form of the same data.

## Interaction with other requirements

If `EnvVarRequirement` is specified alongside a
[DockerRequirement](bblocks://ogc.cwl.v1_2_1.requirements.DockerRequirement), the environment variables must be
provided to Docker using `--env` or `--env-file`, and interact with the container's preexisting
environment as defined by Docker.

See also: the [CWL v1.2 CommandLineTool spec — EnvVarRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#EnvVarRequirement).
