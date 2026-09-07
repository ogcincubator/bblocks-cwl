
# SoftwarePackage (Schema)

`ogc.cwl.v1_2_1.SoftwarePackage` *v1.2.1*

A single software package entry within a `SoftwareRequirement`:
the package name, optionally the compatible version(s), and optionally one or more IRIs identifying
resources for installing or enabling it (e.g. a Debian or Conda package page), which implementations
may resolve to a concrete install action.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Each field plays a distinct role:

- `package` — the software's name. If the name alone is ambiguous (common, inconsistent across
  package managers, etc.) it should be paired with one or more identifiers in `specs`.
- `version` — the version(s) of the software known to be compatible with the process.
- `specs` — one or more [ReferenceURL](bblocks://ogc.cwl.v1_2_1.ReferenceURL) IRIs identifying
  resources for installing or enabling the named package. Implementations may resolve these IRIs
  to a concrete install action, or fall back to using just the `package` name on a best-effort
  basis.

For example, the IRI `https://packages.debian.org/bowtie` could be resolved with
`apt-get install bowtie`, while `https://anaconda.org/bioconda/bowtie` could be resolved with
`conda install -c bioconda bowtie`. IRIs can also be system-independent, mapping to a specific
software concept rather than a particular package manager entry.

A `SoftwarePackage` normally appears as an item of
[SoftwareRequirement](bblocks://ogc.cwl.v1_2_1.requirements.SoftwareRequirement)'s `packages` property.

## Examples

### Package identified by name and version only
A `SoftwarePackage` entry naming a tool and the version(s) known to work, with no
installation IRIs.

#### json
```json
{
  "package": "screed",
  "version": [ "1.0" ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/context.jsonld",
  "package": "screed",
  "version": [
    "1.0"
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwarePackage/> .

[] ns1:package "screed" ;
    ns1:version "1.0" .


```


### Package identified by an installation IRI
A `SoftwarePackage` entry that pins down an ambiguous package name using a `specs` IRI
resolving to a package repository entry.

#### json
```json
{
  "package": "bowtie",
  "specs": [ "https://packages.debian.org/bowtie" ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/context.jsonld",
  "package": "bowtie",
  "specs": [
    "https://packages.debian.org/bowtie"
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwarePackage/> .

[] ns1:package "bowtie" ;
    ns1:specs <https://packages.debian.org/bowtie> .


```

## Schema

```yaml
additionalProperties: false
properties:
  package:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwarePackage/package
  specs:
    items:
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ReferenceURL/schema.yaml
    type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwarePackage/specs
    x-jsonld-type: '@id'
  version:
    items:
      type: string
    type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwarePackage/version
required:
- package
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "package": "cwl:SoftwarePackage/package",
    "specs": {
      "@id": "cwl:SoftwarePackage/specs",
      "@type": "@id"
    },
    "version": "cwl:SoftwarePackage/version",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/SoftwarePackage`

