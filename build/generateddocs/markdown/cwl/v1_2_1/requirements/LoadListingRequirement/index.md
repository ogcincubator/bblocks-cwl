
# LoadListingRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.LoadListingRequirement` *v1.2.1*

Specify the desired behavior for loading the listing field of a 'Directory' object for use by expressions
(see also: https://www.commonwl.org/v1.2/CommandLineTool.html#LoadListingRequirement).


[*Status*](http://www.opengis.net/def/status): Under development

## Description

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

## Examples

### Deep directory listing requirement
A `CommandLineTool` requirement asking the implementation to recursively load the full
directory listing of every `Directory` input, so nested subdirectories are also enumerated
for use in expressions.

#### json
```json
{
  "class": "LoadListingRequirement",
  "loadListing": "deep_listing"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/context.jsonld",
  "class": "LoadListingRequirement",
  "loadListing": "deep_listing"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] a <https://example.org/LoadListingRequirement> ;
    cwl:loadListing "deep_listing" .


```


### Shallow directory listing requirement
A requirement asking the implementation to load only the top-level entries of each
`Directory` input's listing, without recursing into subdirectories.

#### json
```json
{
  "class": "LoadListingRequirement",
  "loadListing": "shallow_listing"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/context.jsonld",
  "class": "LoadListingRequirement",
  "loadListing": "shallow_listing"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] a <https://example.org/LoadListingRequirement> ;
    cwl:loadListing "shallow_listing" .


```

## Schema

```yaml
additionalProperties: false
description: 'Specify the desired behavior for loading the listing field of a ''Directory''
  object for use by expressions

  (see also: https://www.commonwl.org/v1.2/CommandLineTool.html#LoadListingRequirement).

  '
properties:
  class:
    enum:
    - LoadListingRequirement
    type: string
    x-jsonld-id: '@type'
  loadListing:
    $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LoadListingEnum/schema.yaml
    x-jsonld-id: https://w3id.org/cwl/cwl#loadListing
required:
- loadListing
title: LoadListingRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "loadListing": "cwl:loadListing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/LoadListingRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/LoadListingRequirement`

