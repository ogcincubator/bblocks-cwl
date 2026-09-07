
# LinkMergeMethod (Schema)

`ogc.cwl.v1_2_1.LinkMergeMethod` *v1.2.1*

How multiple inbound data links into the same Workflow step input
are combined: `merge_nested` (default; wraps each source's value, producing a list with one entry
per link) or `merge_flattened` (concatenates/appends array-valued sources into a single flat list).

[*Status*](http://www.opengis.net/def/status): Under development

## Examples

### Flattening two sources into one list
A `WorkflowStepInput` receives values from two upstream sources (`file1` and `file2`). Because
both sources produce array values, `merge_flattened` concatenates them into a single flat list
instead of nesting one entry per source.

#### json
```json
"merge_flattened"

```


### Wrapping a single source in a list
A `WorkflowStepInput` with a single source still produces a list when `merge_nested` is used
(the default), wrapping that one source's value as the sole entry.

#### json
```json
"merge_nested"

```

## Schema

```yaml
enum:
- merge_nested
- merge_flattened
type: string

```

Links to the schema:

* YAML version: [schema.yaml](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LinkMergeMethod/schema.json)
* JSON version: [schema.json](https://ogcincubator.github.io/bblocks-cwl/build/annotated/cwl/v1_2_1/LinkMergeMethod/schema.yaml)


# For developers

The source code for this Building Block can be found in the following repository:

* URL: [https://github.com/ogcincubator/bblocks-cwl](https://github.com/ogcincubator/bblocks-cwl)
* Path: `_sources/v1_2_1/LinkMergeMethod`

