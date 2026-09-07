
# CWLCommand (Schema)

`ogc.cwl.v1_2_1.CWLCommand` *v1.2.1*

Command called in the docker image or on shell according to requirements
and hints specifications. Can be omitted if already defined in the docker
image.


[*Status*](http://www.opengis.net/def/status): Under development

## Description

If an array, the first element is the program to execute and any subsequent elements are mandatory
command line arguments that always precede any bindings contributed by `inputBinding` or
[CWLArguments](bblocks://ogc.cwl.v1_2_1.CWLArguments).

If `baseCommand` is omitted, or is an empty array, the first element of the command line produced
after processing input and argument bindings is used as the program to execute instead.

If the program name includes a path separator it must be an absolute path; otherwise, the runner
searches the `$PATH` of the runtime environment (e.g. inside the Docker container specified by a
`DockerRequirement`) to resolve it to an absolute path.

## Examples

### Simple string command
A `CommandLineTool` invoking a single executable with no arguments baked
into `baseCommand` itself, e.g. `cat`.

#### json
```json
"cat"

```


### Command with mandatory leading arguments
A `baseCommand` given as an array. The first element (`cp`) is the
program to execute, and the remaining element (`-r`) is a mandatory
argument that always appears immediately after it on the command line,
before any bindings contributed by inputs or
[CWLArguments](bblocks://ogc.cwl.v1_2_1.CWLArguments).

#### json
```json
["cp", "-r"]

```

## Schema

```yaml
description: 'Command called in the docker image or on shell according to requirements

  and hints specifications. Can be omitted if already defined in the docker

  image.

  '
oneOf:
- title: String command.
  type: string
- additionalProperties: false
  items:
    title: cmd
    type: string
  title: Command Parts
  type: array
title: CWLCommand

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLCommand/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLCommand`

