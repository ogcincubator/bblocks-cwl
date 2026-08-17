`UnknownRequirement` is the catch-all fallback branch used inside
[CWLRequirementsItem](bblocks://ogc.cwl.v1_2_1.CWLRequirementsItem) and
[CWLHintsItem](bblocks://ogc.cwl.v1_2_1.CWLHintsItem) for any requirement/hint `class` that this
register does not model with a dedicated block — most commonly vendor-prefixed extension classes such
as `cwltool:LoadListingRequirement`-style custom classes or arbitrary `x:`/`acme:`-prefixed identifiers
that a particular CWL implementation defines on its own. Its schema only fixes the shape of `class`
(excluding the identifiers already covered by the 18 standard CWL requirement/hint classes) and
otherwise leaves the object open (`additionalProperties: {}`), since the actual content of a
vendor-specific requirement is implementation-defined and unknown to this register.

Note: the `class` exclusion list currently only excludes the 18 standard CWL classes; it does not yet
exclude this register's own OGC-specific hint classes (`BuiltinRequirement`,
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.OGCAPIRequirement),
[WPS1Requirement](bblocks://ogc.cwl.v1_2_1.WPS1Requirement)), so a bare object using one of those three
`class` values currently matches both its dedicated branch and this fallback branch when validated
through the `CWLHintsItem`/`CWLRequirementsItem` `oneOf`. This is a known schema issue tracked
separately and is not fixed here.
