# Explainable AI (XAI)

This post is an overview of the field of Explainable AI (XAI).

----------------

## Scope of the Field of XAI

Explainable AI (XAI) aims to _explain_ (see above) artificial intelligence models inner workings and their outputs.

Briefly, _to explain_ involves answering questions about an _explanandum_ for an audience. It involves the two processes (cognitive and social) described in the more detailed post on [explanations](./explanation.md).

_For an audience_ is more important than it may seem. An audience certain level of expertise, need such as to the know accuracy and limitations of models and goals such as answering certain kinds of questions. These aspects are encapsulated in the social process and gricean maxims.

Broadly speaking, we find two sub-fields within XAI:

- **Post Training Explainability**
    - Of the models' output or decisions,
    - Of the models' internal state, such as the role of each layer, activation, and weight.
- **Intrinsic Explainability**
    - Writing models that are constrained in some way that makes them more interpretable (independently of whether it's been trained or not.),
    - Explaining the internals and rationale of the models themselves.

Since this is a custom classification (though close to others), quotes from papers will make it clear which aspects are we mapping to it.

Explanations can also be Local or Global, referring to a single input-output (e.g. linear LIME) or to the model as a whole (e.g. combining local explanations as SP-LIME does). This post only discusses the two sub-fields above, and makes clarifications about local/global if needed.

> [!NOTE]
> The term "black box" is commonly used to refer to complex deep learning models. It can also refer to a model _unavailable for inspection_ (such as encrypted or proprietary models). In both cases, we can try to explain the outputs, but the internals can only be explained if the model is available.

This post and most papers use "black box" in the first sense: _models which are hard to comprehend_.

> [!NOTE]
> In this blogpost, _explainability_ and _interpretability_ are considered synonyms.

### Intrinsic Explainability

Intrinsic Explainability (or interpretability) refers to designing models that are constrained in form (e.g., [Rudin C.][stop_explaining_interpret_instead]) and also explaining the internals of models.

What design makes a model interpretable is domain-dependent. For example, geometric deep learning can express constraints of connectivity related to molecules and materials (e.g. GNNs);

Other strategies are: imposing physical or connectivity constraints (e.g. GNNs for molecules and materials), inductive biases (such as symmetry), CNNs for processing images (somewhat interpretable to experts), using expert-selected causal features, imposing monotonicity, sparsity or constraining model size or computational complexity.

The paper "[The Mythos of Model Interpretability][mythos]" suggests three components of _transparency_. Very briefly:

1. _Simulatability_ i.e. can mentally run the model,
2. _Decomposability_ i.e. each part of the model admits an intuitive explanation,
3. _Algorithmic training_ which focuses on global vs local minimum, error and loss, guaranteed convergence;

These are important aspects that have to be considered for models, and the emphasis on each will depend on the case.

The paper states:

> Sufficiently high-dimensional [linear] models, unwieldy rule lists, and deep decision trees could all be considered less transparent than comparatively compact neural networks.

[Rudin's paper adds][stop_explaining_interpret_instead]:

> As discussed above, interpretability usually translates in practice to a set of application-specific constraints on the model. Solving constrained problems is generally harder than solving unconstrained problems. Domain expertise is needed to construct the definition of interpretability for the domain, and the features for machine learning. For data that are unconfounded, complete, and clean, it is much easier to use a black box machine learning method than to troubleshoot and solve computationally hard problems.

_But what are examples of some algorithms for some problems? Or maybe common classes of such models?_

Rudin does mention a few pointers:

1. The human-interpretable models we had before machine learning (and some of these can be machine-learnt). Some examples from Rudin's paper, though it will be extended, are:
    - **Logical Models**[^other_names]: use logical conditions such as "or, and, if-then" but _are machine-learnt_ in a reasonable amount of time. The model may be large (non-simulatable) but the explaining condition may be brief and interpretable. Rudin calls these "smaller-than-global explanations" because the explanation is just a few rules of the global model which may have many (Appendix D). Examples: disjunctive normal form models and falling rule lists and CORELS.
    - **Sparse Linear Models**. If it uses integer coefficients is a _scoring system_.
    - **Case-Based**: they _defined interpretability_ for a specific domain, in this case computer vision, in terms of how humans explain them (by pointing at features in regions of the image). This definition led them to create a _prototype network_ ("prototype" in the Eleanor Rosch sense, a characteristic part of an image), and the network _seems to_ crop the image in multiple ways (maybe just outputs prototypical regions bounding boxes) and compare these to training prototypes for each class. The interesting thing is that _this output is the explanation itself_. Finally it does a weighted average.

2. Adequately crafted neural networks.

   or linear fits or case-based reasoning.

It's also possible to imbue interpretable aspects into deep learning models (could be interesting to expand on this aspect, maybe through mechanistic interpretability papers). At the same time, it's important to know when a traditional ML algorithm is a better fit (for interpretability, performance, accuracy).

I would also add that, in scientific disciplines, we may want _causal and interpretable models_, rather than just _interpretable_.

### Post Training Explainability

Usually this is includes extrinsic and post hoc explainability and involves explaining prediction(s), or role of layers and neurons, rather than elucidating precisely how a model works.

<!-- Sometimes they use an extra _explanation model_, but not always. -->

["Why Should I Trust You?"][lime] defines "explaining a prediction" as:

> By "explaining a prediction", we mean presenting textual or visual artifacts that provide qualitative understanding of the relationship between the instance's components (e.g. words in text, patches in an image) and the model's prediction.

This is a visual explanation of the features' contribution to the output from the same paper, where it is used to compare models:

<div class="center w60">
    <a href="../assets/LIME.png">
    <img src="../assets/LIME.png" alt="Comparison between to algorithms analysed by LIME."/>
    </a>
    <p>Image taken from <a href="https://dl.acm.org/doi/10.1145/2939672.2939778">paper</a>.</p>
</div>

They also propose an _explainer desiderata_ for the explanation model: it should be `1.` **interpretable**, by giving a qualitative understanding between inputs and outputs, making it easy to understand, `2.` **model agnostic** and `3.` **locally faithful** (a good fit to the original model in the vicinity of the instance being explained) and `4.` **globally explainable**. In that paper, SP-LIME combines local explanations to provide a _global explanation_ of the model.

[Rudin][stop_explaining_interpret_instead] argues that these simpler explanation models must be wrong. If it is globally accurate, then we don't need the original model. Rudin proposes calling these model-approximation techniques "summary of predictions", "summary statistics" or "trends".

Within other problems the paper states:

> Even an explanation model that performs almost identically to a black box model might use completely different features, and is thus not faithful to the computation of the black box.
> (...)

An explanation model depending on race could construe "This person is predicted to be arrested because they are black." (as the paper states) even if the original model did not depend on this feature directly (it could by proxy features). This would mislead a user very badly.

<!-- citing Box's maxim: "All models are wrong but some are useful" and -->
Within these limitations, methods such as SHAP, LIME can provide _some_ understanding of what the model is doing (though as stated above, they can also be misleading). [Explaining Explanations in AI][xxai] makes an analogy between local approximation and scientific models, they key part being that both may approximate a more detailed model within a narrow domain (in which they are valid).

A an issue with this analogy was noted by [Rudin][stop_explaining_interpret_instead]:

> Note that the term "explanation" here refers to an understanding of how a model works, as opposed to an explanation of how the world works. The terminology "explanation" will be discussed later; it is misleading.

<!-- The interest is usually around a particular prediction or a particular model (requiring a partial causal-rather than a full causal-chain). -->

[In Appendix C, Rudin argues][stop_explaining_interpret_instead] that choosing from one of many possible counterfactual explanations (which apparently are also called _inverse classification_!) is often undecidable:

> Some have argued that counterfactual explanations [e.g., see 37] are a way for black boxes to provide useful information while preserving secrecy of the global model. Counterfactual explanations, also called inverse classification, state a change in features that is sufficient (but not necessary) for the prediction to switch to another class (e.g., "If you reduced your debt by $5000 and increased your savings by $50% then you would have qualified for the loan you applied for"). This is important for recourse in certain types of decisions, meaning that the user could take an ac"ion to reverse a decision [61].
>
> In other words, let us say that there is more than one counterfactual explanation available (e.g., the first explanation is "If you reduced your debt by $5000 and increased your savings by $50% then you would have qualified for the loan you applied for" and the second explanation is "If you had gotten a job that pays $500 more per week, then you would have qualified for the loan"). In that case, the explanation shown to the user should be the easiest one for the user to actually accomplish. However, it is unclear in advance which explanation would be easier for the user to accomplish. In the credit example, perhaps it is easier for the user to save money rather than get a job or vice versa.

<!-- Some post-hoc XAI methods are explained in [strategies](./strategies.md). -->

### Post Hoc Methods

[Explaining Explanations in AI] states that:

> (...) first reviewing methods for producing explanations in xAI, and explain how they are generally more akin to scientific modelling than explanation giving.

Which is an important qualifier, they are more like a _toolkit to produce explanations_. They are also approximations and usually local in the sense of having a _domain of applicability_. Importantly, they are intelligible / interpretable as most scientific models are.

[The Mythos of Model Interpretability][mythos] and [Principles and practise of explaining ML models][principles_and_practice] name and review a few types of _post hoc interpretability_ (extrinsic explainability) techniques.

A similar version to those papers is given below:

- **Textual** e.g. using RNNs or a language model to translate the network state into text (trained with descriptions, similar to captioning images),
- **Similarity** (or Case-Based): Representative items for each class provide insights about the model's internal reasoning. Can be automated with distance KNNs but specific examples may require human selection.
    - They do not explicitly state what parts of the example influence the model. How do inputs from different classes compare? And same?
- **Visualizations**: of learned representations. Altering certain input features to maximise activation of a particular neuron (then looking back at the modified image to see what this neuron is responding to). Easier to communicate to non-technical audiences. Most approaches are intuitive and not hard to implement.
    - There is an upper bound on how many features can be considered at once. Humans must inspect plots to derive explanations. Class boundaries?
- **Contrastive Methods** look for similar cases that lead to a different decision, or that help clarifying the decision in some way.
They are a separate category because they may use the original model, and the key characteristic is the type of question they ask. But, as [Explaining Explanations in AI][xxai] says:
  > (...) choosing a relevant set of cases or events against which contrastive explanations are provided is not a straightforward challenge.
- **Approximations**: Simple, surrogate, interpretable models explain opaque ones, locally and/or globally. They also allow us to ask contrastive or what-if questions (see previous method) such as "What if we change X by X'?" Or "How could I get Y' rather than Y?" However, these approximation models are usually valid over a narrow domain, making many of these questions unfeasible.
    - [Explaining Explanations in AI][xxai] states:
  > These models can be understood as a "do it yourself kit" for explanations, allowing a practitioner to directly answer "what if questions" or generate contrastive explanations without external assistance.
    - **Feature relevance** can be considered a linear approximation model. They operate locally or globally (e.g. LIME and SP-LIME). These Methods may make assumptions which do not hold (e.g. feature independence, linearity).

A useful approach could be to use and compare several different these methods.

The last two classes are popular and often used in the context of **Local Explanations**, discussed in the [next post](./model_explainability_2.md).

----------------

<details>
<summary>Sources</summary>

1. [Can we open the black box of AI?][open_ai_black_box] (2016). This paper briefly explains what ANNs are, their similarities (not the differences) to the brain, and what challenges they pose to us. Primarily, the challenge is that they are hard to explain. It puts as an example a physician or patient relying in the output, but not knowing _why_ it predicts that. The author also cites Michael Tyka saying "The problem is that the knowledge gets baked into the network, rather than into us" which is also interesting.
Furthermore, there isn't a "number 5 pattern" that is the same for many networks; the pattern appears from the training procedure, and although it may be similar for all number 5, it's usually different between training runs, datasets, and networks. Similarly so for brains!
1. ["Why Should I Trust You?": Explaining the Predictions of Any Classifier][lime] (2016)
1. [The Mythos of Model Interpretability][mythos] (2018) is an excellent break down of ideas. This paper is cited and discussed in the post primarily.
1. [A Unified Approach to Interpreting Model Predictions][shap_values] (2017): paper proposing SHAP, that is, showing Shapley values as the best coefficients in linear combination of features, given 3 requirements (local accuracy, missingness and consistency),
1. [Counterfactual Explanations without Opening the Black Box: Automated Decisions and the GDPR][without_opening_bbox] (2017) which (briefly) proposes a set of unconditional counterfactual explanations in the context of GDPR (unconditional as in we can always have them); these are easier to generate and understand than the internals of a complex model, protect trade secrets and privacy (by not revealing datasets).
    - The authors also have a related paper: [Explaining Explanations in AI][xxai] (2019). **First** it review post hoc methods and makes an analogy of XAI post-hoc methods to scientific models (i.e. they are local interpretable approximations and help _generate_ explanations). **Then** answering "why-questions" requires "contrastive, selective and social" explanations. **Finally**, that an interactive, dialectic way to challenge algorithmic decisions is needed. It distinguishes "scientific explanations" addressing general phenomena with a full causal chain from "everyday explanations" addressing particular facts with partial causal chains.
[Explaining Explanations: An Overview of Interpretability of Machine Learning][xx] (2018),
1. [Producing radiologist-quality reports for interpretable artificial intelligence][xai_rnn_radiology] (2018): a "case study",
1. [The Book of Why][tbow] (2018): The introduction and first chapter were read in detail, only the part of interest for XAI (to my judgement) is discussed here, comparison and counterfactuals. It's interesting but may be more useful in other areas (like medical sciences, economics etc.)
1. [Stop Explaining Black Box Machine Learning Models for High Stakes Decisions and Use Interpretable Models Instead][stop_explaining_interpret_instead] (2019).
   <!-- - Suggests post-hoc models are worse than interpretable/transparent ones for high-stakes scenarios. It also states that the definitions of "Interpretable" varies for each field (references removed): -->
   <!-- > Interpretability is a domain-specific notion, so there cannot be an all-purpose definition. Usually, however, an interpretable machine learning model is constrained in model form so that it is either useful to someone, or obeys structural knowledge of the domain, such as monotonicity, causality, structural (generative) constraints, additivity, or physical constraints that come from domain knowledge. Interpretable models could use case-based reasoning for complex domains. -->
   - Discusses problems with post-hoc explainability: `1.` There is a trade-off between interpretability and accuracy; also that `2.` Explanation models (e.g. SHAP, LIME) provide faithful explanations of black-box models (and that a better term to "explanations" is "summary statistics" or "trend"), finally that `3.` The explanations are detailed enough (Saliency Maps) and so forth.
   - And challenges towards Interpretable AI: `1.` Black boxes shields companies from accountability (incentives); `2.` Interpretable models are harder to construct and optimise (require more expertise). `3.` Belief DL models can uncover patterns that interpretable models wouldn't find (the issue is the belief).

1. [The perils and pitfalls of explainable AI: Strategies for explaining algorithmic decision-making][perils_and_pitfalls] (2021): emphasis on socio-political aspects,
1. [Why black box machine learning should be avoided for high-stakes decisions, in brief][interpretable_ml] (2022),
1. [Interpretable and Explainable Machine Learning for Materials Science and Chemistry][xai4mat] (2022),
1. [Principles and practice of explainable machine-learning][principles_and_practice] (2021, 25 pages): Sections 8&ndash;11 are a useful review of explainability methods.
1. [Scientific discovery in the age of artificial intelligence][ai_aided_discovery] (2023).
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2024).

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->
[ai_aided_discovery]: https://www.nature.com/articles/s41586-023-06221-2

[without_opening_bbox]: https://arxiv.org/abs/1711.00399

[interpretable_ml]: https://www.nature.com/articles/s43586-022-00172-0

[lime]: https://dl.acm.org/doi/10.1145/2939672.2939778

[mythos]: https://dl.acm.org/doi/10.1145/3236386.3241340

[open_ai_black_box]: http://www.nature.com/news/can-we-open-the-black-box-of-ai-1.20731

[perils_and_pitfalls]: https://doi.org/10.1016/j.giq.2021.101666

[principles_and_practice]: https://www.frontiersin.org/journals/big-data/articles/10.3389/fdata.2021.688969/full

[shap_values]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html

[stop_explaining_interpret_instead]: http://arxiv.org/abs/1811.10154

[tbow]: https://en.wikipedia.org/wiki/The_Book_of_Why

[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304

[xai_rnn_radiology]: https://arxiv.org/abs/1806.00340

[xai4mat]: https://pubs.acs.org/doi/10.1021/accountsmr.1c00244

[xx]: http://arxiv.org/abs/1806.00069

[xxai]: https://dl.acm.org/doi/10.1145/3287560.3287574

<!-- [^extr_intr]: Intrinsic explainability is also called "Transparency", "Inherently interpretable models"; Extrinsic explainability is also called "black boxedness", post-hoc explainability, opaqueness. -->
[^other_names]: related names are: rule lists, expert systems, decision trees, disjunctive normal form models, associative classifiers.
