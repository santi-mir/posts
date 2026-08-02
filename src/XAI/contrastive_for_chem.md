# XAI4Chem: Contrastive explanations

Previous posts have discussed [explanations] and [model explainability].

One area of interest, both in academia and the pharmaceutical industries, is the explainability of neural networks predicting structures or properties.

Here is an example, from the paper "[Enhancing preclinical drug discovery with artificial intelligence][ai4dd]" (the references were edited out, and can be found in the original article):

> (...) many successful applications of QSAR-based VS workflows for hit identification have been reported. Zhang et al. described the successful implementation of an ML-based QSAR workflow for VS that led to the discovery of novel antimalarial agents.

The ML algorithms were trained on a small dataset of antimalarial drugs. The authors continue:

> The QSAR models were used to carry out VS against the ChemBridge database and resulted in the selection of 174 compounds for a follow-up screening in Plasmodium falciparum growth inhibition and cellular assays. Experimental validation revealed 25 of the selected compounds to be active, yielding a hit rate of 14.2%, with the most potent hit having an EC50 value of 95.6 nM. Subsequently, many studies have reported the application of ML and DL-based QSAR workflows as promising VS tools.

That sound cool and useful. A human expert may be able to detect a pattern on those structures.

- But can we figure out an evaluation mechanism that singles out which fragments are most important?

- At the same time, isolated fragments may be misleading, because the shape of the molecule is also as important. Maybe a "fragments vs shape" could make up a directionally useful plot?

## Paper Idea

Feature Attribution Methods, such as SHAP and LIME help answer the question "_Why was P obtained?_".

On the other hand, contrastive explanations answer the question "_Why P rather than Q_?".

Here, "Q" is the _foil_ (an alternative event), and it's an important tool to make explanations simpler: the aspects that are similar do not need to be explained, it is the differences that count towards explaining "Why P rather than Q".

The paper "[Contrastive explanations for machine learning predictions in chemistry][xai4chem]" (2025) develops a framework called MolCE for:

> deriving contrastive explanations for machine learning models in chemistry to systematically generate intuitive explanations of predictions in high-dimensional feature spaces.

<details>
<summary>Sources</summary>

1. [xai4chem][Contrastive explanations for machine learning predictions in chemistry]

</details>

[ai4dd]: https://www.sciencedirect.com/science/article/pii/S1359644621005043
[xai4chem]: https://jcheminf.biomedcentral.com/articles/10.1186/s13321-025-01100-6
[explanations]: ./explanation.md
[model explainability]: ./model_explainability.md
