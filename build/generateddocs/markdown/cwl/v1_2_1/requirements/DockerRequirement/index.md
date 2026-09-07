
# DockerRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.DockerRequirement` *v1.2.1*

Indicates that a CommandLineTool or ExpressionTool should be run
in a Docker or Docker-compatible (e.g. Singularity, udocker) container, and specifies how to fetch
or build the image (`dockerPull`, `dockerImport`, `dockerLoad`, or `dockerFile`). If listed under
`hints`, the platform may run the tool in the container; if listed under `requirements`, it must.
See the [CWL v1.2 CommandLineTool spec — DockerRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#DockerRequirement)
for the full behavior, including bind-mount and entrypoint handling.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Indicates that a workflow component should be run in a [Docker](https://docker.com) or
Docker-compatible (such as [Singularity](https://www.sylabs.io/) and
[udocker](https://github.com/indigo-dc/udocker)) container environment, and specifies how to fetch or
build the image.

If a `CommandLineTool` lists `DockerRequirement` under `hints`, it may be run in the specified Docker
container; if listed under `requirements`, it must.

The platform must first acquire or install the correct Docker image as specified by exactly one of
`dockerPull`, `dockerImport`, `dockerLoad`, or `dockerFile`, then execute the tool in the container
using `docker run` with the appropriate image and tool command line.

The workflow platform may provide input files and the designated output directory through the use of
volume bind mounts, rewriting file paths in the input object (such as `runtime.outdir` and
`runtime.tmpdir`) to correspond to the Docker bind-mounted locations. The platform must ensure that
`runtime.outdir` and `runtime.tmpdir` are distinct directories. `dockerOutputDirectory` sets the
designated output directory to a specific location inside the container.

When running a tool contained in Docker, the workflow platform must not assume anything about the
contents of the Docker container, except that the generated command line represents a valid command
within the container's runtime environment.

A container image may specify an
[ENTRYPOINT](https://docs.docker.com/engine/reference/builder/#entrypoint) and/or
[CMD](https://docs.docker.com/engine/reference/builder/#cmd). Command line arguments are appended
after all elements of ENTRYPOINT, and override all elements specified using CMD (CMD is only used when
the `CommandLineTool` definition produces an empty command line). Use of implicit ENTRYPOINT or CMD is
discouraged for reproducibility reasons; portable `CommandLineTool` wrappers in which use of a
container is optional must not rely on them, and tools that do rely on them must list
`DockerRequirement` in `requirements` rather than `hints`.

## Interaction with other requirements

If [EnvVarRequirement](bblocks://ogc.cwl.v1_2_1.requirements.EnvVarRequirement) is specified alongside a
`DockerRequirement`, the environment variables must be provided to Docker using `--env` or
`--env-file` and interact with the container's preexisting environment as defined by Docker.

See also: [ResourceRequirement](bblocks://ogc.cwl.v1_2_1.requirements.ResourceRequirement), which specifies the
hardware resources (CPU, RAM, storage) available within the container, and the
[CWL v1.2 CommandLineTool spec — DockerRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#DockerRequirement).

## Examples

### Pulling a published image
A `DockerRequirement` that fetches its image with `docker pull`, adapted from the CWL
conformance test `bwa-mem-tool.cwl`. This is the most common form: `dockerPull` is the only
one of the four mutually exclusive image-source fields (`dockerPull`, `dockerImport`,
`dockerLoad`, `dockerFile`) present.

#### json
```json
{
  "class": "DockerRequirement",
  "dockerPull": "docker.io/python:3-slim"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/context.jsonld",
  "class": "DockerRequirement",
  "dockerPull": "docker.io/python:3-slim"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] a <https://example.org/DockerRequirement> ;
    ns1:dockerPull "docker.io/python:3-slim" .


```


### Pulling an image with a custom output directory
Adapted from the CWL conformance test `docker-output-dir.cwl`. `dockerOutputDirectory`
relocates the designated output directory to a specific path inside the container, which the
tool's command line can then target directly (here, `touch /other/thing`).

#### json
```json
{
  "class": "DockerRequirement",
  "dockerPull": "docker.io/debian:stable-slim",
  "dockerOutputDirectory": "/other"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/context.jsonld",
  "class": "DockerRequirement",
  "dockerPull": "docker.io/debian:stable-slim",
  "dockerOutputDirectory": "/other"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#DockerRequirement/> .

[] a <https://example.org/DockerRequirement> ;
    ns1:dockerOutputDirectory "/other" ;
    ns1:dockerPull "docker.io/debian:stable-slim" .


```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - DockerRequirement
    type: string
    x-jsonld-id: '@type'
  dockerFile:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerFile
  dockerImageId:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerImageId
  dockerImport:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerImport
  dockerLoad:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerLoad
  dockerOutputDirectory:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerOutputDirectory
  dockerPull:
    description: Reference package that will be retrieved and executed by CWL.
    example: docker-registry.host.com/namespace/image:1.2.3
    title: Docker pull reference
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#DockerRequirement/dockerPull
title: DockerRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "dockerFile": "cwl:DockerRequirement/dockerFile",
    "dockerImageId": "cwl:DockerRequirement/dockerImageId",
    "dockerImport": "cwl:DockerRequirement/dockerImport",
    "dockerLoad": "cwl:DockerRequirement/dockerLoad",
    "dockerOutputDirectory": "cwl:DockerRequirement/dockerOutputDirectory",
    "dockerPull": "cwl:DockerRequirement/dockerPull",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/DockerRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/DockerRequirement`

