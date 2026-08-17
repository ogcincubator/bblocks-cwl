To use scatter/gather, [ScatterFeatureRequirement](bblocks://ogc.cwl.v1_2_1.ScatterFeatureRequirement)
must be specified in the workflow or workflow step requirements.

A "scatter" operation specifies that the associated workflow step or subworkflow should execute
separately over a list of input elements. Each job making up a scatter operation is independent and
may be executed concurrently.

The `scatter` field specifies one or more input parameters which will be scattered. An input
parameter may be listed more than once. The declared type of each input parameter implicitly
becomes an array of items of the input parameter type. If a parameter is listed more than once, it
becomes a nested array. As a result, upstream parameters which are connected to scattered parameters
must be arrays.

All output parameter types are also implicitly wrapped in arrays. Each job in the scatter results in
an entry in the output array.

If any scattered parameter's runtime value is an empty array, all outputs are set to empty arrays and
no work is done for the step, according to applicable scattering rules.

If `scatter` declares more than one input parameter, [CWLScatterMethod](bblocks://ogc.cwl.v1_2_1.CWLScatterMethod)
describes how to decompose the input into a discrete set of jobs.
