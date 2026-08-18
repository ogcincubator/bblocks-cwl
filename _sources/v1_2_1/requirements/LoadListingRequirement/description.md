`LoadListingRequirement` lets a `CommandLineTool` or `Workflow` set a default for how deeply
`Directory` inputs are enumerated before their `listing` field becomes available to expressions
(e.g. `inputs.d.listing`). The allowed behaviors are the three
[LoadListingEnum](bblocks://ogc.cwl.v1_2_1.LoadListingEnum) values: `no_listing`, `shallow_listing`,
and `deep_listing`.

Without this requirement, an implementation defaults to `no_listing` — a `Directory` object's
`listing` is left unset unless something asks for it. `LoadListingRequirement` can raise that
default for the whole process, but the setting is layered: an individual input parameter's own
`loadListing` field (part of `LoadContents`) always takes precedence over the process-wide
requirement, which in turn only applies when no per-parameter value is given. In order of
precedence:

1. `loadListing` on an individual input parameter
2. The process's `LoadListingRequirement`
3. The implicit default, `no_listing`

Loading a listing — especially `deep_listing`, which recurses into every subdirectory — can be
costly for large or deeply nested directory trees, so tools should only request the depth of
listing their expressions actually need.
