
# CWLTypeSymbolValues (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeSymbolValues` *v1.2.1*

A single allowed value of an `enum` type's
`symbols` list: a string or number literal.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### String symbol value
A `symbols` entry given as a plain string, the common case for CWL `enum` types (e.g. species
names in a workflow input).

#### json
```json
"homo_sapiens"

```


### Numeric symbol value
Schema-salad also allows `symbols` entries to be numeric literals.

#### json
```json
42

```

## Schema

```yaml
oneOf:
- type: number
- type: string
title: CWLTypeSymbolValues

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbolValues/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeSymbolValues/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeSymbolValues`

