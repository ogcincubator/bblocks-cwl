
# CWLMetadata (Schema)

`ogc.cwl.v1_2_1.CWLMetadata` *v1.2.1*

Shared document-level metadata fields: `s:keywords` (for search and
categorization) and the process/document `version`.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

A mixin of document-level metadata fields shared by CWL's top-level process types
([CommandLineTool](bblocks://ogc.cwl.v1_2_1.CWLAtomic), [Workflow](bblocks://ogc.cwl.v1_2_1.CWLWorkflow),
[ExpressionTool](bblocks://ogc.cwl.v1_2_1.CWLAtomic)) and their nested/graph-embedded counterparts
([CWLAtomicNested](bblocks://ogc.cwl.v1_2_1.CWLAtomicNested),
[CWLGraphItem](bblocks://ogc.cwl.v1_2_1.CWLGraphItem)). It groups:

- `s:keywords` — an array of non-empty, free-text terms used for search and categorization, drawn
  from the schema.org `Thing/keywords` property that `CommonWorkflowLanguage.yml` mixes into every
  process.
- `version` — the process/document's own version string, distinct from
  [CWLVersion](bblocks://ogc.cwl.v1_2_1.CWLVersion)'s `cwlVersion` (which declares which version of
  the *CWL standard itself* a document conforms to). This `version` is the process author's own
  release identifier for the tool or workflow being described.

Keeping these fields in one reusable block avoids repeating the same two properties across every
place a CWL document can declare a process, and lets a profile constrain both fields uniformly.

## Examples

### Keywords and version on a workflow
Document-level metadata attached to a `Workflow`, giving reviewers a way to search and
categorize it and to track the workflow author's own release of it, independent of which
version of the CWL standard it is written against.

#### json
```json
{
  "s:keywords": ["geospatial", "reprojection", "raster"],
  "version": "1.2.0"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/context.jsonld",
  "s:keywords": [
    "geospatial",
    "reprojection",
    "raster"
  ],
  "version": "1.2.0"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwarePackage/> .
@prefix schema: <https://schema.org/> .

[] schema:keywords "geospatial",
        "raster",
        "reprojection" ;
    ns1:version "1.2.0" .


```


### Version only
Both fields are optional and independent — a process may declare only its own release
version without keywords. The `version` pattern also accepts a dotted pre-release/build
suffix, as in `1.4.2.rc1`.

#### json
```json
{
  "version": "1.4.2.rc1"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/context.jsonld",
  "version": "1.4.2.rc1"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#SoftwarePackage/> .

[] ns1:version "1.4.2.rc1" .


```

## Schema

```yaml
properties:
  s:keywords:
    description: Keywords applied to the process for search and categorization purposes.
    items:
      minLength: 1
      title: keyword
      type: string
    title: KeywordList
    type: array
    x-jsonld-id: https://schema.org/keywords
  version:
    description: Version of the process.
    example: 1.2.3
    pattern: ^\d+(\.\d+(\.\d+(\.[A-Za-z0-9\-_]+)*)*)*$
    title: version
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#SoftwarePackage/version
type: object
x-jsonld-prefixes:
  s: https://schema.org/
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "version": "cwl:SoftwarePackage/version",
    "s": "https://schema.org/",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLMetadata/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLMetadata`

