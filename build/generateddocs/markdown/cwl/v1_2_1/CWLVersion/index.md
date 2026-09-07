
# CWLVersion (Schema)

`ogc.cwl.v1_2_1.CWLVersion` *v1.2.1*

The `cwlVersion` field: declares which published version of the CWL
standard a document conforms to. Required once at the root of every CWL document.

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### CWL v1.2 document
The `cwlVersion` field as it appears at the root of a CWL v1.2 document, adapted from the CWL
conformance test `count-lines7-wf.cwl`.

#### json
```json
{
  "cwlVersion": "v1.2"
}

```


### CWL v1.0 document
A document declaring conformance to an earlier published CWL standard version.

#### json
```json
{
  "cwlVersion": "v1.0"
}

```

## Schema

```yaml
properties:
  cwlVersion:
    description: CWL version of the described application package.
    pattern: ^v\d+(\.\d+(\.\d+)*)*$
    title: cwlVersion
    type: string
required:
- cwlVersion
type: object

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLVersion/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/CWLVersion/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/CWLVersion`

