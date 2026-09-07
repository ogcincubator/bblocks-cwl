A CWL `record` is schema-salad's structured type: a set of named `fields`, each with its own
`type`, that together describe a compound value (analogous to a `struct` or an object type).
Records may be declared inline wherever a [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType) is expected —
e.g. as the `type` of a `CommandLineTool` input or output — or given a `name` and referenced from
elsewhere by an IRI (see [type-system/CWLTypeRecordRef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordRef)).

The `fields` themselves — each a [type-system/CWLTypeRecordFieldDef](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordFieldDef) —
can be written in two equivalent forms:

- **Map form**: an object whose keys are the field names and whose values are each field's type
  (either a bare [CWLType](bblocks://ogc.cwl.v1_2_1.CWLType), or a full field definition when
  additional parameters such as `format` or `secondaryFiles` are needed). The field's `name` is
  implied by its key and must not be repeated inside the value.
- **List form**: an array of field definitions, each of which must carry its own `name` property
  since there is no map key to imply it.

Both forms are accepted anywhere a `record`'s `fields` are expected; this block's schema expresses
that as a `oneOf` between the two shapes.
