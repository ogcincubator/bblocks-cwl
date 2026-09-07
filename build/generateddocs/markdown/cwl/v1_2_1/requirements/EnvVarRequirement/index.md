
# EnvVarRequirement (Schema)

`ogc.cwl.v1_2_1.requirements.EnvVarRequirement` *v1.2.1*

Defines a list of environment variables to set in the tool's
execution environment.

[*Status*](http://www.opengis.net/def/status): Under development

## Description

Define a list of environment variables which will be set in the execution environment of the tool.
Each entry is an [`EnvironmentDef`](#EnvironmentDef): an `envName` (the variable name) paired with an
`envValue`, which may be a literal string or a [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression)
evaluated at runtime — for example, to forward the value of an input parameter, or the result of
executing an expression such as building a configuration value from a template. Expression evaluation
requires `InlineJavascriptRequirement` to also be in effect.

`envDef` accepts two equivalent representations:

- An array of `EnvironmentDef` objects, each with explicit `envName`/`envValue` properties.
- A mapping of `envName` to `envValue` (either the value directly, or a nested `EnvironmentDef`-like
  object) — a shorthand JSON-LD map form of the same data.

## Interaction with other requirements

If `EnvVarRequirement` is specified alongside a
[DockerRequirement](bblocks://ogc.cwl.v1_2_1.requirements.DockerRequirement), the environment variables must be
provided to Docker using `--env` or `--env-file`, and interact with the container's preexisting
environment as defined by Docker.

See also: the [CWL v1.2 CommandLineTool spec — EnvVarRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#EnvVarRequirement).

## Examples

### Environment variable set from an input parameter
A single environment variable, `TEST_ENV`, whose value is a
[CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) that forwards an input parameter, using
the shorthand mapping form of `envDef` (`envName` -> `envValue`).

#### json
```json
{
  "class": "EnvVarRequirement",
  "envDef": {
    "TEST_ENV": "$(inputs.in)"
  }
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/context.jsonld",
  "class": "EnvVarRequirement",
  "envDef": {
    "TEST_ENV": "$(inputs.in)"
  }
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#EnvVarRequirement/> .

[] a <https://example.org/EnvVarRequirement> ;
    ns1:envDef "$(inputs.in)" .


```


### Multiple environment variables as an explicit array
Two environment variables declared as an array of `EnvironmentDef` objects, mixing a literal
value and an expression-derived value.

#### json
```json
{
  "class": "EnvVarRequirement",
  "envDef": [
    {
      "envName": "LC_ALL",
      "envValue": "en_US.UTF-8"
    },
    {
      "envName": "DATA_DIR",
      "envValue": "$(inputs.data_dir.path)"
    }
  ]
}

```

#### jsonld
```jsonld
{
  "@context": "https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/context.jsonld",
  "class": "EnvVarRequirement",
  "envDef": [
    {
      "envName": "LC_ALL",
      "envValue": "en_US.UTF-8"
    },
    {
      "envName": "DATA_DIR",
      "envValue": "$(inputs.data_dir.path)"
    }
  ]
}
```

#### ttl
```ttl
@prefix ns1: <https://w3id.org/cwl/cwl#EnvironmentDef/> .
@prefix ns2: <https://w3id.org/cwl/cwl#EnvVarRequirement/> .

[] a <https://example.org/EnvVarRequirement> ;
    ns2:envDef [ ns1:envName "DATA_DIR" ;
            ns1:envValue "$(inputs.data_dir.path)" ],
        [ ns1:envName "LC_ALL" ;
            ns1:envValue "en_US.UTF-8" ] .


```

## Schema

```yaml
$defs:
  EnvironmentDef:
    additionalProperties: false
    properties:
      envName:
        minLength: 1
        type: string
        x-jsonld-id: https://w3id.org/cwl/cwl#EnvironmentDef/envName
      envValue:
        $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
        x-jsonld-id: https://w3id.org/cwl/cwl#EnvironmentDef/envValue
    required:
    - envName
    - envValue
    type: object
additionalProperties: false
properties:
  class:
    enum:
    - EnvVarRequirement
    type: string
    x-jsonld-id: '@type'
  envDef:
    oneOf:
    - items:
        $ref: '#/$defs/EnvironmentDef'
      type: array
    - additionalProperties:
        oneOf:
        - $ref: https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLExpression/schema.yaml
          description: The 'envValue' specified directly
        - $ref: '#/$defs/EnvironmentDef'
      description: Mapping of 'envName' to environment value or definition.
      type: object
    x-jsonld-id: https://w3id.org/cwl/cwl#EnvVarRequirement/envDef
    x-jsonld-container: '@id'
required:
- envDef
type: object
x-jsonld-prefixes:
  cwl: https://w3id.org/cwl/cwl#

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/schema.yaml)


# JSON-LD Context

```jsonld
{
  "@context": {
    "class": "@type",
    "envDef": {
      "@context": {
        "envName": "cwl:EnvironmentDef/envName",
        "envValue": "cwl:EnvironmentDef/envValue"
      },
      "@id": "cwl:EnvVarRequirement/envDef",
      "@container": "@id"
    },
    "cwl": "https://w3id.org/cwl/cwl#",
    "@version": 1.1
  }
}
```

You can find the full JSON-LD context here:
[context.jsonld](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/requirements/EnvVarRequirement/context.jsonld)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/requirements/EnvVarRequirement`

