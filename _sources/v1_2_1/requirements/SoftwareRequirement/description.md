The `packages` property lists the software the process's execution environment must provide. It
accepts two equivalent shapes:

- an array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage) objects, each naming a
  package and optionally its compatible version(s) and identifying IRIs; or
- an object mapping each package name directly to either its `specs`/`version` list (a bare array
  of strings) or a full [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage) object.

The two forms carry the same information: in the map form, the object key stands in for the
package's `package` field, so it does not need to be repeated inside the value.

Implementations are not required to enforce that the requested software is actually present in the
execution environment; `SoftwareRequirement` only records what versions and packages are known to
be usable, leaving actual configuration/resolution up to the runtime.
