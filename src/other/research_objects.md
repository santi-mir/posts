# Research and Data Objects

## FAIR Principles
The FAIR Guiding Principles are suggestions for improving data _reusability_. Also _reproducibility_ and _transparency_. Here the essence of it is described.

### The idea

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

### For humans and machines

Different from other frameworks, FAIR is concerned about how non-human agents and tools would discover, retrieve and be able to use the data.

## Sharing and finding data objects

Common repositories used for scientific objects are of two kinds:

- Special-purpose: World Wide Protein Data Bank (wwPDB), NOMAD and Materials Cloud (for materials)
- General-purpose: FigShare, Zenodo (CERN), GitHub.

**Importantly**, GitHub does not produce DOIs nor guarantees that the item is preserved (it can easily be deleted).

It's important to either inspect or create (for each case above) labels, description, license and other metadata.

## Citing Objects

The recommended practice is to link a dynamic DOI (that tracks versions), especially for software or datasets.

Zenodo handily combines a _concept_ and _version_ DOIs, mapping to the software _project_ and _version_, respectively.

There are two issues, one on each side of the citation problem:

1. Developers are burdened to update the DOI's version, say in the README.
2. Researchers cite a paper DOI rather than dataset / software appears, or simply name the software.

To solve `1.` [a 2019 paper][doi_citation_analysis] analysing citations of Zenodo objects suggests:

> [recommended identifier] ideally represents the whole software project, which is less prone to impermanence. This recommendation does not require maintenance effort on the developer (...)

This is not the "recommended practice" of citing the version as well, but it is a first step. The next step would be to use and update the software DOI version.

### Thoughts on non-paper citations

A clear limitation is that software dependencies don't get any credits, only the top level.

It seems common to also add a citation file format (`file.cff`) to GitHub repos which help when linking repository to Zenodo. Then we must add the Zenodo recommended citation choosing version or concept DOI, as described earlier.

<!--How to identify which are independent data objects, and where to publish each kind?-->

<!-- Metaphors as graph-learning tools? They help us see and remember relationships between nodes by overlapping graphs. -->

<details>
<summary>Resources</summary>

1. [The FAIR Guiding Principles for scientific data management and stewardship][fair] (2016),
2. [The rise of data repositories in materials chemistry][repositories_and_citations_overview] (2024); and the Supplementary Information. Missing: clarifying which repositories ensure preserving data by policy; comparison between repositories should use the same year for all publications,
3. [PRACTICE MEETS PRINCIPLE: TRACKING SOFTWARE AND DATA CITATIONS TO ZENODO DOIs][doi_citation_analysis] (2019).

</details>

[fair]: https://www.nature.com/articles/sdata201618
[doi_citation_analysis]: https://arxiv.org/pdf/1911.00295
[repositories_and_citations_overview]: https://www.nature.com/articles/s42004-024-01143-0
