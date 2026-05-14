# Explanations

_What is the goal here? The goal is use ideas about explanations from the social sciences (this post) to analyse and build explanation-tools for other researchers, and for ordinary people (following posts)._

<!-- _What is the goal here?_ The idea is, first, to build a foundation on general aspects of explanations; second, to use these insights to explain classic and deep learning algorithms; and third to enable us to analyse &mdash;and even build&mdash; explanation tools for other researchers, and for ordinary people). -->
<!---->
<!-- For example: Can we create a deep learning model, or a model-explanation algorithm that best fits ordinary people's requirements? Can we adapt pre-existing ones for this purpose? Can we create or adapt models or explanation models that are suitable for specific audiences (with different requirements)? When can we trade _truth_ or _accuracy_ of an explanation, for _simplicity_? -->

<!-- All these questions serve us in creating new tools and ideas for explaining deep-learning models for different audiences (with different needs, prior knowledge, and so forth). -->

--------------

In most explanations, there is an object that needs clarification, called the _explanandum_.

Explanations may be _interactive_ (e.g. in a conversation), _static_ (a book), or a mix of both. For the latter, consider machines with pre-set questions and answers stored, where the audience can't always ask what it needs.

_Static explanations_ are descriptions aiming to clarify the _explanandum_, and may be found as written text, videos or other formats.

_Interactive explanations_ are a communication process in which an communicator interacts with an audience, with the objective of resolving _what_, _how_ or _why_ questions posed by the audience.

We may consider that interactive explanations are static explanations updated in real time by follow-up questions, behaviour, and other kind of feedback.

The success of an explanation depends on audience (e.g. prior knowledge, interests, needs given by the context, and so forth).

Even though there are general characteristics, we should remember that explanations are for an audience, and in some context.

## The explanation process

Explanations involve a _cognitive_ and a _social_ process. Below, I describe a version inspired by [Explanation in artificial intelligence: insights from the social sciences][explanations_social].

1. During the _cognitive process_, hypotheses / answers are retrieved or generated, for the phenomenon to be explained (the explanandum).
2. Answers are compared, and one may be selected until contradicted by experience or superseeded (e.g. by a simpler explanation). All else being equal, **simple** (shorter) and **general** (wider applicability) hypotheses tend to be preferred.
3. The answer is communicated to an audience in the _social process_.

### Social Process

When an explanation is communicated, the receiver may ask a question, accept or reject the answer. The [Gricean Maxims][gricean_maxims] can aid us towards _good_ communication.

<!-- These rules can also be used as a guide for good _model explanations_. -->

- **Informative** (Quantity): right amount of context and details,
- **Truthful** (Quality, or Fidelity): the explanation should be true,
- **Relevance** (Relation): avoid irrelevant details, focus on what provides insight,
- **Manner** (clarity): express it in elegant terms.

Beyond these general aspects, any particular situation involves the asker acquiring certain knowledge, which is a learning process occurring inside the person. This isn't discussed here.

## Explanation success

This section explores certain aspects of explanations that are usually preferred by most audiences.

### Understanding the difference

Research has shown that _why-questions_ are usually _contrastive_. That is, they are phrased as _Why P rather than Q?_ instead of simply _Why P?_. It's easy to remember it as a "reality (P) vs expectation (Q)" case.

The _fact_ that requires explanation is "P"; the _foil_ is "Q", and represents the case that was expected &mdash;which may also be implicit. The _foil_ can aid explanation-generation. The reason for this is that answering a contrastive question can focus on the difference between the two cases, which is usually easier.

As [Section 3-1][beware_inmates_asylum] states:
> For example, explaining "Why did Mr. Jones open the window?" with the response "Because he was hot" is not useful if the implied foil is Mr. Jones turning on the air conditioner, as this explains both the fact and the foil; or if the implied foil was why Ms. Smith, who was sitting closer to the window, did not open it instead, as the cited cause does not refer to a cause of Ms. Smith's lack of action.

### Attributing Causes

As [Miller et al. state][beware_inmates_asylum]:

> Attribution theory is the study of how people attribute causes to events; something that is necessary to provide explanations.

_Causal attribution_ and _explanation selection_ are summarised below (based on the same paper).

Humans **attribute causes** using either:

- Agent-like model, using intentions, which are more relevant in agent-like AI,
- A general causal model, involving counterfactual reasoning (what would have happened in an alternative case, usually evidenced by the _foil_.)

_But which events to undo or change?_ Social research indicates that we prefer:

- Proximal over distal causes (in the causal chain of events);
- Focus on abnormal events and human intervention (these may be more distal in this causal chain);
- Focus on _controllable_ events.

These heuristics can be used to simplify and/or prioritise explanations.

### I like THIS explanation (evaluation)

Notably, truth isn't always preferred; rather, usefulness, simplicity, generality and consistency with prior knowledge are. Many of these results come from work by Tania Lombrozo.

## Explaining, teaching and learning

We could argue that the explainer is modelling what the explainee doesn't know, aided by behavioural cues, follow-up questions and other forms of feedback. In this sense, explaining is similar to both teaching and learning.

We could say "_filling a gap_" instead of "_guide_" but this comes from an outdated pedagogical view of the learning process (which explanations may involve), based on _knowledge transfer_.

Other views come from _constructivism_ (Piaget) or _constructionism_ (Papert e.g. "Mindstorms", Resnick "Lifelong kindergarten") where the learning process is _active_ and goes through _accommodation_.

More modern views include _connectivism_ (based on connectionism).

Neither of these perspectives nor learning itself are discussed here, but it may be added in a future post.

## Metaphors: The Machine and The Person

These are metaphors different audiences use to understand complex systems, and can help generate explanations for them.

In technical fields, many complex systems are conceptualised as _machines_: composed of parts, each with a function, a role. Many are also conceptualised as graphs.

Ordinary people conceptualise certain kinds of complex systems as humans or agents (wholly or in part). This may happen with systems using human language or behaving autonomously, but other times it is due to pragmatic reasons. They would use and expect the kind of explanation a human would give, if there were one.

This idea is very similar to _social_ versus _general_ causal attribution. It is also similar to what [researchers hypothesise][autonomous_intelligent_systems]:

> For those intentional agents, we hypothesize, people will apply the same conceptual framework of behavior explanation that they apply to humans; and they will expect AIS [Autonomous Intelligent System] to apply this framework as well. There may be a subset of AIS that people do not regard as intentional agents; and for those, they may apply a purely mechanical explanatory framework.

In summary, explanations are often answers to _why-questions_; _good_ explanations respect the Gricean maxims, and will be dependent on the audience (their preferred style, expectations, expertise). The metaphors can help think of an explanation style a given audience.

A table summary:

| Perspective      | Model is a… | Preferred Explanation style           | Audience            |
| ---------------- | ----------- | --------------------------- | ------------------- |
| **Scientific**   | Machine     | Mechanistic, causal, formal | Experts             |
| **Human-facing** | Agent       | Intentional, narrative      | Users, stakeholders |

Many other metaphors could be proposed.

--------------

<details>
<summary>Interesting resources</summary>

1. [Studies in the logic of explanation][logic_of_expl_hempel] (1948), Their _logically deductive_ model, and the related _covariation_ model (Kelley, 1967) isn't how human explanations are considered in social and cognitive sciences any more. However, these are important historical background.
1. [Explanations, Predictions and Laws][scriven] (1948),
1. [On the mechanization of abductive logic][abductive_logic] (1973). The first page is quite interesting.
<!-- A **deduction** (proof) is e.g. "All cats are animals (I); animals are big (II); then cats are big (III)", whereas **abduction** (hypothesis) would be "III; I; maybe II" notice the _maybe_ (anti-clockwise rotation). Another anti-clockwise rotation takes us to **induction** (generalisation,hypothesis): "II; III; maybe all I". -->
1. [Explainable AI: Beware of Inmates Running the Asylum Or: How I Learnt to Stop Worrying and Love the Social and Behavioural Sciences][beware_inmates_asylum] (2017): Section 1 describes what the wrong approach is: building explanation models with an idea of explanation that only applies to experts. Section 2 surveys papers and notes almost none uses insights from social science of explanation to build their XAI algorithms, and even less evaluate them on humans. Section 3 is the most useful, and describes **which insights from social sciences could be used** (and points to research).
   - And an extension of that work ["Explanation in artificial intelligence: insights from the social sciences"][explanations_social] (2019, 38 pages).
   - Once the why-cause is found (diagnosis), it may be communicated, making rules of conversation relevant: [Gricean Maxims of Communication][gricean_maxims] (blog-post), or [Wikipedia's][wikipedia_gricean].
   - The definition of explanation extends previous work by Lombrozo on [The structure and function of explanations][lombrozo] (2006).
1. [How People Explain Action (and Autonomous Intelligent Systems Should Too)][autonomous_intelligent_systems] (2017),
1. Blog Posts: [What is Explainable AI?][what_is_xai] (2022) and from [IBM][xai_ibm].

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[abductive_logic]:https://www.ijcai.org/Proceedings/73/Papers/017.pdf

[autonomous_intelligent_systems]: https://aaai.org/papers/16009-16009-how-people-explain-action-and-autonomous-intelligent-systems-should-too/

[beware_inmates_asylum]: http://arxiv.org/abs/1712.00547

[explanations_social]: https://www.sciencedirect.com/science/article/pii/S0004370218305988

[gricean_maxims]: https://effectiviology.com/principles-of-effective-communication/

[logic_of_expl_hempel]: https://fitelson.org/woodward/hempel_oppenheim.pdf

[lombrozo]: https://fitelson.org/few/few_08/lombrozo_reading.pdf

[scriven]: https://fitelson.org/woodward/scriven_epl.pdf

<!-- [XAI for whom]: http://arxiv.org/abs/2106.05568 -->
[wikipedia_gricean]: https://en.wikipedia.org/wiki/Cooperative_principle
[what_is_xai]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
[xai_ibm]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
