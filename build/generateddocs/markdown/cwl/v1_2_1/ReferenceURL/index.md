
# ReferenceURL (Schema)

`ogc.cwl.v1_2_1.ReferenceURL` *v1.2.1*

A web-resolvable reference URL (http(s) or ftp) pointing to
documentation, a package repository, or similar external resource associated with a requirement or
software package.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This block profiles the generic [`ogc.ogc-utils.iri-or-curie`](bblocks://ogc.ogc-utils.iri-or-curie)
block, adding the `format`/`pattern` constraints from the upstream CWL schema that narrow an
otherwise-generic IRI/CURIE string down to something that actually looks like a resolvable web
address: an optional `http`, `https`, or `ftp`(`s`) scheme followed by a host (domain name,
`localhost`, IPv4, or bracketed IPv6 literal), an optional port, and an optional path/query.

It is used wherever the upstream CWL schema points to external resources rather than in-document
identifiers — for example the `specs` array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage),
which lists URLs identifying a piece of software in package repositories such as
[Anaconda.org](https://anaconda.org) or [Debian packages](https://packages.debian.org).

## Examples

### Package repository URL
A URL pointing to a software package's entry in a package repository, as used in the `specs`
array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage).

#### json
```json
"https://anaconda.org/bioconda/samtools"

```


### Documentation URL
A URL pointing to external documentation associated with a requirement.

#### json
```json
"https://www.commonwl.org/v1.2/Workflow.html"

```

## Schema

```yaml
allOf:
- $ref: https://opengeospatial.github.io/bblocks/annotated-schemas/ogc-utils/iri-or-curie/schema.yaml
- format: url
  pattern: ^((?:http|ftp)s?:\/\/)?(?!.*\/\/.*$)(?:(?:[A-Za-z0-9](?:[A-Za-z0-9-]{0,61}[A-Za-z0-9])?\.)+(?:[A-Za-z]{2,6}\.?|[A-Za-z0-9-]{2,}\.?)|localhost|\[[a-f0-9:]+\]|\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})(?::\d+)?(?:\/?|[/?]\S+)$
  type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ReferenceURL/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/ReferenceURL/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/ReferenceURL`

