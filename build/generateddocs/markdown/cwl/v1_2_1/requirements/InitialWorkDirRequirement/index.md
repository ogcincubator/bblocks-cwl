
# InitialWorkDirRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.InitialWorkDirRequirement` *v1.2.1*

Defines a list of files and subdirectories that must be
staged by the workflow platform prior to executing the command line tool, normally within the
designated output directory (though containers may stage them elsewhere).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Define a list of files and subdirectories that must be staged by the workflow platform prior to
executing the command line tool. Normally files are staged within the designated output directory;
however, when running inside containers, files may be staged at arbitrary locations (see
`entryname` below). Together with `DockerRequirement.dockerOutputDirectory` this makes it possible to
control the locations of both input and output files when running in containers.

`listing` may be a single [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) that evaluates to
the whole list, or an array whose items are each one of: `null` (no effect), a `CWLExpression`, a
`Dirent` (called `DirectoryListingDirent` in this schema), a `File`/`Directory` object
(`DirectoryListingFileOrDirectory`), or an array of `File`/`Directory` objects.

The return type of each expression item must itself validate as `["null", File, Directory, Dirent,
{type: array, items: [File, Directory]}]`:

- A `File` or `Directory` returned by an expression is added to the designated output directory
  before the tool runs.
- A `Dirent` (listed directly or returned by an expression) specifies a file to create or stage in the
  designated output directory before the tool runs. Its `entry` may be a string literal (staged as
  the text content of a new file), an expression evaluating to a `File`/`Directory` object or array of
  such objects (staged as-is), or an expression evaluating to `null` (no effect) or to some other
  JSON value, which is serialized to JSON text and staged as file content.
- `entryname` gives the staged file or subdirectory its target name, overriding the `basename` of a
  `File`/`Directory` `entry`. It is required when `entry` evaluates to file contents only, optional
  when `entry` evaluates to a `File`/`Directory` object with a `basename`, and invalid when `entry`
  evaluates to an array of `File`/`Directory` objects. A relative `entryname` names a location inside
  the designated output directory (one starting with `../`, or resolving above it, is an error); an
  absolute `entryname` is only valid when `DockerRequirement` is in effect and the tool runs inside a
  container with its own root filesystem, in which case it names an absolute path inside the
  container.
- `writable` (default `false`) marks the staged `File`/`Directory` as writable by the tool, isolated
  from any other running process; a writable `Directory` implies all of its contents are writable too.
  Files not marked writable may be made available via bind mount or filesystem link rather than
  copied. Disruptive in-place changes are otherwise disallowed unless
  [InplaceUpdateRequirement](bblocks://ogc.cwl.v1_2_1.requirements.InplaceUpdateRequirement)'s `inplaceUpdate` is
  `true`.

`File`/`Directory` inputs that also appear in the `listing` have their `path` updated to their staged
location; if the same `File`/`Directory` appears more than once in the listing, the implementation may
choose any single value for `path`.

See also: the [CWL v1.2 CommandLineTool spec — InitialWorkDirRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#InitialWorkDirRequirement).

## Examples

### Stage a generated configuration file
A single `Dirent` entry that creates `example.conf` in the designated output directory before
the tool runs, with contents built from an input parameter via a
[CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression).

#### json
```json
{
  "class": "InitialWorkDirRequirement",
  "listing": [
    {
      "entryname": "example.conf",
      "entry": "CONFIGVAR=$(inputs.message)\n"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/context.jsonld",
  "class": "InitialWorkDirRequirement",
  "listing": [
    {
      "entryname": "example.conf",
      "entry": "CONFIGVAR=$(inputs.message)\n"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .

[] a <https://example.org/InitialWorkDirRequirement> ;
    cwl:listing [ ] .


```


### Stage an input file under a new name, writable
A `Dirent` that stages an input `File` under a new `entryname`, marked `writable` so the tool
may modify it in place, alongside a plain `File` object staged as-is.

#### json
```json
{
  "class": "InitialWorkDirRequirement",
  "listing": [
    {
      "entry": "$(inputs.infile)",
      "entryname": "bob.txt",
      "writable": true
    },
    {
      "class": "File",
      "location": "https://example.org/data/reference.txt"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/context.jsonld",
  "class": "InitialWorkDirRequirement",
  "listing": [
    {
      "entry": "$(inputs.infile)",
      "entryname": "bob.txt",
      "writable": true
    },
    {
      "class": "File",
      "location": "https://example.org/data/reference.txt"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#Dirent/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/InitialWorkDirRequirement> ;
    cwl:listing [ a <https://example.org/File> ],
        [ ns1:writable true ] .


```

## Schema

```yaml
$defs:
  InitialWorkDirListing:
    oneOf:
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    - items:
        oneOf:
        - type: 'null'
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
        - $ref: '#/$defs/DirectoryListingDirent'
        - $ref: '#/$defs/DirectoryListingFileOrDirectory'
        - items:
            $ref: '#/$defs/DirectoryListingFileOrDirectory'
          type: array
      title: InitialWorkDirListingItems
      type: array
    title: InitialWorkDirListing
  DirectoryListingDirent:
    $comment: Called 'Dirent' in documentation.
    additionalProperties: false
    properties:
      entry:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      entryname:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
      writable:
        type: boolean
        x-jsonld-id: https://w3id.org/cwl/cwl#Dirent/writable
    required:
    - entry
    title: DirectoryListingDirent
    type: object
  DirectoryListingFileOrDirectory:
    additionalProperties: false
    properties:
      checksum:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/Checksum/schema.yaml
        x-jsonld-id: https://w3id.org/cwl/cwl#File/checksum
      class:
        enum:
        - File
        - Directory
        type: string
        x-jsonld-id: '@type'
      location:
        type: string
      size:
        minimum: 0
        type: integer
        x-jsonld-id: https://w3id.org/cwl/cwl#File/size
    required:
    - class
    - location
    type: object
additionalProperties: false
properties:
  class:
    enum:
    - InitialWorkDirRequirement
    type: string
    x-jsonld-id: '@type'
  listing:
    $ref: '#/$defs/InitialWorkDirListing'
    x-jsonld-id: https://w3id.org/cwl/cwl#listing
required:
- listing
title: InitialWorkDirRequirement
type: object
x-jsonld-extra-terms:
  writable: https://w3id.org/cwl/cwl#Dirent/writable
  checksum: https://w3id.org/cwl/cwl#File/checksum
  size: https://w3id.org/cwl/cwl#File/size
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
    "class": "@type",
    "listing": "cwl:listing",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/InitialWorkDirRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/InitialWorkDirRequirement`

