# Explainable AI

Explanations were defined and characterised in [explanations](./explanation.md). This post explores the connection of _explanations_ to _deep learning models_.

----------------

<!-- ## Real World Objectives-->
<!---->
<!-- Partly based on the paper [The Mythos of Model Interpretability][mythos] we want to:-->
<!-- 1. Trust. In which sense? Accuracy deployment robustness, human-performance? -->
<!-- 2. Causality. They are usually trained to just make correlations/associations, and they may learn to use proxy-variables, confounders (X-Y may have both an underlying Z-cause), shortcuts; we would want causal relationships instead. Bayesian Networks and Regression Trees? How can we infer causal relations from observational data (Pearl, Causality) -->
<!-- Transferability: This isn't just about Out Of Distribution, but that the training environment correctly reflects the deployment one (for example, programmers may misinterpret the meaning of some column, or it may even be wrong, which could still happen in accurate models! So this should be broken down into database trust (which is also mentioned by Rudin though in terms of data poisoning rather than errors) and data-task correctly understood, and model generality / performance OoD.
Unclear why this item is about interpretability.
-->
<!-- Informativeness: Interesting. Besides or along with the primary training objective it may be possible to extract extra information from the model, to help (inform) the user. This may be provided with posthoc or intrinsic XAI as well. Rudin et.al., created a "classifier-by-similarity" CNN that outputs which images in the dataset where used to decide, compared to. Or point to similar cases. Counterfactuals / Contrasts seem another way (Juergensen).
-->
<!-- Ethics: Right to explanation (GDPR), Conform to ethical standards,..-->
<!-- 4. Improve debugging / troubleshooting? -->
<!-- 5. Get more useful information from the model. -->

## Model Explainability

Explainable AI (XAI) is primarily about explaining machine and deep learning models and their outputs. In this blogpost, explainability and interpretability are considered synonyms. _Model explainability_ can be defined as:

> The degree to which we can answer questions about a model and its output. The _answers_ are context and audience (including ourselves).

<!-- Since there are many definitions and goals of XAI we should always define the term (even approximately) or to cite a definition, and to state _which problems_ our ideas aim to solve. -->

Below, a few types of _model explainability_, namely Intrinsic and Extrinsic[^1], Local and Global, are explained.

### Intrinsic Explainability

Looks at the internal mechanics, at the roles of layers, neurons, weights; it may also relate to constraining the model in form (e.g., [Rudin C.][stop_explaining_interpret_instead] or [Zachary C.][mythos]) &mdash;that is, imposing physical constraints, inductive biases, causal inputs selected by experts, monotonicity, sparsity, constraining model size or computational complexity. Or as Zachary C. [puts it][mythos]:

> Sufficiently high-dimensional [linear] models, unwieldy rule lists, and deep decision trees could all be considered less transparent than comparatively compact neural networks.

Transparency is domain-dependent. For example, the field of **geometric deep learning** can express constraints (or inductive biases) of connectivity related to molecules and materials (e.g. GNNs), making them more interpretable than other network architectures for representing this particular input / physical problem. This can be further extended to symmetry and other aspects.

### Extrinsic Explainability

Aims to give a qualitative understanding between inputs and outputs, be easy to understand, and be model agnostic. They should also have good local fidelity, that is, they should be a good approximation to the original model in the vicinity of the instance being predicted. The local explanations may also be combined to provide a _global explanation_ of the model. All of these properties were taken from [LIME][lime].

The fidelity usually isn't perfect &mdash;unless it's just the original model. Simplified models may use less variables than the original, making it easier to understand.

[Rudin][stop_explaining_interpret_instead] argues that these simpler explanation models must be wrong; if it is the same, then we don't need the original model. Rudin proposes calling these model-approximation techniques "summary of predictions", "summary statistics" or "trends".

