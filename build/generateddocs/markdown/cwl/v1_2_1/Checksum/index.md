
# Checksum (Schema)

`ogc.cwl.v1_2_1.Checksum` *v1.2.1*

An optional hash code for validating file integrity. Currently must be in
the form `sha1$<hexadecimal string>`, using the SHA-1 algorithm.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Minimal pattern check to know which hash algorithm to apply,
but don't check too harshly for the rest (length, allowed characters, etc.).

## Examples

### SHA-1 checksum of a File
The `checksum` field of a `File` object, prefixed with the hash algorithm identifier (`sha1$`)
followed by the hexadecimal SHA-1 digest of the file's contents.

#### json
```json
"sha1$959e6b13ecc44e1af7c94cc76ff6a5eb5b4c6f76"

```

## Schema

```yaml
$comment: 'Minimal pattern check to know which hash algorithm to apply,

  but don''t check too harshly for the rest (length, allowed characters, etc.).

  '
pattern: ^[a-z0-9\-]+\$[\w\-.]+$
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/Checksum/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/Checksum/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/Checksum`

