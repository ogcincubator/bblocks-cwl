
# CWLTextPatternID (Schema)

`ogc.cwl.v1_2_1.CWLTextPatternID` *v1.2.1*

Generic identifier name pattern.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Identifier with text pattern that can allow additional non-ASCII characters depending on regex implementation.
The identifier allows a '#' or a relative 'sub/part#ref' prefix, to support references to other definitions
in the CWL document, such as when using 'SchemaDefRequirement'.

JSON spec regex does not include '\w' in its default subset to allow all word-like unicode characters
(see reference: https://json-schema.org/understanding-json-schema/reference/regular_expressions.html).

Since support is implementation specific, add both the ASCII-only and '\w' representation simultaneously
and let the parser reading this document apply whichever is more relevant or supported
(see discussion: https://github.com/common-workflow-language/cwl-v1.2/pull/256#discussion_r1234037814).

## Examples

### Local fragment identifier
A short local identifier, as used for an `id` field within a single (non-packed) CWL document.

#### json
```json
"main"

```


### Fragment reference into a sub-part
An identifier referencing a sub-part definition through a `#` fragment prefix, such as an entry
defined under `SchemaDefRequirement`.

#### json
```json
"sub/part#ref"

```

## Schema

```yaml
$comment: 'Identifier with text pattern that can allow additional non-ASCII characters
  depending on regex implementation.

  The identifier allows a ''#'' or a relative ''sub/part#ref'' prefix, to support
  references to other definitions

  in the CWL document, such as when using ''SchemaDefRequirement''.


  JSON spec regex does not include ''\w'' in its default subset to allow all word-like
  unicode characters

  (see reference: https://json-schema.org/understanding-json-schema/reference/regular_expressions.html).


  Since support is implementation specific, add both the ASCII-only and ''\w'' representation
  simultaneously

  and let the parser reading this document apply whichever is more relevant or supported

  (see discussion: https://github.com/common-workflow-language/cwl-v1.2/pull/256#discussion_r1234037814).

  '
description: Generic identifier name pattern.
pattern: ^([A-Za-z0-9\w]+(/[A-Za-z0-9\w]+)*)?[#.]?[A-Za-z0-9\w]+(?:[-_.][A-Za-z0-9\w]+)*$
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTextPatternID/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLTextPatternID`

