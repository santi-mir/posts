# Model Explainability

Explanations were defined and characterised in a [previous post](./explanation.md).

Explainable AI (XAI) is primarily about explaining the model and its output, although it may include other aspects. _Model explainability_ can be defined as:

> The degree to which we can answer questions about the model and its output. The _answers_ are audience and context dependent. The audience, in some cases, may be ourselves.

Some systems may require that we, as operators, understand the decisions (explain to ourselves), or that the system can be explained by an expert to an audience.

As noted in the previous post, the "questions" may be implicit; and it's common that the question, implicit or explicit is a _contrastive why-question_.

Model explainability _includes_ terms like interpretability and transparency (which look inside the model) but also methods to analyse black-box models. Here is one possible classification:

- Intrinsic vs Extrinsic
    - Intrinsic or Transparency: looks at the internal mechanics and roles of layers, neurons, weights; also at the complexity of the model, training process, and so forth.
    - Extrinsic or Post Hoc (aka opaque or black box): looks at input-outputs relations.
- Global (valid for all inputs) vs local (for specific inputs)

> [!NOTE]
> Explaining and understanding can be mixed up, because the latter also involves some internal conversation or reflection. Here understanding, with or without that monologue, is equated to the _cognitive process_, prior to any communication. However, it certainly seems more complex.

## Trade-offs

In deep learning practice, tradeoffs abound. For example, explainability _tends to_ be harder with more accurate models, since they _tend to_ be more complex.

<div class="center w30">
    <a href="../assets/tradeoff.webp">
    <img src="../assets/tradeoff.webp" alt="Model Explainability vs Model accuracy tradeoff."/>
    </a>
    <p>Model accuracy vs Model explainability tradeoff.</p>
</div>

Moreover, simple explanations can **oversimplify** its operation, or lack **generality**.

## Explaining by Comparison

This framework is explained separately from methods to expand a bit more, but some of the methods are based on this logic behind.

### Will it rain today?

Let's take an imaginary model, $y = f(u)$, the variable $u$ being the proportion of people with an umbrella, $f$ the model and $y$ the probability of rain.

It reaches low evaluation error and everyone is happy.

However, it is sometimes found that if the people don't take the umbrella it may still rain. Why? There may be different reasons:

1. The model is doing correlation / association, but there wasn't correlation data available for such an event, so the predictions bad;
   - With a large and diverse possible dataset, most questions may be answerable; but may not generalise out of distribution, restricting discoveries to certain interpolations.
   - This _is_ useful and discoveries have been made this way, but it clearly limits them to interpolation, and low success out of distribution.
2. The model does not use causal information, like a weather forecast model would (not taking an umbrella doesn't make raining impossible).
   - Using causal models may help to overcome the problems highlighted in the previous point. It's _a bit like_ turning it into a law or theory expected to have found some deep structure that generates the data, even the unseen data.

The model is then modified to use causal variables instead (such as pressure and temperature), implicitly turning it into a _causal model_. But does it have _all_ the _causal inputs_?

An expert may pick known causes-effects pairs as inputs-outputs to train a model, but others may unknowingly build a correlation model instead.

A subset of causal-variables may do for a good-enough approximation, and likely be robust for generalising out of distribution. In some cases though, it may be enough to have a correlation model, but they should be distinguished.

### What if...?

A model that does correlation is more likely to fail out of distribution, because it has not learnt the correlation. Causal models should in principle have less of this issue.

_Counterfactuals_ ask _What would happen if this other input (fact) was used instead of the former one_, or if one feature is changed slightly? They are also similar to _What ifs_ (as the question shows).

For a model, _counterfactuals_ yet another prediction, but the question is helpful because that is one way humans explain things. In a similar fashion to counterfactuals, we can compare with reference inputs.

Both of these are known techniques listed in the next section.

<!-- (A logic-inference section could be added, but at the moment I don't see it adding much useful information.) -->

### Higher-Level Aspects of Networks

The recognition of higher level patterns in graph can also span across methods.

These can even be inspired by other networks or graphs; for example, insect colonies can be considered as graphs of insect-nodes and pheromone-edges, and certain nodes have roles and tasks they specialise on. A similar situation can be postulated to happen in human networks, and in neural (biological and artificial) networks, where the node is affected by, and also affects other nodes.

A basic description of graph and networks and how there can be transfer learning between the different areas can be found in [Siemens - Connectivism][connectivism_siemens] and particularly in [Downes - Connectivism][connectivism_downes].

## Overview of methods

Within the _cognitive process_ of explanations, _model explainability_ benefits from methods to identify causes or relevant properties.

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

The focus here though, is explaining _deep learning_ models. These are usually _opaque_ ("_black-box_") models, and their accuracy is usually higher than classic ML models.

<!-- In other words, classical ML and DL models each have their use-cases. -->

-------------------

<details>
<summary>Sources</summary>

1. [The Mythos of Model Interpretability][mythos] (2018), excellent and easy-to-read. They consider two interpretability strategies:
   - _Transparency_ (intrinsic explainability), divided into 3 levels `1.` _simulatability_ or simplicity, `2.` _decomposability_ or part-role mapping, and `3.` _algorithmic training_ which focuses on error, loss, convergence.);
   - _Post hoc_ interpretability (black box / extrinsic explainability): breaks down techniques such as textual explanations using RNNs, visual explanations, local, by example and so forth.
1. [A Unified Approach to Interpreting Model Predictions][shap_values] (2017): paper proposing SHAP, that is, showing Shapley values as the best coefficients in linear combination of features, given 3 requirements (local accuracy, missingness and consistency),
1. [Explaining Explanations: An Overview of Interpretability of Machine Learning][xx] (2018),
1. [Producing radiologist-quality reports for interpretable artificial intelligence][xai_rnn_radiology] (2018): a "case study",
1. [The Book of Why][tbow] (2018): The introduction and first chapter were read in detail, only the part of interest for XAI (to my judgement) is discussed here, comparison and counterfactuals. It's interesting but may be more useful in other areas (like medical sciences, economics etc.)
1. [The perils and pitfalls of explainable AI: Strategies for explaining algorithmic decision-making][perils_and_pitfalls] (2021): emphasis on socio-political aspects,
1. [Interpretable and Explainable Machine Learning for Materials Science and Chemistry][xai4mat] (2022),
1. [Principles and practice of explainable machine-learning][principles_and_practice] (2021, 25 pages): Sections 8&ndash;11 are a useful review of explainability methods.
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2024).
</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[mythos]: https://dl.acm.org/doi/10.1145/3236386.3241340

[perils_and_pitfalls]: https://www.sciencedirect.com/science/article/pii/S0740624X21001027

[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full

[shap_values]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html

[tbow]: https://en.wikipedia.org/wiki/The_Book_of_Why

[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304

[xai_rnn_radiology]: https://arxiv.org/abs/1806.00340

[xai4mat]: https://pubs.acs.org/doi/10.1021/accountsmr.1c00244

[xx]: http://arxiv.org/abs/1806.00069
