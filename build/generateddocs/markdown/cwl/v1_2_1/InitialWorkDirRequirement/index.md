
# InitialWorkDirRequirement (Schema)

`ogc.cwl.v1_2_1.InitialWorkDirRequirement` *v1.2.1*

InitialWorkDirRequirement

[*Status*](http://www.opengis.net/def/status): Under development

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
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/DirectoryListingDirent/schema.yaml
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/DirectoryListingFileOrDirectory/schema.yaml
        - items:
            $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/DirectoryListingFileOrDirectory/schema.yaml
          type: array
      title: InitialWorkDirListingItems
      type: array
    title: InitialWorkDirListing
additionalProperties: false
properties:
  class:
    enum:
    - InitialWorkDirRequirement
    type: string
  listing:
    $ref: '#/$defs/InitialWorkDirListing'
required:
- listing
title: InitialWorkDirRequirement
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InitialWorkDirRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InitialWorkDirRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "writable": "cwl:Dirent/writable",
    "checksum": "cwl:File/checksum",
    "size": "cwl:File/size",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InitialWorkDirRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/InitialWorkDirRequirement`

