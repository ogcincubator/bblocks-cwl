
# UnknownRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.UnknownRequirement` *v1.2.1*

Generic schema to allow alternative CWL requirements/hints not explicitly defined in schemas.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

`UnknownRequirement` is the catch-all fallback branch used inside
[CWLRequirementsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLRequirementsItem) and
[CWLHintsItem](bblocks://ogc.cwl.v1_2_1.requirements.CWLHintsItem) for any requirement/hint `class` that this
register does not model with a dedicated block — most commonly vendor-prefixed extension classes such
as `cwltool:LoadListingRequirement`-style custom classes or arbitrary `x:`/`acme:`-prefixed identifiers
that a particular CWL implementation defines on its own. Its schema only fixes the shape of `class`
(excluding the identifiers already covered by the 18 standard CWL requirement/hint classes) and
otherwise leaves the object open (`additionalProperties: {}`), since the actual content of a
vendor-specific requirement is implementation-defined and unknown to this register.

Note: the `class` exclusion list currently only excludes the 18 standard CWL classes; it does not yet
exclude this register's own OGC-specific hint classes (`BuiltinRequirement`,
[OGCAPIRequirement](bblocks://ogc.cwl.v1_2_1.requirements.OGCAPIRequirement),
[WPS1Requirement](bblocks://ogc.cwl.v1_2_1.requirements.WPS1Requirement)), so a bare object using one of those three
`class` values currently matches both its dedicated branch and this fallback branch when validated
through the `CWLHintsItem`/`CWLRequirementsItem` `oneOf`. This is a known schema issue tracked
separately and is not fixed here.

## Examples

### Vendor-specific extension requirement
A vendor-prefixed requirement/hint class (here, an invented `acme:CustomRequirement`)
that falls outside the standard CWL requirement classes and this register's own
OGC-specific hints. `UnknownRequirement` acts as the catch-all extension point that
accepts such vendor-defined classes with arbitrary additional properties.

#### json
```json
{
  "class": "acme:CustomRequirement",
  "acme:priority": "high",
  "acme:retries": 3
}

```

## Schema

```yaml
additionalProperties: {}
description: Generic schema to allow alternative CWL requirements/hints not explicitly
  defined in schemas.
properties:
  class:
    description: CWL requirement class specification.
    example: UnknownRequirement
    not:
      enum:
      - cwltool:CUDARequirement
      - DockerRequirement
      - SoftwareRequirement
      - ShellCommandRequirement
      - EnvVarRequirement
      - SchemaDefRequirement
      - InitialWorkDirRequirement
      - InlineJavascriptRequirement
      - InplaceUpdateRequirement
      - LoadListingRequirement
      - NetworkAccess
      - ResourceRequirement
      - ScatterFeatureRequirement
      - ToolTimeLimit
      - WorkReuse
      - MultipleInputFeatureRequirement
      - StepInputExpressionRequirement
      - SubworkflowFeatureRequirement
      - BuiltinRequirement
      - OGCAPIRequirement
      - WPS1Requirement
    title: Requirement Class Identifier
    type: string
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/UnknownRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/UnknownRequirement/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/UnknownRequirement`

