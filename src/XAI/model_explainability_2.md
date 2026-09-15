# Topics in XAI

Having described the structure of the field of XAI, with a brief on popular methods, let's now discuss two topics: the modelling trade-off and generalisation out of distribution. Finally, an interesting map of XAI extracted from one paper is shown.

----------------------

## Trade-offs?

We may expect _model explainability_ to be inversely correlated with model complexity or accuracy. Graphically:

<div class="center w30">
    <a href="../assets/tradeoff.webp">
    <img src="../assets/tradeoff.webp" alt="Model Explainability vs Model accuracy tradeoff."/>
    </a>
    <p>Hypothesis: Model explainability v. Accuracy tradeoff.</p>
</div>

And in ["Why Should I Trust You?"][lime] (refs removed):

> Recognizing the utility of explanations in assessing trust, many have proposed using interpretable models, especially for the medical domain. While such models may be appropriate for some domains, they may not apply equally well to others (...). Interpretability, in these cases, comes at the cost of flexibility, accuracy, or efficiency.

And in [SHAP][shap]:

> However, the highest accuracy for large modern datasets is often achieved by complex models that even experts struggle to interpret, such as ensemble or deep learning models, creating a tension between accuracy and interpretability.

And in [Explaining Explanations in AI][xxai]:

> (...) three-way trade-off between the simplicity of the approximated model, the size of the domain it describes, and the accuracy of this description.

Other researchers such as [Rudin][interpretable_ml] disagree (references were removed):

> Two obstacles to using interpretable models are that they are harder to optimize because they require extra constraints, and there is an incorrect perception that they are less accurate than black boxes. On the first point, the community is getting quite good at building interpretable sparse models and interpretable neural networks. On the second point, there is no scientific evidence that accuracy must be sacrificed when adding interpretability constraints.

Rudin's [more detailed paper][stop_explaining_interpret_instead] states something similar:

> There is a widespread belief that more complex models are more accurate, meaning that a complicated black box is necessary for top predictive performance. However, this is often not true, particularly when the data are structured, with a good representation in terms of naturally meaningful features.

I'd make two comments to the quote above. First, _good representation in terms of naturally meaningful features_ may be hard to obtain or create. Second, NNs tend to perform better as we scale them up. Though there is some "optimal-size region" and going beyond could plateau or even decrease its performance.

The paper also states a related complication:

> Interpretable models can entail significant effort to construct, in terms of both computation and domain expertise. (...) for high-stakes decisions, analyst time and computational time are less expensive than the cost of having a flawed or overly complicated model.
> (...)
> The researcher needs to create a model that has the capability of uncovering the types of patterns that the user would find interpretable, but also the model needs to be flexible enough to fit the data accurately. This, and the optimization challenges discussed above, are where the difficulty lies with constructing interpretable models.

## Out of Distribution

Consider an imaginary model $y = f(u)$, $f$ being the model, $u$ being the proportion of people with an umbrella and $y$ the probability of rain. The model reaches low evaluation error and everyone is happy.

However, the model consistently fails to predict rains when people didn't take the umbrella. Why could this happen? Some of the reasons below were inspired by the paper "[The Mythods of Model Interpretability][mythos]":

1. The model _undefitted_ the data, and we may need a better model.
1. The dataset is _not representative_ the deployment environment, and the model can't generalise out of training distribution. Can it be fixed if we don't have those datapoints? Were there simply wrong datapoints, that led the model in the wrong direction? Can we create synthetic data?
1. The approach itself was incorrect: we use variables that promote _association rather than causation_.

Selecting possible causal variables, such as pressure and temperature, rather than the fraction of humans carrying out an umbrella, could help to make it more accurate, and even more explainable. But does it have _all_ the _causal inputs_? Why do we expect it to work out of distribution, though?[^selection_problem]

A subset of causal-variables may do for a good-enough approximation, and even generale well out of distribution. In some cases though, it may be enough to have a correlation model, but they should be distinguished.

Selecting those variables is not very easy, though. An expert must pick known causes-effects pairs as inputs-outputs to train a model, but others may unknowingly build a correlation model instead.

> It is hard to predict whether a model will work out of distribution without knowing what it has learnt. Knowing what a model has learnt is part of the XAI discipline, both opening the box, or carefully comparing its outputs.

Similarly, [this two-page comment][interpretable_ml] by Cynthia Rudin highlights the preference for interpretable (transparent) models in high stakes scenarios.

In Deep Learning Models, the problem constraints can be used to add inductive biases or priors to architectures, such as symmetry constraints, connectivity (say through graph networks). This may also reduce the amount of training data needed, improve generalisation and improve interpretability.

An idea related to "Out Of Distribution" inference is that of "Transfer Learning": If a model has learnt "essential, compact features" then they should generalise to other task, as stated in [Scientific discovery in the age of artificial intelligence][ai_aided_discovery] (references where removed):

> Self-supervised learning (Box 1) has enabled neural networks trained on labelled or unlabelled data to transfer learned representations to a different domain with few labelled examples, for example, by pre-training large foundation models and adapting them to solve diverse tasks across different domains.

This is especially useful when models can leverage large amount of data, which is usually in the form of unlabelled data (there are also mechanisms to label data semi-reliably).

Another promising path towards better generalisation is that of Causal AI. As ["Scientific discovery in the age of artificial intelligence"][ai_aided_discovery] puts it:

> Although many scientific laws are not universal, their applicability is generally broad. Compared with state-of-the-art AI, human brains can better and faster generalize to modified settings. An attractive hypothesis is that this is because humans build not just a statistical model of what they observe but a causal model, that is, a family of statistical models indexed by all possible interventions (for example, different initial states, actions of agents or different regimes). Incorporating causality in AI is still a young field

## Map of XAI

An interesting map of XAI is given in the survey [Principles and practice of explainable ML][principles_and_practice] (2021).

Most _classic ML_ models are in the <span style="padding:0.15rem; display: inline-block; border-radius:0.5rem; border:0.15rem dashed purple">dashed</span> area under **Model types** column.

_Classic ML_ models are usually _transparent_ (intrinsically explainable) but _may_ benefit from post-hoc (post training) explanations, such as visualising it. When transparency is key and the predictions are accurate enough, these may be preferred over DL models.

<div class="center w50">
    <a href="../assets/taxonomy.webp">
    <img src="../assets/taxonomy.webp" alt="Complex Graph linking prediction models such as SVMs, kinds of explanations such as text or graph, and explanation methods such as SHAP."/>
    </a>
    <p>
    Image from <a href="https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full">paper</a> under <a href="https://creativecommons.org/licenses/by/4.0/">CC-BY</a>
    </p>
</div>

To the visual explanations, t-SNE, PCA and other dimensionality reduction techniques can be added.

The focus here though, is explaining _deep learning_ models which are often, but not always, more accurate than classic ML models.

[ai_aided_discovery]: https://www.nature.com/articles/s41586-023-06221-2
[lime]: https://dl.acm.org/doi/10.1145/2939672.2939778
[mythos]: https://dl.acm.org/doi/10.1145/3236386.3241340
[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full
[stop_explaining_interpret_instead]: http://arxiv.org/abs/1811.10154
[xxai]: https://dl.acm.org/doi/10.1145/3287560.3287574

[^selection_problem]: Could metaphors and analogies (from experience) be the missing ingredient of this to succeed? Could using causal models help to overcome these problems? How can we make a model that uses analogies?


<!-- In other words, classical ML and DL models each have their use-cases. -->

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->
