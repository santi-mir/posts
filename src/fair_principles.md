# FAIR

The FAIR Guiding Principles are suggestions for improving data _reusability_. Also _reproducibility_ and _transparency_. Here the essence of it is described.

## The idea

The paper states:

> [good data management] is the key conduit leading to knowledge discovery and innovation.

We can imagine science as an activity of "solving the puzzle of knowledge together".
Theories, observations, workflows, processing pipelines and algorithms, software and other data are the puzzle pieces. If the piece is (each term only briefly summarised, oversimplified):

- Findable: there is some place to query for it,
- Accessible: the object is explorable, downloadable,
- Interoperable: uses a common format rather than private,
- Reusable: contains permissive usage policies / license such that it can be reused in future research.

### Benefits

Sharing data objects has many benefits:

- _Researchers_ would earn citations through publishing data-objects.
- _Software developers_ can also get recognition for their published data-objects;
- _Peer-researchers_ can then test and reuse the results, while enhancing data-mining and have other areas.

And so forth.

## Sharing and finding data objects

Common repositories used for scientific objects are of two kinds:

- Special-purpose: World Wide Protein Data Bank (wwPDB), NOMAD and Materials Cloud (for materials)
- General-purpose: FigShare, Zenodo, GitHub.

**Importantly**, GitHub does not produce DOIs nor guarantees that the item is preserved (it can easily be deleted).

It's important to either inspect or create (for each case above) labels, description, license and other metadata.

## For humans and machines

Different from other frameworks, FAIR is concerned about how non-human agents and tools would discover, retrieve and be able to use the data.

<!--How to identify which are independent data objects, and where to publish each kind?-->

<!-- Metaphors as graph-learning tools? They help us see and remember relationships between nodes by overlapping graphs. -->

<details>
<summary>Resources</summary>

1. [The FAIR Guiding Principles for scientific data management and stewardship][fair] (2016)
2. [The rise of data repositories in materials chemistry][repositories_and_citations_overview] (2024); and the Supplementary Information. Missing: clarifying which repositories ensure preserving data by policy; comparison between repositories should use the same year for all publications.

</details>

[fair]: https://www.nature.com/articles/sdata201618
[doi_citation_analysis]: https://arxiv.org/pdf/1911.00295
[repositories_and_citations_overview]: https://www.nature.com/articles/s42004-024-01143-0
