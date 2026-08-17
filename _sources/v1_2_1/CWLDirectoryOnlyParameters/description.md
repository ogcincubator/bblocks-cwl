`loadListing` is only meaningful for an input/output whose `type` (or array `items`) resolves to
`Directory`: it controls whether, and how deeply, the runtime populates the `listing` field of the
corresponding `Directory` object for use by expressions. It has no effect on `File`-typed parameters —
see [CWLFileOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLFileOnlyParameters) for the parameters that
apply there instead.

The allowed values are defined by [LoadListingEnum](bblocks://ogc.cwl.v1_2_1.LoadListingEnum):
`no_listing`, `shallow_listing`, or `deep_listing`.

If `loadListing` is not set on a given parameter, the effective value is resolved in this order of
precedence:

1. `loadListing` on the individual parameter itself;
2. otherwise, the value inherited from a
   [LoadListingRequirement](bblocks://ogc.cwl.v1_2_1.LoadListingRequirement) in effect for the step;
3. otherwise, `no_listing` by default.

This block only declares the `loadListing` property itself; the conditional logic that restricts its
use to `Directory`-typed parameters lives in
[CWLDirectoryOnlyParametersConditional](bblocks://ogc.cwl.v1_2_1.CWLDirectoryOnlyParametersConditional).
