
# CWLTypeSymbols (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeSymbols` *v1.2.1*

The `symbols` list of an `enum` type: the set of allowed
values composing the enum.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Species enum symbols
The `symbols` list of an inline `enum` type restricting an input to two species names, adapted
from the CWL conformance test `anon_enum_inside_array.cwl`.

#### json
```json
["homo_sapiens", "mus_musculus"]

```

## Schema

```yaml
items:
  $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbolValues/schema.yaml
summary: Allowed values composing the enum.
title: CWLTypeSymbols
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbols/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbols/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeSymbols`

