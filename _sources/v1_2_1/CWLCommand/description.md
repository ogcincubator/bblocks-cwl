If an array, the first element is the program to execute and any subsequent elements are mandatory
command line arguments that always precede any bindings contributed by `inputBinding` or
[CWLArguments](bblocks://ogc.cwl.v1_2_1.CWLArguments).

If `baseCommand` is omitted, or is an empty array, the first element of the command line produced
after processing input and argument bindings is used as the program to execute instead.

If the program name includes a path separator it must be an absolute path; otherwise, the runner
searches the `$PATH` of the runtime environment (e.g. inside the Docker container specified by a
`DockerRequirement`) to resolve it to an absolute path.
