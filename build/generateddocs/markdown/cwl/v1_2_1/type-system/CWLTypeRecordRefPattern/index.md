
# CWLTypeRecordRefPattern (Schema)

`ogc.cwl.v1_2_1.type-system.CWLTypeRecordRefPattern` *v1.2.1*

The URL/fragment syntax for referencing a named
record type by IRI: an optional URL/local path prefix followed by a `#RecordName` fragment
identifier, resolved per [CWL's identifier resolution rules](https://www.commonwl.org/v1.2/SchemaSalad.html#Identifier_resolution).

[*Status*](http://www.opengis.net/def/status): Under development

## Description

This pattern matches values of the form:

```
[<document-path-or-URL>]#<RecordName>
```

The document part is optional and, when present, may be a bare relative path (e.g.
`schema.yml`), an absolute local path, or a full `http(s)://`/`ftp(s)://` URL. What follows
the `#` is the record's local name (e.g. `HelloType`). A bare `#RecordName` with no document
part is also valid, and resolves relative to the current document.

This is the syntax used to reference a `record` type defined out-of-line — most commonly one
declared in a `SchemaDefRequirement` document (via [`$import`](https://www.commonwl.org/v1.2/SchemaSalad.html#Import))
rather than inlined with [bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema].
[bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef] narrows this pattern further, excluding
the strings that are already reserved as CWL primitive/array type keywords or as the
`stdin`/`stdout`/`stderr` literals, so a plain type reference is never ambiguous with a named
record reference.

## Examples

### Record name with a relative document prefix
A record reference combining a relative document path with a `#RecordName` fragment,
adapted from [schemadef-tool.cwl](https://github.com/common-workflow-language/common-workflow-language/blob/main/v1.2/v1.2/schemadef-tool.cwl).

#### json
```json
"schemadef-type.yml#HelloType"

```


### Bare fragment identifier
A record reference consisting of just the `#RecordName` fragment, with no document
prefix — resolved relative to the current document per CWL's identifier resolution rules.

#### json
```json
"#HelloType"

```

## Schema

```yaml
format: url
pattern: ^(((?:http|ftp)s?:\/\/)?(?!.*\/\/.*$)(?:(?:[A-Za-z0-9](?:[A-Za-z0-9-]{0,61}[A-Za-z0-9])?\.)+(?:[A-Za-z]{2,6}\.?|[A-Za-z0-9-]{2,}\.?)|localhost|\[[a-f0-9:]+\]|\d{1,3}\.\d{1,3}\.\d{1,3}\.\d{1,3})(?::\d+)?(?:\/?|[\/?]\S+))?(?:[A-Za-z0-9\w\-.\/]+)?\#?[A-Za-z0-9\w\-.]+$
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRefPattern/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/type-system/CWLTypeRecordRefPattern/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/type-system/CWLTypeRecordRefPattern`

