# Additive Feature Attribution Methods

This post explores the "Additive Feature Attribution Methods" class of extrinsic explainability methods, where the reference model interals aren't analysed. There is less emphasis on audiences or technicalities about explanations.

---------

Additive Feature Attribution methods are linear approximations ($g$) to the original model ($f$). Mathematically:

$$f(x) \approx g(z) = \phi_0 + \sum_{i=1} \phi_i z_i$$

$\phi_i$s are the effect of each _binary_ feature $z_i$ in the output. Clarifications:

1. Two complex models $f_1$, $f_2$ trained with same data likely have different coefficients for each approximation model ($\phi_i$s),
1. Methods don't protect from a biased model.

_Note_: these could be called linear combination of binary features as well.

## Best coefficients?

Existing additive feature methods (e.g. SHAP, LIME) calculate $\phi_i$s differently, in turn yielding different coefficients. But...which one obtains the _best_ coefficients $\phi_i$? A definition of _best_ is needed.

The [Unified Approach to Interpret Model Predictions][unified_approach_lcobf] proposes that models should have _local accuracy_, _missingness_, _consistency_. With these requirements, they show that Shapley values are the best coefficients. Other methods violate some of these 3 properties.

The authors argue these properties lead to coefficients that are more intuitive for humans.

## Method: SHAP

SHAP stands for SHapley Additive exPlanations, it is considered a feature attribution method rather than a simplification method. The [Principles and practice of explaining ML][principles_and_practice] states:

> The objective in this case is to build a linear model around the instance to be explained, and then interpret each features' coefficient as the features' importance. This idea is similar to LIME, in fact LIME and SHAP are closely related, but SHAP comes with a set of nice theoretical properties.

The exact Shapley values $\phi_i$ result from an expensive combinatorial (see sources at the end). Approximations to the exact formula can be made, with extra assumptions, which **may not hold**:

Assumption 1: Feature independence (implies non-multicollinearity).

- Shapley sampling values method,
- Quantitative Input Influence,
- Plus assumption 2, model linearity: Kernel SHAP (LIME + Shapley values)

Assumption 2, model linearity: Shapley regression values.

SHAP provides both global (average across inputs) and local (for a given input).

## LIME and SP-LIME

The paper ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] proposes the Local Interpretable Model-Agnostic eXplanation (LIME) and the Submodule Picking LIME.

LIME isn't a particular model. It's more like a framework or general idea of the desired charteristics that explainable methods should have (more on this later).

Let's first look at LIME as implemented in a concrete case.

### A concrete example

This is in line with LIME's approach.

A linear model with few-ish, interpretable features, locally fit to a complex one is in line with LIMEs' requirements.

Local fit means fitting only in the vicinity of the input of interest.The input features may differ from those in the original model.

Why would this be useful?

The [original paper][lime] shows an example comparing two different models that were fit by linear ones:

<div class="center w60">
    <a href="../assets/LIME.png">
    <img src="../assets/LIME.png" alt="Comparison between to algorithms analysed by LIME."/>
    </a>
    <p>Image taken from <a href="https://dl.acm.org/doi/10.1145/2939672.2939778">paper</a>.</p>
</div>

As long as the fit is faithful, the value of this simplification is:

- The interpretable features, alongside their contributions (weights) to the prediction, can help decide whether to trust the prediction or not.
- Comparing models is easy (through the linear proxies). It's especially useful if the original models' accuracy (and other metrics) are similar, and their features non-interpretable.
- Here, one of them is untrustworhy (right hand side), giving high weight to meaningless features.

### Explanation Model Desiderata

The authors consider 4 properties to be desirable in an explanation model:

- _Local_: the interpretable or explanation model approximates the original model in the vicinity of a particular prediction. In contrast, _global_ explanations explain the full model.
- _Model-agnostic_: any model can in principle be explained by this method.
- _Interpretable Explanation_: In this paper, "interpretable" is a desired characteristic of "explanation", and provides qualititative understanding (a simple answer to "Why was this prediction made?"). In their own words:
  > An essential criterion for explanations is that they must be **interpretable**, i.e., provide qualitative understanding between the input variables and the response. We note that interpretability must take into account the user's limitations.

