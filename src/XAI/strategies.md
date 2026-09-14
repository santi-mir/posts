# Additive Feature Attribution Methods

This post explores the "Additive Feature Attribution Methods" class of _extrinsic explainability_ methods (where the reference model's internals aren't analysed).

<!-- There is less emphasis on audiences or technicalities about explanations. -->

---------

## What are AFAMs?

Additive Feature Attribution Methods (AFAMs) approximate a prediction of the original model ($f$) with an _explanation model_ ($g$) which is a linear addition of binary features, making it simpler and interpretable.

How do _explanation models_ relate to out general idea of [explanations](./explanation.md)? Here is what [Explaining Explanations in AI][xxai] says:

> These [explanation] models can be understood as a "do it yourself kit" for explanations, allowing a practitioner to directly answer "what if questions" or generate contrastive explanations without external assistance.

Mathematically, the explanation model ($g$) is described as:

$$f(x) \approx g(z') = \phi_0 + \sum_{i=1}^M \phi_i z_i'$$

Each $\phi_i \in R$ is an effects of a _binary_ feature $z_i' \in \{0, 1\}^M$ in the output. The different methods in the class estimate $\phi_i$ differently.

> [!NOTE]
> **Explanation Model**
>
> [In their words][shap_values] : "We introduce the perspective of viewing any explanation of a model’s prediction as a model itself, which we term the _explanation model_." and also "Instead, we must use a simpler _explanation model_, which we define as any interpretable approximation of the original model.".

The paper [Explaining Explanations in AI][xxai] relates such models to approximate scientific models (which are all of them as reminded by Box's maxim "All models are wrong but some are useful"). So it is important for the recipients or users to know where models are reliable, where they break down or where they have unknown behaviour. In their words:

> For an individual to be able to trust such a model as an approximation, they must know over which domain a model is reliable and accurate, where it breaks down, and where its behaviour is uncertain. If the recipient of a local approximation does not understand its limitations, at best it is not comprehensible, and at worst misleading.
>
> This is not to say that local approximations are without merit, but rather that they can only reliably have explanatory power if their limitations are clearly documented and understood by recipients.

The paper also highlights a link between _explanation models_ (and would also apply to transparent models) to contrastive and what-if explanations:

> Over the domain for which the model accurately maps onto the phenomena we are interested in, it can be used to answer "what if" questions, for example "What would the outcome be if the data looked like this instead?" and to search for contrastive explanations, for example "How could I alter the data to get outcome X?"

However (as they note) local explanation models won't be accurate outside of the local domain (by definition). Also, the explanation models may be faithful to the prediction model, but if the latter is unreliable, the explanation model will also be (though on the positive side, this may be more obvious in the simpler model).

Finally, just for completeness:

> [!NOTE]
> The AFAM class was identified in the paper [A Unified Approach To Interpreting Model Predictions][unified_approach_lcobf].

## SHAP

Linear LIME, DeepLIFT and other methods calculate $\phi_i$s differently, in turn yielding different coefficients.

The [Unified Approach to Interpret Model Predictions][unified_approach_lcobf] proposes that models should have _local accuracy_, _missingness_, _consistency_ which, they argue, lead to coefficients that are more intuitive for humans.

The terms are defined as:

- **Local Accuracy**: There must be equality when the input is the original one ($x$), that is $f(x) = g(x')$.
- **Missingness**: If the reference vector ($x'$) has a "missing" component ($x_i'=0$) then the feature must have no impact, that is $\phi_i = 0$.
- **Consistency**: if one of two models is larger just turning feature $i$ on and off, then it must have a larger $\phi_i$.

Their Theorem (Theorem 1) guarantees ahat a linear explanation model plus the 3 requirements leave Shapley Values (a result from [game-theory found by Shapley][shap original]) as the best (and unique) coefficients. Other methods violate some of these 3 properties (so the authors modify them to comply).

SHAP (SHapley Additive Explanations) Values are the Shapley Values of a conditional expectation function of the original model: $f(h_x(z')) =  \mathbb{E}[f(z)|z_S]$ (Section 4, see Figure 1). $S$ are non-zero indices.

- For example, with $\vec{z} = \langle{}v_1, 0, v_2\rangle{}$ then $\phi_3 = \mathbb{E}[f(z)|z_{1,3}]$. So the Shapley values are the change in the expected model prediction when conditioning on a feature.

> [!NOTE]
> The most accurate Shapley Values are expensive to calculate. Approximations can be used in some cases to speed this up.

<!-- They come from a combinatorial which depends on the prediction model $f(h_x(z))$ and a "fixed" input $x$: -->
<!-- - $\phi_i(f,x)$ is a complex combinatorial depending on on the definition of $f$ around a point $x$, which they define as an expectation value $f(h_x(z)) =  \mathbb{E}[f(z)|z_S]$
When the model $f$ is highly non-linear or the features are correlated, the estimation of SHAP values involves a complex average of values, otherwise there are useful approximations to them. -->

### Approximating SHAP Values

The approximations can be _model agnostic_: Shapley Sampling Values, Quantitative Input Influence, Kernel SHAP; or they can be _model-specific_: Max SHAP, Deep SHAP.

The actual approximations are:

**Approximation 1**: Feature independence (implies non-multicollinearity).

- Shapley sampling values method,
- Quantitative Input Influence,
- Kernel SHAP (requires both assumptions).

**Approximation 2**, model linearity: Shapley regression values.

- SHAP provides both global (average across inputs) and local (for a given input).

### Kernel SHAP

Can we modify Linear LIME's Loss function so that the values of coefficients found are Shapley values? Yes! These are also more intuitive to humans, and remove some of the heuristics (kernel selection and complexity metric) of it.

The Linear LIME quantities of _proximity kernel_ ($\pi_x$), complexity penalty ($\Omega(g)$) and Loss ($L$) are turned into a _shapley kernel_, $\Omega(g) = 0$, and the same weighted loss.

The SHAP values / coefficients for this linear model with assumed-uncorrelated features can be estimated by weighted linear regression.

This method is called Kernel SHAP, and it's fast to compute.

## LIME and SP-LIME

The paper ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] proposes the Local Interpretable Model-Agnostic eXplanation (LIME) and the Submodule Picking LIME.

LIME isn't a particular model but rather a set of characteristics that explainable methods should have, according to the authors (more on this later).

Let's first look at LIME as implemented in a concrete case.

### Why would this be useful? A concrete example

A linear model with few-ish, interpretable features, locally fit to a complex one is in line with LIMEs' requirements.

Local fit means fitting only in the vicinity of the input of interest. The input features may differ from those in the original model.

The [original paper][lime] shows an example comparing two different models that were fit by linear ones:

<div class="center w60">
    <a href="../assets/LIME.png">
    <img src="../assets/LIME.png" alt="Comparison between to algorithms analysed by LIME."/>
    </a>
    <p>Image taken from <a href="https://dl.acm.org/doi/10.1145/2939672.2939778">paper</a>.</p>
</div>

The image makes clear some of the uses of it:

- The interpretable features, alongside their contributions (weights) to the prediction, can help decide whether to trust the prediction or not.
- Feature engineering such as removing features (or certain data) that the model uses but harm generalisation,
- Comparing models is easy (through the linear proxies). It's especially useful if the original models' accuracy (and other metrics) are similar, and their features non-interpretable.
- Here, one of them is untrustworhy (right hand side), giving high weight to meaningless features.

### LIME / Desiderata

The authors consider 4 properties to be desirable in an explanation model:

- _Local_: the interpretable or explanation model approximates the original model in the vicinity of a particular prediction. In contrast, _global_ explanations explain the full model.
- _Model-agnostic_: any model can in principle be explained by this method.
- _Interpretable Explanation_: In this paper, "interpretable" is a desired characteristic of "explanation", and provides qualititative understanding (a simple answer to "Why was this prediction made?"). In their own words:
  > An essential criterion for explanations is that they must be **interpretable**, i.e., provide qualitative understanding between the input variables and the response. We note that interpretability must take into account the user's limitations.

Additionally, they include `4.` A global perspective, a mechanism to get a sense of the full model's behaviour.

The first 3 can be called LIME; the Submodule Picking LIME (SP-LIME), which selects LIME explanations to give a global explanation of the model.

LIME is a slightly more explicit version of the first 3 desired properties. Let's explore this.

- Which specific representations does the [LIME][lime] framework consider interpretable?

  An example of an _interpretable representation_ is a binary vector with components indicating presence / absence of a feature (e.g. a word) in the explanation model.

- Which models does the [LIME][lime] paper consider interpretable?

  > (...) interpretable models, such as linear models, decision trees, or falling rule lists [27], i.e. a model $g \in G$ can be readily presented to the user with visual or textual artifacts.

- Complexity is the opposite of interpretable, so the loss (we skip it here) to train the explainable model accounts for it, and gives local samples more importance than remote ones. Here $G$ being the model class of $g$:

  > As not every $g \in G$ may be simple enough to be interpretable thus we let $\Omega(g)$ be a measure of complexity (as opposed to interpretability) of the explanation $g \in G$.

  The definition of complexity depends on $G$. For linear models it may be the number of weights.

- They also define a sampling procedure to create the training set. This is detailed in the concrete algorithm in the next section.

### Linear LIME: An Algorithm

The paper implements LIME using the class $G$ of sparse linear models as explanation model, which we could call Linear LIME (as
[A Unified Approach to Interpreting Model Predictions][unified_approach_lcobf] does). Here is my interpretation of the algorithm (the primed variables denote binary vectors):

1. A model $f$ and an input vector $x \in R^n$ needs explaining,
2. Start an interpretable, binary vector $x' \in \{0,1\}^{n'}$ with only the dimensions of interest of $x$ (it may be all-ones often),
3. Generate perturbed binary variants of $x'$ called $z'_i$,
4. Use different $z'$ to make variants of $x$ called $z \in R^n$.
    - Written in [A Unified Approach to Interpreting Model Predictions][unified_approach_lcobf] paper as $z = h_x(z')$.
5. Now we have training tuples $(f(z), z', \pi_{x} (z))$.
6. Use the dataset to fit the linear model $g$ using $K-LASSO$.
    - To select $K$ interpretable features they apply $K$-LASSO.
    - LASSO is like a sparse linear regression, some coefficients are pushed to $0$ and correspond to variables we can ignore. How many are are pushed to $0$ may be controlled by the complexity penalty in the loss function.
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

## Robustness Fixes

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
1. ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] (2016),
1. [A Unified Approach to Interpreting Model Predictions][unified_approach_lcobf] (2017),
1. [Explaining Explanations in AI][xxai] (2019),
1. [Principles and practice of explainable machine-learning][principles_and_practice] (2021, 25 pages): overview of many aspects of XAI,
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2025): conceptual aspects (weaknesses, strengths, assumptions) of the popular XAI methods SHAP and LIME.

</details>

[lime]: https://dl.acm.org/doi/10.1145/2939672.2939778
[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full
[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304
[unified_approach_lcobf]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html
[shap original]: https://sites.math.rutgers.edu/~zeilberg/EM22/Shapley1952.pdf
[xxai]: https://dl.acm.org/doi/10.1145/3287560.3287574

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

<!-- Considerations: -->
<!-- 1. Two complex models $f_1$, $f_2$ trained with same data likely have different coefficients for each approximation model ($\phi_i$s), -->
<!-- 1. Explanation models don't protect from a biased prediction model, -->
<!-- 1. Some methods, such as Kernel SHAP and LIME, assume independent features, -->
<!-- 1. If we assume linearity and the reality is non-linear there will also be an error. -->

<!-- _Note_: these could be called linear combination of binary features as well. -->