On the other hand, methods such as SHAP, LIME, t-SNE, can provide _some_ understanding of the model, even if using approximations. In the case of LIME, the explanations are _not global_, but _local_, so the model can't replace the original, and it may be locally-faithful. The question is rather _how faithful_ it needs to be. Combination of local explanations may also give a global understanding of the model. As [LIME][lime]'s paper puts it:

> By "explaining a prediction", we mean presenting textual or visual artifacts that provide qualitative understanding of the relationship between the instance's components (e.g. words in text, patches in an image) and the model’s prediction.

> [!NOTE]
> Not all models need an explanation model, some may use explanation techniques that still look at them as black boxes, such as contrastive or counterfactual explanations.

### Global vs Local

- Global: valid for all inputs, e.g. LIME combining local explanations and also gradient based methods (which are never local).
- Local: for specific inputs, e.g. LIME and other input-perturbation explanation models.

### Brief Aside: Neural Netwoks

This post assumes a working idea of what deep learning models or neural networks are. A simple definition is provided in the paper [Can we open the black box of AI?][open_ai_black_box] (Section "Good Trip").

But what exactly do these networks _learn_? ["Scientific discovery in the age of artificial intelligence"][ai_aided_discovery] states that:

> [AI methods] includes deep representation learning (Box 1), particularly multilayered neural networks capable of identifying essential, compact features that can simultaneously solve many tasks that underlie a scientific problem.

So a key aspect of understanding and explaining will be to decode those "essential, compact features" into domain concepts. What concepts, if any, are stored there, in the synapses?

It's also useful to have in mind a general idea of where are neural networks models being used, and how:

1. Domain-specific (Narrow AI): these are small or large models but trained on a specific domain (protein folding, generating new molecules, predicting spectra and so forth). These models benefit from XAI, inductive biases and constrains, and would ideally be interpretable.
2. Domain-general (Foundation Models): there is a spectrum between networks trained for a task in a domain, and for a whole domain (e.g. chemistry). These models are usually very large, pre-trained in some unsupervised way and then need to be fine tuned to specific tasks, where they reuse the learnt building blocks.
3. AI agents: These are clusters of models working together to carry out many parts of the scientific process of discovery (hypothesis generation, reading literature, suggesting experiments and running code simulations etc.) In some cases they may also have access to robotics platforms and run real world experiments. The difference to other approaches is that these models are reasoning, and to some extent work like a team of scientists.

Here we are concerned with `1.` primarily, and with the possibility to explain them, design them such that they are interpretable and finally understand them better.

### Trade-offs?

We may expect _model explainability_ to be inversely correlated with model complexity or accuracy. Graphically:

<div class="center w30">
    <a href="../assets/tradeoff.webp">
    <img src="../assets/tradeoff.webp" alt="Model Explainability vs Model accuracy tradeoff."/>
    </a>
    <p>Hypothesis: Model explainability v. Accuracy tradeoff.</p>
</div>