Additionally, they include `4.` A global perspective, a mechanism to get a sense of the full model's behaviour.

The first 3 can be achieved using LIME. The fourth, using the Submodule Picking LIME (SP-LIME), which selects LIME explanations to give a global explanation of the model.

### LIME: General Framework

LIME is a slightly more constrained version of the first 3 desired properties. They consider some input representations, some explanation models, and a sampling procedure to train it (not related to SP-LIME).

- Which specific representations does the [LIME][lime] framework consider interpretable?

  An example of an _interpretable representation_ is a binary vector with components indicating presence / absence of a feature (e.g. a word) in the explanation model.

- Which models does the [LIME][lime] paper consider interpretable?

  > (...) interpretable models, such as linear models, decision trees, or falling rule lists [27], i.e. a model $g \in G$ can be readily presented to the user with visual or textual artifacts.

- Complexity is the opposite of interpretable, so the loss (we skip it here) to train the explainable model accounts for it, and also weighs local samples more than remote ones. Here $G$ being the model class of $g$:

  > As not every $g \in G$ may be simple enough to be interpretable thus we let $\Omega(g)$ be a measure of complexity (as opposed to interpretability) of the explanation $g \in G$.

  The definition of complexity depends on $G$. For linear models it may be the number of weights.

They also define a sampling procedure to create the training set. This is detailed in the concrete algorithm in the next section.

### LIME: An Algorithm

The paper implements LIME using the class $G$ of sparse linear models as explanation model. Here is my interpretation of the algorithm (the primed variables denote binary vectors):

