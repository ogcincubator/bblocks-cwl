A Workflow step's `in` field connects the step's input parameters to values coming from the
workflow's own inputs, from other steps' outputs, or from literal defaults. CWL allows `in` to be
written in two equivalent forms, captured here as a `oneOf`:

- **Map form** (`CWLWorkflowStepInMap`): an object keyed by input parameter name, where each value
  is either a bare `source` string, a list of `source` strings, or a full input object (see
  [CWLWorkflowStepInputBase](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepInputBase) and
  [CWLWorkflowStepInputDefault](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepInputDefault)).
- **List form** (`CWLWorkflowStepInList`): an array of
  [CWLWorkflowStepInItem](bblocks://ogc.cwl.v1_2_1.CWLWorkflowStepInItem) objects, each of which
  carries its own `id` alongside the same wiring fields.

## Merging multiple inbound data links

If a step input's `source` names more than one upstream parameter, the values are combined
according to `linkMerge`
(see [LinkMergeMethod](bblocks://ogc.cwl.v1_2_1.LinkMergeMethod)): `merge_nested` (the default)
wraps each linked value into one entry of a result list, while `merge_flattened` concatenates
array-valued sources and appends scalar-valued sources into a single flat list. If `linkMerge` is
not specified and `source` has only one entry, the input takes that entry's value directly, without
being wrapped in a list.

CWL also defines a `pickValue` field for this purpose — evaluated after `linkMerge` and before
`scatter`/`valueFrom` — to select non-null values among several inbound links
(`first_non_null`, `the_only_non_null`, `all_non_null`); this is particularly useful alongside
conditional (`when`) steps, whose skipped runs produce `null`. This register's schema does not
currently model `pickValue` as a validated property.

## Other wiring fields

- `valueFrom` (see [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)): overrides or computes
  the final input value, optionally as a CWL parameter-reference expression evaluated against the
  `source` value (`self`) once `MultipleInputFeatureRequirement`/`StepInputExpressionRequirement`
  requirements are satisfied.
- `default` (see [CWLDefault](bblocks://ogc.cwl.v1_2_1.CWLDefault)): the value used when `source` is
  absent, or when the value it produces is `null`; applied before scattering or evaluating
  `valueFrom`.
