# Explanations

Let's start with a simplified definition of an _explanation_, which is then refined:

> An explanation is an answer to a _why-question_.

Other questions (e.g. _how_, _what_) &mdash;and even no question&mdash; may also prompt an explanation. For example, lessons or books which may count as explanations without defined questions.

_Why-questions_ tend to be _contrastive_, that is, phrased as _why P rather than Q_ instead of _why P_. The _foil_ (Q) may also be implicit.

Another way to think of explanations is of filling-a-gap (in imaginary or present askers), though it's an oversimplified view of the learning process.

Finally, explanations frequently occur as part of _conversations_, where social aspects play an important role. For example, follow up questions and behaviours can act like direction-signs in the journey towards an explanation.

The different question types, the _contrastive_ consideration, and the social aspects may be included in an extended definition:

> Explanations are commonly answers to _what_, _how_ and _why_ questions aiming to fill-a-gap in someone's perspective. The question may question may be implicit, requiring us to infer it.
>
> Frequently, _contrastive questions_ are successful explanation-generators because the answer can be simplified.
>
> Explanations may be part of a _communication process_ in which feedback and other queues refine both the questions and the answers.


## Characteristics of explanations

Generating explanations involve a _cognitive_ and a _social_ process. Below, I describe a version inspired by [Explanation in artificial intelligence: insights from the social sciences][explanations_social].

1. During the _cognitive process_, hypotheses / answers are retrieved or generated, for whatever is to be explained (_explanandum_).
2. Answers are compared, and one may be selected until contradicted by experience or super-seeded (e.g. by a simpler explanation). All things equal, **simple** (shorter) and **general** (wider applicability) hypotheses tend to be preferred.
3. The answer is communicated to an audience in the _social process_.

### Social Process

When an explanation is communicated, the receiver may ask be question, accept or reject the answer. The [Gricean Maxims][gricean_maxims] can aid us towards _good_ communication.

<!-- These rules can also be used as a guide for good _model explanations_. -->

- **Informative** (Quantity): right amount of context and details,
- **Truthful** (Quality, or Fidelity): Try to make it true,
- **Relevance** (Relation): do not state things that aren't needed (provide insight),
- **Manner** (clarity): express it in elegant terms.

Beyond these general aspects, any particular situation involves the asker acquiring certain knowledge, which is a learning process occurring inside the person. This isn't discussed here.

### Metaphors: The Machine and The Agent

These are metaphors different audiences use to understand models, and can help generate explanations for them.

In the scientific and science-adjacent domains, models are conceptualised as _machines_: composed of parts, each with a function, a role.

Outside of science or the technical domain, they're conceptualised as _human-like agents_: explained in human terms, expected to be reliable, consistent.

In summary, explanations are answers to _why-questions_; _good_ explanations respect the Gricean maxims, and will be dependent on the audience (their preferred style, expectations, expertise). The metaphors can help think of an explanation-style a given audience.

A table summary:

| Perspective      | Model is a… | Preferred Explanation style           | Audience            |
| ---------------- | ----------- | --------------------------- | ------------------- |
| **Scientific**   | Machine     | Mechanistic, causal, formal | Experts             |
| **Human-facing** | Agent       | Intentional, narrative      | Users, stakeholders |

Many other metaphors could be proposed.

----------------

<details>
<summary>Interesting resources</summary>

1. [Studies in the logic of explanation][logic_of_expl_hempel] (1948), all the conceptual, i.e. non algebraic/logical analysis, is interesting.
1. [Explanations, Predictions and Laws][scriven] (1948),
1. [On the mechanization of abductive logic][abductive_logic] (1973). The first page is quite interesting.
<!-- A **deduction** (proof) is e.g. "All cats are animals (I); animals are big (II); then cats are big (III)", whereas **abduction** (hypothesis) would be "III; I; maybe II" notice the _maybe_ (anti-clockwise rotation). Another anti-clockwise rotation takes us to **induction** (generalisation,hypothesis): "II; III; maybe all I". -->
1. The paper ["Explanation in artificial intelligence: insights from the social sciences"][explanations_social] (2019, 38 pages). Once the why-cause is found (diagnosis), it may be communicated, making rules of conversation relevant: [Gricean Maxims of Communication][gricean_maxims] (blog-post), or [Wikipedia's][wikipedia_gricean].
   - The definition of explanation extends previous work by Lombrozo on [The structure and function of explanations][lombrozo] (2006).
1. Blog Posts: [What is Explainable AI?][what_is_xai] (2022) and from [IBM][xai_ibm],

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[abductive_logic]:https://www.ijcai.org/Proceedings/73/Papers/017.pdf

[explanations_social]: https://www.sciencedirect.com/science/article/pii/S0004370218305988

[gricean_maxims]: https://effectiviology.com/principles-of-effective-communication/

[logic_of_expl_hempel]: https://fitelson.org/woodward/hempel_oppenheim.pdf

[^logic_of_expl_hempel]: e.g. [Studies in the logic of explanations][logic_of_expl_hempel] (1948)

[lombrozo]: https://fitelson.org/few/few_08/lombrozo_reading.pdf

[scriven]: https://fitelson.org/woodward/scriven_epl.pdf

<!-- [XAI for whom]: http://arxiv.org/abs/2106.05568 -->
[wikipedia_gricean]: https://en.wikipedia.org/wiki/Cooperative_principle
[what_is_xai]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
[xai_ibm]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
