
# SoftwareRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.SoftwareRequirement` *v1.2.1*

A list of software packages that should be configured in the
process's execution environment.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

The `packages` property lists the software the process's execution environment must provide. It
accepts two equivalent shapes:

- an array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage) objects, each naming a
  package and optionally its compatible version(s) and identifying IRIs; or
- an object mapping each package name directly to either its `specs`/`version` list (a bare array
  of strings) or a full [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage) object.

The two forms carry the same information: in the map form, the object key stands in for the
package's `package` field, so it does not need to be repeated inside the value.

Implementations are not required to enforce that the requested software is actually present in the
execution environment; `SoftwareRequirement` only records what versions and packages are known to
be usable, leaving actual configuration/resolution up to the runtime.

## Examples

### Packages listed as an array
`packages` given as an array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage)
objects.

#### json
```json
{
  "class": "SoftwareRequirement",
  "packages": [
    {
      "package": "screed",
      "version": [ "1.0" ]
    },
    {
      "package": "bowtie",
      "specs": [ "https://packages.debian.org/bowtie" ]
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/context.jsonld",
  "class": "SoftwareRequirement",
  "packages": [
    {
      "package": "screed",
      "version": [
        "1.0"
      ]
    },
    {
      "package": "bowtie",
      "specs": [
        "https://packages.debian.org/bowtie"
      ]
    }
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwarePackage/> .
@prefix ns2: <https://w3id.org/cwl/cwl#SoftwareRequirement/> .

[] a <https://example.org/SoftwareRequirement> ;
    ns2:packages [ ns1:package "screed" ;
            ns1:version "1.0" ],
        [ ns1:package "bowtie" ;
            ns1:specs <https://packages.debian.org/bowtie> ] .


```


### Packages listed as a name-keyed map
`packages` given as an object keyed by package name, where each value is either a bare
list of specification IRIs/versions or a full
[SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage) object.

#### json
```json
{
  "class": "SoftwareRequirement",
  "packages": {
    "sourmash": [ "https://doi.org/10.21105/joss.00027" ],
    "screed": {
      "package": "screed",
      "version": [ "1.0" ]
    }
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/context.jsonld",
  "class": "SoftwareRequirement",
  "packages": {
    "sourmash": [
      "https://doi.org/10.21105/joss.00027"
    ],
    "screed": {
      "package": "screed",
      "version": [
        "1.0"
      ]
    }
  }
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwareRequirement/> .
@prefix ns2: <https://w3id.org/cwl/cwl#SoftwarePackage/> .

<https://example.org/screed> ns2:package "screed" ;
    ns2:version "1.0" .

[] a <https://example.org/SoftwareRequirement> ;
    ns1:packages <https://example.org/screed>,
        "https://doi.org/10.21105/joss.00027" .


```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    enum:
    - SoftwareRequirement
    type: string
    x-jsonld-id: '@type'
  packages:
    oneOf:
    - items:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/schema.yaml
      type: array
    - additionalProperties:
        oneOf:
        - items:
            type: string
          type: array
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/SoftwarePackage/schema.yaml
      description: Mapping of 'package' name to its specifications.
      type: object
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwareRequirement/packages
    x-jsonld-container: '@id'
required:
- packages
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "packages": {
      "@context": {
        "package": "cwl:SoftwarePackage/package",
        "specs": {
          "@id": "cwl:SoftwarePackage/specs",
          "@type": "@id"
        },
        "version": "cwl:SoftwarePackage/version"
      },
      "@id": "cwl:SoftwareRequirement/packages",
      "@container": "@id"
    },
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/SoftwareRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/SoftwareRequirement`

