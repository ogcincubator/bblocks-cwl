
# CWLFileOnlyParameters (Schema)

`ogc.cwl.v1_2_1.CWLFileOnlyParameters` *v1.2.1*

Parameters that only apply to File-typed (or File-array-typed)
inputs/outputs: `format` (the file's content format/media type, as an IRI or CWL expression),
`streamable`, `loadContents` (whether to load the first 64 KiB of file content for use in
expressions), and `secondaryFiles` (associated files expected alongside the primary one).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

These four fields only have meaning when the `type` (or `items`, for arrays) of the input/output
parameter they belong to resolves to `File`; on any other type they are meaningless and should be
absent. Applying them is enforced separately by
[type-system/CWLTypeRecordFieldDef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef), which
uses an `if`/`then`/`else` conditional on the parameter's `type`/`items` to require this schema when
`File` is detected and forbid these properties otherwise. The directory-typed counterparts —
`loadListing` (see [LoadListingRequirement](bblocks://ogc.cwl.v1_2_1.requirements.LoadListingRequirement)) — are
covered separately by
[CWLDirectoryOnlyParameters](bblocks://ogc.cwl.v1_2_1.CWLDirectoryOnlyParameters).

- **`format`** — the IRI of a concept node (preferably from an ontology) representing the file's
  content format/media type, or a CWL expression that evaluates to one. Reasoning about format
  compatibility is done by checking that an input file's format is the same as, `owl:equivalentClass`
  of, or `rdfs:subClassOf` the format required by the input parameter.
- **`secondaryFiles`** — one or more patterns (or expressions) describing additional files or
  directories that must be staged alongside the primary file, such as an index file or an external
  reference. A plain (non-expression) pattern string is applied to the primary file's path: a
  trailing `?` marks the secondary file optional, and each leading `^` strips one file extension from
  the path before the remainder of the pattern is appended.
- **`streamable`** — when `true`, indicates the file is read or written sequentially without seeking,
  which an implementation may use to decide whether it can stream the file's contents through a named
  pipe. Defaults to `false`.
- **`loadContents`** — when `true`, requires the file to be a UTF-8 text file of 64 KiB or smaller;
  the implementation reads its entire contents into the `contents` field of the File object so it is
  available to expressions. It is a fatal error if the file exceeds the 64 KiB limit.

## Examples

### Indexed FASTA input with required and optional secondary files
A `File`-typed input declaring its content format and a list of secondary files with
explicit `pattern`/`required` schemas, adapted from the CWL v1.2 conformance test
`docker-array-secondaryfiles.cwl`.

#### json
```json
{
  "format": "http://edamontology.org/format_1929",
  "streamable": false,
  "secondaryFiles": [
    {
      "pattern": ".fai",
      "required": true
    },
    {
      "pattern": ".crai",
      "required": false
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/context.jsonld",
  "format": "http://edamontology.org/format_1929",
  "streamable": false,
  "secondaryFiles": [
    {
      "pattern": ".fai",
      "required": true
    },
    {
      "pattern": ".crai",
      "required": false
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#FieldBase/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] ns1:streamable false ;
    cwl:format <http://edamontology.org/format_1929> ;
    cwl:secondaryFiles [ ],
        [ ] .


```


### Streamed file loaded for use in an expression
A `File`-typed input whose contents are read (subject to the 64 KiB `loadContents` limit)
and made available to CWL expressions, with a single secondary file declared using the
shorthand string form (`^` strips one extension, trailing `?` marks it optional).

#### json
```json
{
  "loadContents": true,
  "streamable": true,
  "secondaryFiles": "^.bai?"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/context.jsonld",
  "loadContents": true,
  "streamable": true,
  "secondaryFiles": "^.bai?"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#FieldBase/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] ns1:streamable true ;
    cwl:loadContents true ;
    cwl:secondaryFiles "^.bai?" .


```

## Schema

```yaml
$defs:
  CWLTypeRecordSecondaryFiles:
    oneOf:
    - $comment: Either an expression or the regex pattern directly.
      $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    - $ref: '#/$defs/CWLTypeRecordSecondaryFileSchema'
    - items:
        $comment: Either an expression or the regex pattern directly.
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      type: array
    - items:
        $ref: '#/$defs/CWLTypeRecordSecondaryFileSchema'
      type: array
  CWLTypeRecordSecondaryFileSchema:
    additionalProperties: false
    properties:
      pattern:
        $comment: Either an expression or the regex pattern directly.
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      required:
        oneOf:
        - type: boolean
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    required:
    - pattern
    type: object
properties:
  format:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    - items:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      type: array
    x-jsonld-id: https://w3id.org/cwl/cwl#format
    x-jsonld-type: '@id'
  loadContents:
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#loadContents
  secondaryFiles:
    $ref: '#/$defs/CWLTypeRecordSecondaryFiles'
    x-jsonld-id: https://w3id.org/cwl/cwl#secondaryFiles
  streamable:
    type: boolean
    x-jsonld-id: https://w3id.org/cwl/cwl#FieldBase/streamable
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "format": {
      "@id": "cwl:format",
      "@type": "@id"
    },
    "loadContents": "cwl:loadContents",
    "secondaryFiles": "cwl:secondaryFiles",
    "streamable": "cwl:FieldBase/streamable",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLFileOnlyParameters/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLFileOnlyParameters`

