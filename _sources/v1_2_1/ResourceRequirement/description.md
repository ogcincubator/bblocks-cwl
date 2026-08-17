Specify basic hardware resource requirements.

"min" is the minimum amount of a resource that must be reserved to schedule a job. If "min"
cannot be satisfied, the job should not be run.

"max" is the maximum amount of a resource that the job shall be allocated. If a node has
sufficient resources, multiple jobs may be scheduled on a single node provided each job's "max"
resource requirements are met. If a job attempts to exceed its resource allocation, an
implementation may deny additional resources, which may result in job failure.

If both "min" and "max" are specified, an implementation may choose to allocate any amount
between "min" and "max", with the actual allocation provided in the `runtime` object.

If "min" is specified but "max" is not, then "max" == "min". If "max" is specified but "min" is
not, then "min" == "max".

It is an error if max < min. It is an error if the value of any of these fields is negative.

If neither "min" nor "max" is specified for a resource, the defaults are: 1 core, 256 MiB RAM,
1024 MiB output directory storage, 1024 MiB temporary directory storage.

See also: [CWL v1.2 CommandLineTool spec — ResourceRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#ResourceRequirement).
