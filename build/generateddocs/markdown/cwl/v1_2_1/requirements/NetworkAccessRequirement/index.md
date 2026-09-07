
# NetworkAccessRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.NetworkAccessRequirement` *v1.2.1*

`cwltool` extension hint/requirement indicating whether a
process needs outgoing network access. If not specified or false, tools must not assume network
access beyond localhost; if true, the tool may make outgoing connections, though implementations may
still apply their own security policies. Does not imply a publicly routable address or inbound
connections.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Tool requiring outgoing network access
A `CommandLineTool` that downloads a resource over HTTP needs to declare that it requires
outgoing network access, since implementations must otherwise assume the tool is isolated from
the network except for `localhost`.

#### json
```json
{
  "class": "NetworkAccess",
  "networkAccess": true
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/context.jsonld",
  "class": "NetworkAccess",
  "networkAccess": true
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#NetworkAccess/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] a <https://example.org/NetworkAccess> ;
    ns1:networkAccess true .


```


### Network access conditional on a runtime expression
`networkAccess` may also be given as a CWL expression (requires
`InlineJavascriptRequirement`), letting the requirement depend on an input parameter rather
than being hard-coded.

#### json
```json
{
  "class": "NetworkAccess",
  "networkAccess": "$(inputs.allow_network)"
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/context.jsonld",
  "class": "NetworkAccess",
  "networkAccess": "$(inputs.allow_network)"
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#NetworkAccess/> .

[] a <https://example.org/NetworkAccess> ;
    ns1:networkAccess "$(inputs.allow_network)" .


```

## Schema

```yaml
additionalProperties: false
properties:
  class:
    $comment: Not 'NetworkAccessRequirement'
    enum:
    - NetworkAccess
    type: string
    x-jsonld-id: '@type'
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

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "networkAccess": "cwl:NetworkAccess/networkAccess",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/NetworkAccessRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/NetworkAccessRequirement`

