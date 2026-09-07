
# LoadListingEnum (Schema)

`ogc.cwl.v1_2_1.LoadListingEnum` *v1.2.1*

The allowed values for `loadListing`, controlling how deeply a
Directory's contents are enumerated for use in expressions: `no_listing` (don't load it),
`shallow_listing` (top level only), or `deep_listing` (recurse into subdirectories).

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Deep listing
Requesting a fully recursive directory listing, so subdirectories are also expanded for use
in expressions.

#### json
```json
"deep_listing"

```


### No listing
Suppressing the directory listing entirely, so `listing` is left unset on the `Directory` object.

#### json
```json
"no_listing"

```

## Schema

```yaml
enum:
- no_listing
- shallow_listing
- deep_listing
title: LoadListingEnum
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LoadListingEnum/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LoadListingEnum/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/LoadListingEnum`

