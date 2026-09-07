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
