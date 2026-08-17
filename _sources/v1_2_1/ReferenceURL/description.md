This block profiles the generic [`ogc.ogc-utils.iri-or-curie`](bblocks://ogc.ogc-utils.iri-or-curie)
block, adding the `format`/`pattern` constraints from the upstream CWL schema that narrow an
otherwise-generic IRI/CURIE string down to something that actually looks like a resolvable web
address: an optional `http`, `https`, or `ftp`(`s`) scheme followed by a host (domain name,
`localhost`, IPv4, or bracketed IPv6 literal), an optional port, and an optional path/query.

It is used wherever the upstream CWL schema points to external resources rather than in-document
identifiers — for example the `specs` array of [SoftwarePackage](bblocks://ogc.cwl.v1_2_1.SoftwarePackage),
which lists URLs identifying a piece of software in package repositories such as
[Anaconda.org](https://anaconda.org) or [Debian packages](https://packages.debian.org).
