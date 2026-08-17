Define a list of files and subdirectories that must be staged by the workflow platform prior to
executing the command line tool. Normally files are staged within the designated output directory;
however, when running inside containers, files may be staged at arbitrary locations (see
`entryname` below). Together with `DockerRequirement.dockerOutputDirectory` this makes it possible to
control the locations of both input and output files when running in containers.

`listing` may be a single [CWLExpression](bblocks://ogc.cwl.v1_2_1.CWLExpression) that evaluates to
the whole list, or an array whose items are each one of: `null` (no effect), a `CWLExpression`, a
`Dirent` (called `DirectoryListingDirent` in this schema), a `File`/`Directory` object
(`DirectoryListingFileOrDirectory`), or an array of `File`/`Directory` objects.

The return type of each expression item must itself validate as `["null", File, Directory, Dirent,
{type: array, items: [File, Directory]}]`:

- A `File` or `Directory` returned by an expression is added to the designated output directory
  before the tool runs.
- A `Dirent` (listed directly or returned by an expression) specifies a file to create or stage in the
  designated output directory before the tool runs. Its `entry` may be a string literal (staged as
  the text content of a new file), an expression evaluating to a `File`/`Directory` object or array of
  such objects (staged as-is), or an expression evaluating to `null` (no effect) or to some other
  JSON value, which is serialized to JSON text and staged as file content.
- `entryname` gives the staged file or subdirectory its target name, overriding the `basename` of a
  `File`/`Directory` `entry`. It is required when `entry` evaluates to file contents only, optional
  when `entry` evaluates to a `File`/`Directory` object with a `basename`, and invalid when `entry`
  evaluates to an array of `File`/`Directory` objects. A relative `entryname` names a location inside
  the designated output directory (one starting with `../`, or resolving above it, is an error); an
  absolute `entryname` is only valid when `DockerRequirement` is in effect and the tool runs inside a
  container with its own root filesystem, in which case it names an absolute path inside the
  container.
- `writable` (default `false`) marks the staged `File`/`Directory` as writable by the tool, isolated
  from any other running process; a writable `Directory` implies all of its contents are writable too.
  Files not marked writable may be made available via bind mount or filesystem link rather than
  copied. Disruptive in-place changes are otherwise disallowed unless
  [InplaceUpdateRequirement](bblocks://ogc.cwl.v1_2_1.InplaceUpdateRequirement)'s `inplaceUpdate` is
  `true`.

`File`/`Directory` inputs that also appear in the `listing` have their `path` updated to their staged
location; if the same `File`/`Directory` appears more than once in the listing, the implementation may
choose any single value for `path`.

See also: the [CWL v1.2 CommandLineTool spec — InitialWorkDirRequirement](https://www.commonwl.org/v1.2/CommandLineTool.html#InitialWorkDirRequirement).
