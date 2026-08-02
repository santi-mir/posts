# Explanations

_What is the goal of this post? The goal is to describe ideas about "explanations" from the social sciences._

In future posts, explanation-tools for two different audiences &mdash;researchers and ordinary people&mdash; will be analysed.

<!-- For example: Can we create a deep learning model, or a model-explanation algorithm that best fits ordinary people's requirements? Can we adapt pre-existing ones for this purpose? Can we create or adapt models or explanation models that are suitable for specific audiences (with different requirements)? When can we trade _truth_ or _accuracy_ of an explanation, for _simplicity_? -->

--------------

## Definitions

Explanations may be _interactive_ (a conversation), _static_ (a book), or a mix of both. In most explanations there is _that which needs clarification_, called the _explanandum_.

- **Static explanations**: descriptions aiming to clarify the _explanandum_, and may be found as written text, videos or other formats.
- **Interactive explanations**: a communicator and an audience interact aiming to resolve _what_, _how_ or _why_ questions posed by the audience.
- **Mix**: consider machines with pre-set questions and answers, where the audience can't always ask what it needs.

<!-- Interactive explanations are similar to static explanations, just updated in real time by follow-up questions, behaviour, and other kind of feedback. -->

> [!NOTE]
> Understanding is having a theory or idea about how something works. Usually we refine these with experience. So it is a prerequisite for an explanation.

It is also interesting to note that humans explain phenomena in the world, but don't have access to our brain's detailed processes, nor do others. Maybe this is an interesting heuristic to apply to non-human agents.

## The explanation process

Explanations involve a _cognitive_ and a _social_ process. The version below was inspired by [Explanation in artificial intelligence: insights from the social sciences][explanations_social].

1. During the _cognitive process_, hypotheses (e.g. causal connections) are generated aiming to clarify the _explanandum_.
   - Hypotheses are then compared, and one may be selected until contradicted by experience or superseeded (e.g. by a simpler explanation).
2. During the _social process_, the answer is communicated to an audience.

The process may iterate and update during the interaction (or not, in a static explanation). For example, the _explanandum_ may be refined.

Note: the problems of causal _connection_ and _selection_ (`1.`) are well known in psychology.

## Contrastive Questions

Research has shown that _why-questions_ are usually _contrastive_. That is, they are phrased as _Why P rather than Q?_ instead of simply _Why P?_. It's easy to remember it as a "reality (P) vs expectation (Q)" case.

The _fact_ that requires explanation is "P"; the _foil_ is "Q", and represents the case that was expected &mdash;which may also be implicit. The _foil_ can aid explanation-generation. The reason for this is that answering a contrastive question can focus on the difference between the two cases, which is usually easier to answer than the case separately.

As [Section 3-1][beware_inmates_asylum] states:
> For example, explaining "Why did Mr. Jones open the window?" with the response "Because he was hot" is not useful if the implied foil is Mr. Jones turning on the air conditioner, as this explains both the fact and the foil; or if the implied foil was why Ms. Smith, who was sitting closer to the window, did not open it instead, as the cited cause does not refer to a cause of Ms. Smith's lack of action.

Another way to state this by [Hesslow][causal_selection_problem]:

> What I want to suggest, then, is that the explanandum should be construed as a relation which involves three things: an _object a_, an _object of comparison b_ and an _explanandum property E_ which a has and b does not have.

### Relevant Causes

