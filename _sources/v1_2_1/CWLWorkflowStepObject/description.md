## Scatter/gather

To use scatter/gather, `ScatterFeatureRequirement` must be listed among the workflow's or workflow
step's [requirements](bblocks://ogc.cwl.v1_2_1.CWLRequirementsItem).

A scatter operation specifies that the step (or subworkflow) should execute separately over a list
of input elements. Each job making up a scatter operation is independent and may be executed
concurrently. `scatter` names one or more of the step's [`in`](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepIn)
parameters to scatter over; an input parameter may be listed more than once, in which case it
becomes a nested array. The declared type of each scattered input parameter implicitly becomes an
array of items of that type, so upstream parameters connected to it must themselves be arrays. All
[`out`](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepOut) parameter types are likewise implicitly wrapped
in arrays, with each scatter job contributing one entry. If a scattered parameter's runtime value is
an empty array, all outputs are set to empty arrays and no work is done for the step.

When `scatter` names more than one input parameter, `scatterMethod` says how to decompose the inputs
into a discrete set of jobs:

- **dotproduct** — the input arrays are aligned and one element is taken from each to construct each
  job. It is an error if the input arrays are not all the same length.
- **nested_crossproduct** — the Cartesian product of the inputs, producing a job for every
  combination of the scattered inputs. Output arrays are nested, one level per scattered input, in
  the order the inputs are listed in `scatter`.
- **flat_crossproduct** — the same Cartesian product as `nested_crossproduct`, but the output arrays
  are flattened to a single level, still listed in the order the inputs appear in `scatter`.

## Conditional execution

`when` makes execution of the step conditional on an [expression](bblocks://ogc.cwl.v1_2_1.CWLExpression)
that is evaluated with `inputs` bound to the step's input object (or, for a scattered step, to each
individual scatter job's input object) and must return a boolean value; it is an error for the
expression to return anything else. A step whose condition evaluates to `false` is *skipped* and
produces `null` for all of its output parameters. Because the condition is evaluated per scatter job,
some jobs in a scatter may run while others are skipped; when the results are gathered, skipped jobs
appear as `null` entries in the output arrays.

Conditionals are an optional CWL feature: an implementation that does not support them must return a
fatal error when asked to execute a workflow that relies on conditional constructs it does not
implement.

## Subworkflows

To nest a workflow as the `run` value of a step, `SubworkflowFeatureRequirement` must be listed among
the workflow's or workflow step's requirements. It is a fatal error for a workflow to directly or
indirectly invoke itself as a subworkflow.
