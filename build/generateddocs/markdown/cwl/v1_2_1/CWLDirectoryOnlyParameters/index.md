
# CWLDirectoryOnlyParameters (Schema)

`ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters` *v1.2.1*

Parameters that only apply to Directory-typed (or
Directory-array-typed) inputs/outputs: `loadListing`, controlling whether/how deeply the directory's
contents are enumerated for use in expressions.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

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
   [LoadListingRequirement](bblocks://ogc.cwl.v1_2_1.requirements.LoadListingRequirement) in effect for the step;
3. otherwise, `no_listing` by default.

This block only declares the `loadListing` property itself; the conditional logic that restricts its
use to `Directory`-typed parameters lives in
[type-system/CWLTypeRecordFieldDef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef).

## Examples

### Directory input requesting a shallow listing
A `CommandLineTool` input parameter of type `Directory` that requests a shallow
(top-level only) directory listing, adapted from the CWL conformance test
`listing_shallow2.cwl`.

#### json
```json
{
  "type": "Directory",
  "loadListing": "shallow_listing"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/context.jsonld",
  "type": "Directory",
  "loadListing": "shallow_listing"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] cwl:loadListing "shallow_listing" .


```


### Directory input requesting a deep listing
A `Directory`-typed input parameter that requests a full recursive listing,
adapted from the CWL conformance test `listing_deep2.cwl`.

#### json
```json
{
  "type": "Directory",
  "loadListing": "deep_listing"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/context.jsonld",
  "type": "Directory",
  "loadListing": "deep_listing"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] cwl:loadListing "deep_listing" .


```

## Schema

```yaml
properties:
  loadListing:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LoadListingEnum/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#loadListing
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "loadListing": "cwl:loadListing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDirectoryOnlyParameters/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLDirectoryOnlyParameters`

