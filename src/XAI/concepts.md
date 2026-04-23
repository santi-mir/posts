# Explanations

Explanations are usually defined as answers to a _why-question_, with certain properties and structure. There are definitions extending the _question-type_, and more flexible in terms of what counts as an answer.

## Characteristics of explanations

Explanations can be characterised as a:

1. _Cognitive process_: the process of finding an answer; we can expand it (if the answer is already known, only `5.` is needed):
  1. There is _something_ to explain (_explanandum_),
  2. The explainer _filters_ aspects of the _explanandum_ deemed relevant (using prior knowledge),
  3. _Generates_ possible answers (through explanation techniques),
  4. _Weight_ the likelihood of each hypotheses,
  5. Possibly selecting the most likely until contradicted by experience or super-seeded (e.g. by a simpler explanation),
2. _Product_: the answer, as in the prior definition,
3. _Social process_: The answer must then be communicated, and there are expectations about it. [Gricean Maxims][gricean_maxims] are rules observed in _good_ communication. These rules can also be used as a guide for good _model explanations_:
   - **Informative** (Quantity): right amount of context and details,
   - **Truthful** (Quality, or Fidelity): Try to make it true,
   - **Relevance** (Relation): do not state things that aren't needed (provide insight),
   - **Manner** (clarity): express it in elegant terms.

Which is a customised version of [Explanation in artificial intelligence: insights from the social sciences][explanations_social].

Importantly, the paper above notes that _why-questions_ are usually **contrastive questions** e.g. phrased as _why P rather than Q_ instead of _why P_, where the _foil_ (Q) is frequently implicit.

## Explanatory success

There are aspects that tend to make explanations more successful:

- **Simplicity**: if it involves a shorter chain of causes, it is preferred,
- **Generality**: if it explains other cases, it is preferred,
- **Prior knowledge/beliefs**
    - Conditions generation and veto of hypotheses. For example, "The drawer slides because it wants." may be ignored in different basis. Another illustrative example from [The structure and function of explanations][lombrozo]:
    > (...) If told that herring and tuna have a disease, naive participants are more likely to extend the property to wolffish, the more similar item, than to dolphins. However, among fishing experts, who can generate an explanation for why the property might hold (e.g. tuna contract the disease by eating infected herring), similarity is less predictive of property extensions. (...)

    - Aids selecting what seems causally / explanatory relevant from what is not. Consider two light beams interfering on a Sunday. The day is irrelevant (usually), we disregard a confounding factor.

I don't have much to say about _product_ (`2.`), so we jump to `3`.

## Causal Inference

Defining _cause_ has been a topic of debate.

Two important definitions of _cause_ are usually attributed to Hume: regularity and counterfactual.

- **Regularity**: things that occur together, or are always followed one after another. Confuses it with _correlation_.
- **Counterfactuals**: imaginary situation negating (countering) the fact: _What would have happened with Y, had X not happened?_. In that case $X$ causes $Y$ (in a necessary or sufficient manner) if $Y$ is reduced.

In statistics, one could say that $X$ causes $Y$ if $P(Y|X, k) > P(Y)$ i.e. it _increases_ its probability, keeping any other variables ($k$) constant. This and counterfactuals are common conceptions.

The AI researcher Judea Pearl, whose aim was to create thinking machines, proposed a framework to think about causes:

1. Use a causal diagram: a graph made from prior causal knowledge, or find out doing an experiment,
2. Use a query language: a mathematical expression of what we want to know, which an engine then translates (using the diagram) into a statistics formula.

Briefly put, ladder's steps are:
- _Association_: relating raw-data with no causal information.
- _Intervention_: changing one variable to detect the causal relation , this is, doing an experiment. He wrote this as $P(Y|do(X))$, which is then translated into a statistics formula.
- _Imagination_: involves counterfactual thinking, that is, thinking what would happen in the opposite world.[^1] What would have happened with his life expectancy, had Joe _not_ taken the drug?

How does all this relate to science or deep learning? An expert may frequently select inputs-outputs to a model which are _known causes-effects_. Then the models _do_ learn something like causal inference (though the graph is external in a sense).

For a non-expert, how does him/her know which columns (say form CSV tables) are inputs and which are outputs? Are those inputs are _actual_ causes and not just predictors? This can cause issues down the line, since knowing which are causes and effects is critical in many cases.

That is where having a causal graph is relevant for modelling.

Counterfactuals then, can be used in DL models as long as the inputs are known causes! This is in fact what counterfactual-methods for explainability: asking _what if this input was used instead_ and such counterfactual questions.


