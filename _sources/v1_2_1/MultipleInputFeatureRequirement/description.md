Without this requirement, a [`WorkflowStepInput`](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepInputBase)'s
`source` field must reference a single upstream parameter. Declaring
`MultipleInputFeatureRequirement` lifts that restriction, allowing `source` to list an array of
upstream parameters whose values are merged into the sink input.

The merge behavior is controlled by the sink input's `linkMerge` field
(see [`LinkMergeMethod`](bblocks://ogc.cwl.v1_2_1.LinkMergeMethod)): `merge_nested` (the default)
wraps the value from each link into one entry of a list, while `merge_flattened` concatenates
array-valued links into a single flat list. If `linkMerge` is left unset and `source` lists more
than one upstream parameter, `merge_nested` applies; if `source` lists only one, the input takes
that single value directly, unwrapped.