A similar idea may be behind [Zachary's paper][mythos]:

> One advantage of this concept of interpretability [post hoc interpretability] is that opaque models can be interpreted after the fact, without sacrificing predictive performance.

And similarly, in [LIME][lime] (refs removed):

> Recognizing the utility of explanations in assessing trust, many have proposed using interpretable models, especially for the medical domain. While such models may be appropriate for some domains, they may not apply equally well to others (...). Interpretability, in these cases, comes at the cost of flexibility, accuracy, or efficiency.

Other researchers such as [Rudin][interpretable_ml] disagredisagree (bold is mine, references were removed):

> Two obstacles to using interpretable models are that they are harder to optimize because they require extra constraints, and there is an **incorrect perception** that they are **less accurate than black boxes**. On the first point, the community is getting quite good at building interpretable sparse models and interpretable neural networks. On the second point, there is **no scientific evidence that accuracy must be sacrificed when adding interpretability constraints**.

Rudin's [more detailed paper][stop_explaining_interpret_instead] states something similar:

> There is a widespread belief that more complex models are more accurate, meaning that a complicated black box is necessary for top predictive performance. However, this is often not true, particularly when the data are structured, with a good representation in terms of naturally meaningful features.

I'd make two comments to the quote above. First, _good representation in terms of naturally meaningful features_ may be hard to obtain or create. Second, NNs tend to perform better as we scale them up. Though there is some "optimal-size region" and going beyond could plateau or even decrease its performance.

For complex tasks (Natural Language Processing, Computer Vision), DL models surpass most other algorithms. For narrower tasks, it is sometimes possible to find interpretable models that are also very accurate (benchmarks?), but they can be very hard to design, making the time-risk-benefit tradeoff worth considering:

> Interpretable models can entail significant effort to construct, in terms of both computation and domain expertise. (...) for high-stakes decisions, analyst time and computational time are less expensive than the cost of having a flawed or overly complicated model.
> (...)
> The researcher needs to create a model that has the capability of uncovering the types of patterns that the user would find interpretable, but also the model needs to be flexible enough to fit the data accurately. This, and the optimization challenges discussed above, are where the difficulty lies with constructing interpretable models.

<!-- explain also that there are are clear reasons companies may prefer black box models (in two senses): proprietary helps to profit (and restricts gaming them), black box helps avoid accountability / responsibility. -->

## Out of Distribution

Consider an imaginary model $y = f(u)$, $f$ being the model, $u$ being the proportion of people with an umbrella and $y$ the probability of rain. The model reaches low evaluation error and everyone is happy.

However, the model consistently fails to predict rains when people didn't take the umbrella. Why could this happen? Some of the reasons below were inspired by the paper "[The Mythods of Model Interpretability][mythos]":

1. The model _undefitted_ the data, and we may need a better model.
1. The dataset is _not representative_ the deployment environment, and the model can't generalise out of training distribution. Can it be fixed if we don't have those datapoints? Were there simply wrong datapoints, that led the model in the wrong direction? Can we create synthetic data?
1. The approach itself was incorrect: we use variables that promote _association rather than causation_.

Selecting possible causal variables, such as pressure and temperature, rather than the fraction of humans carrying out an umbrella, could help to make it more accurate, and even more explainable. But does it have _all_ the _causal inputs_? Why do we expect it to work out of distribution, though?[^2]

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

## Model Insights from Comparisons

How many ways do we have to make comparisons? Probably dozens. Analogies, metaphors, counterfactuals, a reference case (opposite or similar), a prototype or class-assignment (generalisation uses comparison).

_Counterfactuals_ What would have happened with an alternative input (a hypothetical case counter to the fact). It's most informative to use the minimum changes that change an output class. They are also similar to _What ifs_ (as the question shows).

Counterfacturals and other comparisons can help to explain models without opening the box.

For a model, _counterfactuals_ are yet another inference from another input, but the comparison is helpful because that is one way humans understand things. We can use them as a proxy to "understand how the model is thinking" (that is, by comparing results or inferences).

In a similar fashion to counterfactuals, we can compare with reference inputs.

<!-- (A logic-inference section could be added, but at the moment I don't see it adding much useful information.) -->

<!-- ## Higher-Level Aspects of Networks -->
<!---->
<!-- The recognition of higher level patterns in graph can also span across methods. -->
<!---->
<!-- These can even be inspired by other networks or graphs; for example, insect colonies can be considered as graphs of insect-nodes and pheromone-edges, and certain nodes have roles and tasks they specialise on. A similar situation can be postulated to happen in human networks, and in neural (biological and artificial) networks, where the node is affected by, and also affects other nodes. -->
<!---->
<!-- A basic description of graph and networks and how there can be transfer learning between the different areas can be found in [Siemens - Connectivism][connectivism_siemens] and particularly in [Downes - Connectivism][connectivism_downes]. -->

## Overview of methods

There are many methods to identify causes or relevant properties on models, that help explain how they work. Some of them include counterfactuals and comparison, in the same sense as used in our previous section.

For all audiences, we can group these methods into more general categories, and then go into specific cases for a certain audience.

### Kinds of Methods

The survey [Principles and practise of explaining ML models][principles_and_practice] includes a table of **method kinds**. A modified version of the table is below:

| Kind         | Advantages    | Disadvantages | Question |
|---------------------|---------------|---------------|----------|
| **Local explanations** | Explains the model's behaviour in a local area of interest. Operates on instance-level explanations. | Explanations do not generalize on a global scale. Small **perturbations** might result in very different explanations.| How do small perturbations affect the output / prediction? |
| **Examples**      | Representative items for each class provide insights about the model's internal reasoning. | Examples require human selection. They do not explicitly state what parts of the example influence the model. | How do inputs from different classes compare? And same? |
| **Feature relevance** | They operate on an instance level (some can operate globally). | Methods may make assumptions which do not hold (e.g. feature independence, linearity).| Which input features are most important? |
| **Simplification**  | Simple surrogate models explain opaque ones. | Surrogate models may not approximate original models well. | Can we get local insights by using a simpler model? |
| **Visualizations**  | Easier to communicate to non-technical audiences. Most approaches are intuitive and not hard to implement. | There is an upper bound on how many features can be considered at once. Humans must inspect plots to derive explanations. | Class boundaries? |

A method not listed there are text explanations, which can be generated from an RNN or a language model, reading the model's internal state (for example, this can generate captions).

We should remember that:

> Relying on only one technique will only give us a partial picture of the whole story, possibly missing out important information. Hence, combining multiple approaches together provides for a more cautious way to explain a model. (...) At this point we would like to note that there is no established way of combining techniques (in a pipeline fashion),

In the next posts, we focus on **methods** that aid _causal attribution_ (or cognitive process) with a scientific audience in mind.

### Map of XAI

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

<!-- In other words, classical ML and DL models each have their use-cases. -->

----------------

<details>
<summary>Sources</summary>

1. [Can we open the black box of AI?][open_ai_black_box] (2016). This paper briefly explains what ANNs are, their similarities (not the differences) to the brain, and what challenges they pose to us. Primarily, the challenge is that they are hard to explain. It puts as an example a physician or patient relying in the output, but not knowing _why_ it predicts that. The author also cites Michael Tyka saying "The problem is that the knowledge gets baked into the network, rather than into us" which is also interesting.
Furthermore, there isn't a "number 5 pattern" that is the same for many networks; the pattern appears from the training procedure, and although it may be similar for all number 5, it's usually different between training runs, datasets, and networks. Similarly so for brains!
1. ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] (2016)
1. [The Mythos of Model Interpretability][mythos] (2018) is an excellent break down of ideas. They consider two interpretability strategies:
   - _Transparency_ (intrinsic explainability) can refer to: `1.` _simulatability_ i.e. can mentally run the model, `2.` _decomposability_ i.e. each part of the model admits an intuitive explanation, and `3.` _algorithmic training_ which focuses on global vs local minimum, error and loss, guaranteed convergence.;
   - _Posthoc_ interpretability (black boxness / extrinsic explainability): does not elucidate precisely how a model works. It breaks down techniques such as `1.` Textual explanations using RNNs, visual explanations of learned representations (dimensionality reduction methods such as t-SNE, PCA), input alteration (to maximise activation of a neuron), `2.` Local alterations using derivative of input wrt output (measuring "sensitivity" to each pixel); `3.` By example / similarity / comparison and so forth. Posthoc is the sort of interpretability / explainability that applies to humans (which are otherwise black boxes).
   - Another takeaway is that obsessing about model transparency can harm accuracy and capability of a model, so it is important to consider this aspect.
1. [A Unified Approach to Interpreting Model Predictions][shap_values] (2017): paper proposing SHAP, that is, showing Shapley values as the best coefficients in linear combination of features, given 3 requirements (local accuracy, missingness and consistency),
1. [Explaining Explanations: An Overview of Interpretability of Machine Learning][xx] (2018),
1. [Producing radiologist-quality reports for interpretable artificial intelligence][xai_rnn_radiology] (2018): a "case study",
1. [The Book of Why][tbow] (2018): The introduction and first chapter were read in detail, only the part of interest for XAI (to my judgement) is discussed here, comparison and counterfactuals. It's interesting but may be more useful in other areas (like medical sciences, economics etc.)
1. [Stop Explaining Black Box Machine Learning Models for High Stakes Decisions and Use Interpretable Models Instead][stop_explaining_interpret_instead] (2019).
   - Suggests post-hoc models are worse than interpretable/transparent ones for high-stakes scenarios. It also states that the definitions of "Interpretable" varies for each field (references removed):
   > Interpretability is a domain-specific notion, so there cannot be an all-purpose definition. Usually, however, an interpretable machine learning model is constrained in model form so that it is either useful to someone, or obeys structural knowledge of the domain, such as monotonicity, causality, structural (generative) constraints, additivity, or physical constraints that come from domain knowledge. Interpretable models could use case-based reasoning for complex domains.
   - The paper also **challenges the beliefs** that `1.` There is a trade-off between interpretability and accuracy; also that `2.` Explanation models (e.g. SHAP, LIME) provide faithful explanations of black-box models (and that a better term to "explanations" is "summary statistics" or "trend"), finally that `3.` The explanations are detailed enough (Saliency Maps) and so forth.
   - And describes challenges towards Interpretable AI: `1.` Black boxes shields companies from accountability (incentives); `2.` Interpretable models are harder to construct (require more expertise). `3.` Belief DL models can uncover patterns that interpretable models wouldn't find (the issue is the belief).

1. [The perils and pitfalls of explainable AI: Strategies for explaining algorithmic decision-making][perils_and_pitfalls] (2021): emphasis on socio-political aspects,
1. [Why black box machine learning should be avoided for high-stakes decisions, in brief][interpretable_ml] (2022),
1. [Interpretable and Explainable Machine Learning for Materials Science and Chemistry][xai4mat] (2022),
1. [Principles and practice of explainable machine-learning][principles_and_practice] (2021, 25 pages): Sections 8&ndash;11 are a useful review of explainability methods.
1. [Scientific discovery in the age of artificial intelligence][ai_aided_discovery] (2023).
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2024).

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->
[ai_aided_discovery]: https://www.nature.com/articles/s41586-023-06221-2