## Metaphors

<details><summary>The Machine and The Agent (click to open)</summary>

In the scientific and science-adjacent domains, models are conceptualised as _machines_: composed of parts, each with a function, a role.

Outside of science or the technical domain, they're conceptualised as _human-like agents_: explained in human terms, expected to be reliable, consistent.

In summary, explanations are answers to _why-questions_; _good_ explanations respect the Gricean maxims, and will be dependent on the audience (their preferred style, expectations, expertise). The metaphors can help think of an explanation-style a given audience.

A table summary:

| Perspective      | Model is a… | Preferred Explanation style           | Audience            |
| ---------------- | ----------- | --------------------------- | ------------------- |
| **Scientific**   | Machine     | Mechanistic, causal, formal | Experts             |
| **Human-facing** | Agent       | Intentional, narrative      | Users, stakeholders |

Many other metaphors could be proposed.

</details>

------------

<details>
<summary>Interesting resources</summary>

1. [Studies in the logic of explanation][logic_of_expl_hempel] (1948),
1. [Explanations, Predictions and Laws][scriven] (1948),
1. [On the mechanization of abductive logic][abductive_logic] (1973). The first page is quite interesting.
<!-- A **deduction** (proof) is e.g. "All cats are animals (I); animals are big (II); then cats are big (III)", whereas **abduction** (hypothesis) would be "III; I; maybe II" notice the _maybe_ (anti-clockwise rotation). Another anti-clockwise rotation takes us to **induction** (generalisation,hypothesis): "II; III; maybe all I". -->
1. [A Unified Approach to Interpreting Model Predictions][shap_values] (2017): paper proposing SHAP, that is, showing Shapley values as the best coefficients in linear combination of features, given 3 requirements (local accuracy, missingness and consistency),
1. [Explaining Explanations: An Overview of Interpretability of Machine Learning][xx] (2018),
1. [Producing radiologist-quality reports for interpretable artificial intelligence][xai_rnn_radiology] (2018): a "case study",
1. The paper ["Explanation in artificial intelligence: insights from the social sciences"][explanations_social] (2019, 38 pages). Once the why-cause is found (diagnosis), it may be communicated, making rules of conversation relevant: [Gricean Maxims of Communication][gricean_maxims] (blog-post), or [Wikipedia's][wikipedia_gricean].
   - The definition of explanation extends previous work by Lombrozo on [The structure and function of explanations][lombrozo] (2006).
1. [The perils and pitfalls of explainable AI: Strategies for explaining algorithmic decision-making][perils_and_pitfalls] (2021): emphasis on socio-political aspects,
1. [Interpretable and Explainable Machine Learning for Materials Science and Chemistry][xai4mat] (2022),
1. Blog Posts: [What is Explainable AI?][what_is_xai] (2022) and from [IBM][xai_ibm],
1. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][using_shap_lime] (2024).

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[abductive_logic]:https://www.ijcai.org/Proceedings/73/Papers/017.pdf
[explanations_social]: https://www.sciencedirect.com/science/article/pii/S0004370218305988
[gricean_maxims]: https://effectiviology.com/principles-of-effective-communication/
[logic_of_expl_hempel]: https://fitelson.org/woodward/hempel_oppenheim.pdf
[lombrozo]: https://fitelson.org/few/few_08/lombrozo_reading.pdf
[perils_and_pitfalls]: https://www.sciencedirect.com/science/article/pii/S0740624X21001027
[shap_values]: https://proceedings.neurips.cc/paper/2017/hash/8a20a8621978632d76c43dfd28b67767-Abstract.html
[scriven]: https://fitelson.org/woodward/scriven_epl.pdf
[using_shap_lime]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304
<!-- [XAI for whom]: http://arxiv.org/abs/2106.05568 -->
[wikipedia_gricean]: https://en.wikipedia.org/wiki/Cooperative_principle
[what_is_xai]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
[xai4mat]: https://pubs.acs.org/doi/10.1021/accountsmr.1c00244
[xai_ibm]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
[xai_rnn_radiology]: https://arxiv.org/abs/1806.00340
[xx]: http://arxiv.org/abs/1806.00069

[^1]:  Since a fact is in the past, it is always retrospective thinking. Planning and predicting involves considering many possibilities, and both involve simulating situations. It's interesting to imagine future-situation thinking as synthesizing a reference situation, and "counter-reference" to it as a tool for planning, predicting. For a robot though, the issue would be how to construct this initial situation (which will involve a lot of its history, past experience etc. maybe things like LLMs are good at this.)
