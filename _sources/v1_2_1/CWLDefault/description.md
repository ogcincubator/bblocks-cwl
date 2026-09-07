The `default` field of an [`InputParameter`](https://www.commonwl.org/v1.2/Workflow.html#InputParameter)
supplies the value to use for that input when it is missing from the input object, or when its value
is `null`. Default values are applied before evaluating any expressions that depend on the input
(e.g. a dependent `valueFrom` field).

This block enumerates the shapes a `default` value may take:

- a single literal — number, boolean or string (`AnyLiteralType`);
- an array of such literals (`AnyLiteralList`);
- a [`CWLDefaultLocation`](bblocks://ogc.cwl.v1_2_1.CWLDefaultLocation) object — a literal `File` or
  `Directory` identified by `path`/`location` — for File- or Directory-typed inputs;
- an arbitrary JSON object that does *not* declare a `File`/`Directory` `class` (`CWLDefaultObject`),
  covering `record`-typed defaults; or
- an array of such objects.

The `CWLDefaultObject` branch's `not` constraint exists purely to keep it from swallowing what is
actually a `File`/`Directory` default, so that shape is unambiguously matched by
[`CWLDefaultLocation`](bblocks://ogc.cwl.v1_2_1.CWLDefaultLocation) instead. This block does not check
the default's shape against the input's declared `type` — see
[CWLDefaultTypedConditional](bblocks://ogc.cwl.v1_2_1.CWLDefaultTypedConditional) for that.
