
# NetworkAccessRequirement (Schema)

`ogc.cwl.v1_2_1.NetworkAccessRequirement` *v1.2.1*

NetworkAccessRequirement

[*Status*](http://www.opengis.net/def/status): Under development

## Schema

```yaml
additionalProperties: false
properties:
  class:
    $comment: Not 'NetworkAccessRequirement'
    enum:
    - NetworkAccess
    type: string
  networkAccess:
    description: Indicate whether a process requires outgoing IPv4/IPv6 network access.
    example: true
    oneOf:
    - type: boolean
    - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
    title: NetworkAccess
    x-jsonld-id: https://w3id.org/cwl/cwl#NetworkAccess/networkAccess
required:
- networkAccess
title: NetworkAccessRequirement
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/NetworkAccessRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/NetworkAccessRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "networkAccess": "cwl:NetworkAccess/networkAccess",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/NetworkAccessRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/NetworkAccessRequirement`