We never provide causal chains (it's infinite), but a small-enough one that explains the event in question (this is the _causal selection problem_).

Researchers have pointed out many heuristics used: proximal over distal events (in the causal chain of events); abnormal or unexpected events; controllable events, deviation from theoretical ideals, model, predictive power, responsibility, and so forth.

But those are taken care of by _contrastive why-questions_ which compare the event to be explained to a reference case (particular instance or general case). In this regard, [Hesslow][causal_selection_problem] states (bold is mine):

> Many of the selection criteria listed in Section 3 can be construed as the result of **choosing different objects of comparison or reference classes**. Let us consider again the fire in the barn, and let us suppose that we have in the back of our minds the picture of a normal barn. (...) the normal barn has not caught fire, it follows that an explanatorily relevant condition for this barn's catching fire must be abnormal. Thus, selection of **abnormal conditions** can be viewed as the result of comparing the explanandum object with a normal object.

And also most other causal selections are contained:

> (...) the difference between this barn now and this barn yesterday, i.e. we would be selecting a **precipitating** cause [proximal in the list above]. Selection of the **unexpected** may be viewed as the result of explaining the difference between an expected and an actual outcome. Selection according to **responsibility** follows from a comparison between actual and morally ideal behaviour. Selection of conditions which cause a **deviation from a theoretical ideal** involves a comparison between an actual and a theoretically ideal situation, and so on (cf. Hesslow, 1983).

Here is yet another illustration by Hesslow, of how contrasts cases narrow down possible causes:

> For instance, if we want to explain why the fly Ml has shorter wings than Nl, then the temperature in which the flies were raised is explanatorily irrelevant, since the temperature was the same in both cases. The mutated gene on the other hand was present in one case and absent in the other.It is, therefore, explanatorily relevant.

### Pragmatism

Notably, accuracy may not be preferred in an explanation; rather, usefulness, simplicity, generality and consistency with prior knowledge are.

Many of these results come from work by Tania Lombrozo. (This section will eventually be expanded.)

## Social Process (Communication)

The communication can be aided by the [gricean maxims][gricean_maxims]: rules of _effective_ communication.

- **Informative** (Quantity): right amount of context and details,
- **Truthful** (Quality, or Fidelity): the explanation should be true,
- **Relevance** (Relation): avoid presumed-known or superfluous details, focus on what provides insight,
    - One example given earlier is to focus on unexpected events, whilst ignoring what is presumed to be known by the listener.
- **Manner** (clarity): express it in elegant terms.

In some cases, humans also tend to prefer concrete over abstract explanations, so "concreteness" could be added to the list.

_Relevance_ is primarily related to the _causal selection problem_, as [how-people-explain-action-and-autonomous-intelligent-systems-should-too][Malle et al state]:

> How do people solve this problem? They determine what exact question the audience is interested in (McClure and Hilton 1998); they take into account what their audience member already knows (Slugoski et al. 1993); and they offer elements of explanations that build bridges between presumed knowledge and novel information (Korman and Malle 2016). In short, they offer explanations that generate coherence in a knowledge structure of old and new information (Thagard 1989).

_Contrastive explanations_ take care of many of these aspects automatically.

## Metaphors: The Machine and The Person

As [Miller et al. state][beware_inmates_asylum]:

> Attribution theory is the study of how people attribute causes to events; something that is necessary to provide explanations.

Humans **attribute causes** using either:

- **Agent-like model** Explanation uses goals, motives, duties to justify intentional actions or behaviour.
    - _Unintentional_ behaviour is usually explained using the next type.
- **General causal model** explain outcomes by counterfactual reasoning or contrastive explanations.

These basically define _modes_ of explanation.

In technical fields, many complex systems are conceptualised as _machines_: composed of parts, each with a function, a role. Many are also conceptualised as graphs.

Ordinary people conceptualise certain kinds of complex systems as humans or agents (wholly or in part). This may happen with systems using human language or behaving autonomously, but other times it is due to pragmatic reasons. They would use and expect the kind of explanation a human would give, if there were one.

This is similar to what [researchers hypothesise][autonomous_intelligent_systems]:

> For those intentional agents, we hypothesize, people will apply the same conceptual framework of behavior explanation that they apply to humans (...) a subset of AIS that people do not regard as intentional agents; and for those, they may apply a purely mechanical explanatory framework.

| Perspective      | Model is a… | Preferred Explanation style           | Audience            |
| ---------------- | ----------- | --------------------------- | ------------------- |
| **Scientific**   | Machine     | Mechanistic, causal, formal | Experts             |
| **Human-facing** |Agent/Person | Intentional, narrative      | Users, stakeholders |

Other metaphors could be proposed.

<!-- ## Explaining is Teaching -->
<!---->
<!-- The communicator models what the audience doesn't know, and receives feedback. In this sense, the communicator teaches and the audience learns. (The communicator needn't be the expert, but aside from that, they seem very similar.) -->
<!---->
<!-- The communication process is at times like "_filling a gap_" in the audience's understanding. (An outdated pedagogical view of the learning process based on _knowledge transfer_.) -->
<!---->
<!-- Other views come from _constructivism_ (Piaget) or _constructionism_ (Papert e.g. "Mindstorms", Resnick "Lifelong Kindergarten") where the learning process is _active_ and goes through _accommodation_. -->
<!---->
<!-- More modern views include _connectivism_ (based on connectionism). -->
<!---->
<!-- This is a fascinating and related topic, but currently not discussed in the posts. -->
<!---->

--------------

<details>
<summary>Sources</summary>

1. [Studies in the logic of explanation][logic_of_expl_hempel] (1948), Their _logically deductive_ model, and the related _covariation_ model (Kelley, 1967) isn't how human explanations are considered in social and cognitive sciences any more. However, these are important historical background.
1. [Explanations, Predictions and Laws][scriven] (1948),
1. [On the mechanization of abductive logic][abductive_logic] (1973). The first page is quite interesting.
1. [The Problem of Causal Selection][causal_selection_problem] (1988) fascinating and easy-to-read article.
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

[causal_selection_problem]: https://www.researchgate.net/publication/232592695_The_problem_of_causal_selection

[explanations_social]: https://www.sciencedirect.com/science/article/pii/S0004370218305988

[gricean_maxims]: https://effectiviology.com/principles-of-effective-communication/

[logic_of_expl_hempel]: https://fitelson.org/woodward/hempel_oppenheim.pdf

[lombrozo]: https://fitelson.org/few/few_08/lombrozo_reading.pdf

[scriven]: https://fitelson.org/woodward/scriven_epl.pdf

<!-- [XAI for whom]: http://arxiv.org/abs/2106.05568 -->
[wikipedia_gricean]: https://en.wikipedia.org/wiki/Cooperative_principle
[what_is_xai]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/
[xai_ibm]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/

<!-- A **deduction** (proof) is e.g. "All cats are animals (I); animals are big (II); then cats are big (III)", whereas **abduction** (hypothesis) would be "III; I; maybe II" notice the _maybe_ (anti-clockwise rotation). Another anti-clockwise rotation takes us to **induction** (generalisation,hypothesis): "II; III; maybe all I". -->