[interpretable_ml]: https://www.nature.com/articles/s43586-022-00172-0

[lime]: https://dl.acm.org/doi/10.1145/2939672.2939778

[mythos]: https://dl.acm.org/doi/10.1145/3236386.3241340

[open_ai_black_box]: http://www.nature.com/news/can-we-open-the-black-box-of-ai-1.20731

[perils_and_pitfalls]: https://www.sciencedirect.com/science/article/pii/S0740624X21001027

[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full

[shap_values]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html

[stop_explaining_interpret_instead]: http://arxiv.org/abs/1811.10154

[tbow]: https://en.wikipedia.org/wiki/The_Book_of_Why

[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304

[xai_rnn_radiology]: https://arxiv.org/abs/1806.00340

[xai4mat]: https://pubs.acs.org/doi/10.1021/accountsmr.1c00244

[xx]: http://arxiv.org/abs/1806.00069

<!-- As noted in the previous post, the "questions" may be implicit; and it's common that the question, implicit or explicit is a _contrastive why-question_. -->

<!-- It's interesting to consider, that we ourselves can't really inspect our own models within the brain. We a human explains a model, there is still the "human black box", but one which we trust, maybe because of human-human similarities. -->

[^1]: Intrinsic explainability is also called "Transparency", "Inherently interpretable models"; Extrinsic explainability is also called "black boxedness", post-hoc explainability, opaqueness.
[^2]: Could metaphors and analogies (from experience) be the missing ingredient of this to succeed? Could using causal models help to overcome these problems? How can we make a model that uses analogies?
