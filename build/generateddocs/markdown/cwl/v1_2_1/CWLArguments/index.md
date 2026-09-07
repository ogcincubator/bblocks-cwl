
# CWLArguments (Schema)

`ogc.cwl.v1_2_1.CWLArguments` *v1.2.1*

Base arguments passed to the command.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Command line bindings that are not directly associated with an input parameter. Each item is either
a plain string, used verbatim as a literal argument, or an [InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding)
object, which additionally lets an argument declare a `prefix`, a `position`, and a `valueFrom`
expression to compute its value.

Together with any `inputBinding` declared on the tool's inputs, these bindings are sorted by their
numeric `position` (lower values first, default `0`; ties broken by the input's declaration order)
to build the final command line, after the leading elements from
[CWLCommand](bblocks://ogc.cwl.v1_2_1.CWLCommand). When a value needs shell metacharacters or
quoting beyond a plain literal, see [ShellCommandRequirement](bblocks://ogc.cwl.v1_2_1.requirements.ShellCommandRequirement).

## Examples

### Literal string arguments
Arguments given as plain strings are used verbatim, in order, as literal
command line arguments, e.g. invoking `bwa mem` as part of a longer
command line.

#### json
```json
["bwa", "mem"]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/context.jsonld",
  "http://www.w3.org/1999/02/22-rdf-syntax-ns#value": {
    "@list": [
      "bwa",
      "mem"
    ]
  }
}
```

#### ttl
```ttl
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

[] rdf:value ( "bwa" "mem" ) .


```


### Positioned argument with a computed value
An argument expressed as an [InputBinding](bblocks://ogc.cwl.v1_2_1.InputBinding)
object, placing a runtime-computed value (the tool's output directory)
at command line position `2`, after the leading elements from
[CWLCommand](bblocks://ogc.cwl.v1_2_1.CWLCommand) and any lower-position
input bindings.

#### json
```json
[
  {
    "position": 2,
    "valueFrom": "$(runtime.outdir)"
  }
]

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/context.jsonld",
  "@graph": [
    {
      "position": 2,
      "valueFrom": "$(runtime.outdir)"
    }
  ]
}
```

#### ttl
```ttl
@prefix cwl: <https://w3id.org/cwl/cwl#> .
@prefix ns1: <https://w3id.org/cwl/cwl#CommandLineBinding/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

[] ns1:position 2 ;
    cwl:valueFrom "$(runtime.outdir)" .


```

## Schema

```yaml
description: Base arguments passed to the command.
items:
  oneOf:
  - type: string
  - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/InputBinding/schema.yaml
title: CWLArguments
type: array

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "itemSeparator": "cwl:CommandLineBinding/itemSeparator",
    "position": "cwl:CommandLineBinding/position",
    "prefix": "cwl:CommandLineBinding/prefix",
    "shellQuote": "cwl:CommandLineBinding/shellQuote",
    "valueFrom": "cwl:valueFrom",
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLArguments/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLArguments`

