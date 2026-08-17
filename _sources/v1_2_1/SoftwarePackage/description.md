Each field plays a distinct role:

- `package` — the software's name. If the name alone is ambiguous (common, inconsistent across
  package managers, etc.) it should be paired with one or more identifiers in `specs`.
- `version` — the version(s) of the software known to be compatible with the process.
- `specs` — one or more [ReferenceURL](bblocks://ogc.cwl.v1_2_1.ReferenceURL) IRIs identifying
  resources for installing or enabling the named package. Implementations may resolve these IRIs
  to a concrete install action, or fall back to using just the `package` name on a best-effort
  basis.

For example, the IRI `https://packages.debian.org/bowtie` could be resolved with
`apt-get install bowtie`, while `https://anaconda.org/bioconda/bowtie` could be resolved with
`conda install -c bioconda bowtie`. IRIs can also be system-independent, mapping to a specific
software concept rather than a particular package manager entry.

A `SoftwarePackage` normally appears as an item of
[SoftwareRequirement](bblocks://ogc.cwl.v1_2_1.SoftwareRequirement)'s `packages` property.
