
# CWLTypeDefinition (Schema)

`ogc.cwl.v1_2_1.CWLTypeDefinition` *v1.2.1*

Field type definition.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Note that 'Any' is equivalent to any of the non-null types.
Therefore, a nullable 'Any' explicitly specified by 'Any?' or its array-nullable form 'Any[]?' are not equivalent.

## Examples

### File type
A required `File` parameter type.

#### json
```json
"File"

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": "File"
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value "File" .


```


### Optional array of strings
A nullable array of strings, combining the array (`[]`) and nullable (`?`) suffixes.

#### json
```json
"string[]?"

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": "string[]?"
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value "string[]?" .


```

## Schema

```yaml
$comment: 'Note that ''Any'' is equivalent to any of the non-null types.

  Therefore, a nullable ''Any'' explicitly specified by ''Any?'' or its array-nullable
  form ''Any[]?'' are not equivalent.

  '
description: Field type definition.
enum:
- 'null'
- Any
- Any?
- Any[]
- Any[]?
- Directory
- Directory?
- Directory[]
- Directory[]?
- File
- File?
- File[]
- File[]?
- boolean
- boolean?
- boolean[]
- boolean[]?
- double
- double?
- double[]
- double[]?
- enum?
- enum[]
- enum[]?
- float
- float?
- float[]
- float[]?
- int
- int?
- int[]
- int[]?
- integer
- integer?
- integer[]
- integer[]?
- long
- long?
- long[]
- long[]?
- string
- string?
- string[]
- string[]?
summary: CWL type string definition.
title: CWL type string definition
type: string
x-jsonld-extra-terms:
  'null': https://w3id.org/cwl/salad#null
  boolean: http://www.w3.org/2001/XMLSchema#boolean
  int: http://www.w3.org/2001/XMLSchema#int
  integer: http://www.w3.org/2001/XMLSchema#int
  long: http://www.w3.org/2001/XMLSchema#long
  float: http://www.w3.org/2001/XMLSchema#float
  double: http://www.w3.org/2001/XMLSchema#double
  string: http://www.w3.org/2001/XMLSchema#string
  File: https://w3id.org/cwl/cwl#File
  Directory: https://w3id.org/cwl/cwl#Directory
x-jsonld-prefixes:
  sld: https://w3id.org/cwl/salad#
  xsd: http://www.w3.org/2001/XMLSchema#
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "null": "sld:null",
    "boolean": "xsd:boolean",
    "int": "xsd:int",
    "integer": "xsd:int",
    "long": "xsd:long",
    "float": "xsd:float",
    "double": "xsd:double",
    "string": "xsd:string",
    "File": "cwl:File",
    "Directory": "cwl:Directory",
    "sld": "https://w3id.org/cwl/salad#",
    "xsd": "http://www.w3.org/2001/XMLSchema#",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLTypeDefinition/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLTypeDefinition`