1. A model $f$ and an input vector $x \in R^n$ needs explaining,
2. Start an interpretable, binary vector $x' \in \{0,1\}^{n'}$ with only the dimensions of interest of $x$ (it may be all-ones often),
3. Generate perturbed binary variants of $x'$ called $z'_i$,
4. Use $z'$ to make variants of $x$ called $z \in R^n$,
5. Now we have training tuples $(f(z), z', \pi_{x} (z))$.
6. Use the dataset to fit the linear model $g$ using $K-LASSO$.
    - To select $K$ interpretable features they apply $K$-LASSO.
    - LASSO is like a sparse linear regression, some coefficients are pushed to 0 and correspond to variables we can ignore. How many are are pushed to $0$ may be controlled by the complexity penalty in the loss function.
    - This is why the number of input features for the interpretable model ($x'$, $z'$) may be much smaller than that of $x$, $z$.
    - Then the non-zero variables are used to fit $g$ to $f$ but now using least-squares.

SP-LIME is defined as:

> [SP-LIME] a global understanding of the model by explaining a set of individual instances.

The complex part of SP-LIME is selecting instances that add the maximum insight, and avoiding repeated ones. The algorithm is briefly described later on.

### SP-LIME: The Algorithm

The goal here is picking the most informative instances, and without repetition.

A _coverage_ metric is defined: $c(V, W, I) = \sum_j \mathbb{1}_[\exists i \in V:W_{ij}\gt 0] I_j$.

Here, $W$ is a matrix of weights (columns) for each instance (row).

$I$ is the _global importance_ of a component, defined as $I_j = \sqrt{\sum_{i} W_{ij}}$. The larger the sum of weights is, the more important.

A marginal coverage for each candidate instance ($i$) $c_{i} - c$ is performed, then the instance that increases $c$ of $V$ the most is appended to it.

> [!NOTE]
> This approximates the $V$ with the largest coverage, but it's not exact because the total max could be one that does not max it on each step!

To increase the coverage at all, it must add some non-zero value to a column of zeros.

### LIME: Final Comments

Explanation models do not replace but complement accuracy or other evaluation metrics.

<!-- The input representation must also be conceptually meaningful. -->

## Fixes

- Normalised Moving Rate (NMR): tests the stability of the list against the collinearity. Smaller NMR means more stable ordering.
- Modified Index Position, in the [paper's words][using_shap_lime]:
  > [MIP] works similarly to NMR by iteratively removing the top feature and retraining and testing the model. Thereafter, it examines how the features are reordered in the model which implies the effect of collinearity.

These two methods (MIP, NMR) can be useful both in having a reliable sorting of features, and on selecting one &mdash;most stable&mdash; of several methods.

## Definition of a few concepts

<details><summary>Aside: Collinearity and Non-linearity</summary>

**Multicollinearity**: one feature is a linear combination of one or more other features. For example, $x_3 = \beta_2 x_2 + \beta_1 x_1 + \beta_0$; assuming linear independence would be an error. In the [paper's words][using_shap_lime]:

> Indeed, some features might be assigned a low score despite being significantly associated with the outcome. This is because they do not improve the model performance due to their collinearity with other features whose impact has already been accounted for.

**Non-linearity**: output changes are not proportional to input changes. For example $y = \beta x^N$ is non-linear, and fitting a line $y' = \alpha x$ to it would be inaccurate. Some SHAP models can model this correctly.

</details>

Let's now look at other methods.

<details>
<summary>Sources</summary>

1. [A value for n-person games][shap original] (1952)
1. ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] (2016)
1. [A Unified Approach to Interpreting Model Predictions][unified_approach_lcobf] (2017)
1. [Principles and practice of explainable machine-learning][principles_and_practices] (2021, 25 pages): overview of many aspects of XAI,
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2025): conceptual aspects (weaknesses, strengths, assumptions) of the popular XAI methods SHAP and LIME.

</details>

[lime]: https://dl.acm.org/doi/10.1145/2939672.2939778
[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full
[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304
[unified_approach_lcobf]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html
[shap original]: https://sites.math.rutgers.edu/~zeilberg/EM22/Shapley1952.pdf

<!-- ### LIME: Two Explanatory Levels -->
<!---->
<!-- The paper describes two explanatory levels; they also map to _trust_ levels: an explanation increases understanding which in turn calibrates our trust. -->
<!---->
<!-- - _Explaining / Trusting a prediction_: Does the user trust the prediction to take an action based on it? For that, the user needs to develop an intuitive understanding of which features contribute most to the model's output. Also, the explanation model must be faithful and simple. -->
<!---->
<!-- - _Explain / Trusting the whole model_: Does it perform well on real-world data? For the right reasons? Explanations from representative inputs may be aggregated to (global explanation), beyond just particular predictions. The method used for this purpose is called SP-LIME. This is used alongside evaluation accuracy and other metrics. -->
<!---->
<!-- Both explanations boil down to understanding predictions. -->

<!-- They also propose a complexity metric because even those simpler models can become hard to interpret (they call this fidelity-interpretability tradeoff).  -->

<!-- Diagramatically, it would be: -->

<!-- ```mermaid -->
<!-- flowchart TB -->
<!-- A["x=[1.2,2.5,...,6.0]"] -->
<!-- B["x'=[1,..,1]"] -->
<!-- C["z'_1=[0,..,1]",  g(z'_1)] -->
<!-- D["z'_2=[1,..,0]",  g(z'_2)] -->
<!-- E["z_1=[0,..,6.0],  f(z_1)"] -->
<!-- F["z_2=[1.2,..,0]", f(z_2)] -->
<!---->
<!-- A --\> B -->
<!-- B --\> C -->
<!-- B --\> D -->
<!-- C --\> E -->
<!-- D --\> F -->
<!-- ``` -->

<!-- The interpretable representation is a binary vector that may use a subset of the original features (even transformed ones). This vector is easier to understand while staying close to the original model _around a prediction_ (locally faithful). -->

<!-- The **benefits** of such desiderata are: -->
<!---->
<!-- - Providing understanding of predictions, -->
<!-- - Deciding whether and why to accept (or reject) a prediction, -->
<!-- - Choosing between competing models, -->
<!-- - Suggesting improvement to a model (e.g. that which uses relevant features). -->
<!---->
<!-- Some of the **drawbacks**: -->
<!---->
<!-- - Explanation model will be sometimes wrong, -->
<!-- - May be inaccurate if reference model is highly non-linear around sample, -->
<!-- - Some input-features may be hard to encode in binary form. -->
<!-- - If a model uses a binary or interpretable input, then the contribution of a feature may be known by "turning it on and off". LIME helps when there are too many, or they are not interpretable. -->
