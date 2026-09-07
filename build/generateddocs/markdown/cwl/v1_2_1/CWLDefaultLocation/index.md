
# CWLDefaultLocation (Schema)

`ogc.cwl.v1_2_1.CWLDefaultLocation` *v1.2.1*

The shape of a `default` value for a File- or Directory-typed
input: a literal File or Directory object, identified by a `path` or `location` and optionally
`basename`/`nameroot`, used when no value is provided for the input at execution time.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

A CWL [`File`](https://www.commonwl.org/v1.2/Workflow.html#File) or
[`Directory`](https://www.commonwl.org/v1.2/Workflow.html#Directory) object identifies the resource it
represents through one of two mutually-non-exclusive but here XOR-constrained properties:

- `location` — an IRI that uniquely identifies the file or directory. Implementations must support the
  `file://` scheme and may support others (e.g. `http://`); a relative reference is resolved against the
  IRI of the document it appears in.
- `path` — a filesystem path available on the same host as the CWL runner (for inputs) or the runtime
  environment of a tool execution (for outputs).

This block requires exactly one of the two (`oneOf: [{required: [path]}, {required: [location]}]`),
alongside the mandatory `class` (`File` or `Directory`) and the optional `basename`/`nameroot`
properties, which name the file as staged on disk when it differs from the resource name.

It intentionally omits every other `File`/`Directory` field (`checksum`, `size`, `secondaryFiles`,
`listing`, `contents`, …) that only matter once a value is materialized at runtime — a `default` is a
literal value supplied at authoring time, not a description of a staged file, so those fields have no
role here.

This shape is reused across the register wherever a *literal* `File`/`Directory` default value is
needed: as a `default` value branch in [CWLDefault](bblocks://ogc.cwl.v1_2_1.CWLDefault), and as the
`default` shape enforced for `File`/`Directory`-typed inputs by
[CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional).

## Examples

### File identified by location
A literal File object identified by a `location` IRI, adapted from
[`bwa-mem-tool.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/bwa-mem-tool.cwl).

#### json
```json
{
  "class": "File",
  "location": "args.py"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/context.jsonld",
  "class": "File",
  "location": "args.py"
}
```

#### ttl
```ttl

<https://example.org/args.py> a <https://example.org/File> .


```


### File identified by path
A literal File object identified by a filesystem `path`, adapted from
[`dynresreq-workflow-inputdefault.cwl`](https://github.com/common-workflow-language/cwl-v1.2/blob/main/tests/dynresreq-workflow-inputdefault.cwl).

#### json
```json
{
  "class": "File",
  "path": "special_file"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/context.jsonld",
  "class": "File",
  "path": "special_file"
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] a <https://example.org/File> ;
    cwl:path <https://example.org/special_file> .


```

## Schema

```yaml
additionalProperties: false
oneOf:
- required:
  - path
- required:
  - location
properties:
  basename:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#basename
  class:
    enum:
    - File
    - Directory
    type: string
    x-jsonld-id: '@type'
  location:
    type: string
    x-jsonld-id: '@id'
  nameroot:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#File/nameroot
  path:
    type: string
    x-jsonld-id: https://w3id.org/cwl/cwl#path
    x-jsonld-type: '@id'
required:
- class
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "basename": "cwl:basename",
    "class": "@type",
    "location": "@id",
    "nameroot": "cwl:File/nameroot",
    "path": {
      "@id": "cwl:path",
      "@type": "@id"
    },
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLDefaultLocation/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLDefaultLocation`

