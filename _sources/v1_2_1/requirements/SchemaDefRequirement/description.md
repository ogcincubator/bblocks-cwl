Type definitions may only use the `enum` and `record` forms — see
[type-system/CWLTypeEnum](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeEnum) and
[type-system/CWLTypeRecordSchema](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordSchema) — or an
array whose `items` resolve to one of those, via
[type-system/CWLTypeRecordArray](bblocks://ogc.cwl.v1_2_1.type-system.CWLTypeRecordArray). Each entry
may instead be an [CWLImport](bblocks://ogc.cwl.v1_2_1.CWLImport) (`$import`) directive, so a set of
shared type definitions can be kept in a separate file and reused across multiple CWL documents rather
than repeated inline.

Once declared here, a definition can be referenced by IRI from an `inputs`/`outputs` `type` field
elsewhere in the document, instead of being written out inline at the point of use.
