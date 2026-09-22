# Explanations

This post describes what _explanations_ are in the context of artificial intelligence.

--------------

## Definition

_What is an explanation?_ They more than the presentation of causes, but that is an essential aspect. Here is definition from "[How People Explain Action (and Autonomous Intelligent Systems Should Too)][autonomous_intelligent_systems]" (2017):

> Explanation is arguably a three-value predicate: someone, a communicator, explains something to someone, an audience. The success of an explanation therefore depends on several critical audience factors—assumptions, knowledge, and interests that an audience has when decoding the explanation.

<!-- That's a step forwards. But what is _explains_? -->

[Explaining Explanations in AI][xxai] also defines of explanations and explanation in AI:

> (...) "explanation" refers to numerous ways of exchanging information about a phenomenon, in this case the functionality of a model or the rationale and criteria for a decision, to different stakeholders (Lipton, 2016; Miller, 2017).

Inspired by [Explanation in artificial intelligence: insights from the social sciences][explanations_social], this post defines _explanation_ as:

> **Explanation**
>
> A two-step process involving `1.` the generation of explanatory hypotheses (cognitive process) and `2.` the communication to an audience (social process) possibly including ourselves. The process may repeat indefinitely.

Explaining can evidentiate a lack (or illusion) of understanding, and also improve understanding. Eventually, one best hypothesis may be selected until contradicted by experience, superseded by a simpler one, or shown to be inconsistent with prior knowledge.

The hypothesis (formed in the _cognitive process_) reflects our understanding: Understanding is having a theory, hypothesis or model about how something works (cognitive process).

Everyday explanations tend to be _contrastive_ as this helps to reduce the length of the causal chain; _selective_, which helps to focus on what is most relevant for the explainee; and _social_ or interactive. All three characteristics will be discussed in this post.

In the case of _AI-models_ (either approximations or the original ones) we may also require to know the limitations, domain of applicability, accuracy and other model characteristics.

## Contrastive and Causal Explanations

_Causal explanations_ (or causal hypotheses) can be given in terms of counterfactuals. As [Explaining Explanations in AI][xxai] states:

> In short, contrastive theories argue that causal explanations inevitably involve appeal to a counterfactual case, be it a cause or event, which did not occur. A canonical example is provided by Lipton Lipton (1990): "To explain why P rather than Q, we must cite a causal difference between P and not-Q, consisting of a cause of P and the absence of a corresponding event in the history of not-Q".

They can also be given via other terms (intervention and observation/association, as in the 3 steps of the Ladder of Causation).

_Contrastive explanations_ don't require counterfactuals, but contrastive _why-questions_ are asking for a cause (causal explanation) and can be answered via counterfactuals. I call these **causal-contrastive** explanations and questions (next section). Their defining characteristic seems that comparison plays an important role in the answer (and in the question though it may be implicit).

However, they can be given via counterfactuals since they also involve comparison. They can also be given via other means.

We can have also functional or mechanistical explanations relying on contrasts, which are not causal.

### Causal-contrastive Explanations and Questions

Causal-contrastive explanation from causal-contrastive _why-questions_  involve assigning a cause (part of _attribution theory_) aided by a contrast.

Causal-contrastive questions are phrased as _Why P rather than Q?_ instead of simply _Why P?_ Usually P is the real case (or fact) and Q the expected case (or foil), which may also be implicit.

These are _sometimes_ answered via counterfactuals. _But what are counterfactuals?_ If X leads to both P and Q, then it can't help to explain why only one occurred. So we want a case where P needs X to have happened, Q could happen if and only if X wouldn't have happened. Or briefly: X leads to P and only ~X can leads to Q.

The paper [Beware of Inmates Running the Asylum][beware_inmates_asylum] has an interesting example:

> For example, explaining "Why did Mr. Jones open the window?" with the response "Because he was hot" is not useful if the implied foil is Mr. Jones turning on the air conditioner, as this explains both the fact and the foil; or if the implied foil was why Ms. Smith, who was sitting closer to the window, did not open it instead, as the cited cause does not refer to a cause of Ms. Smith's lack of action.

The _foil_ focuses the explanation on "What leads to P and not to Q". Similarly it ignores what leads to both. This is usually easier to explain than the standalone fact P.
<!-- , and can also reduce confusion. -->

### More on Contrastive Questions and Explanations

[Hesslow][causal_selection_problem] states:

> What I want to suggest, then, is that the explanandum should be construed as a relation which involves three things: an _object a_, an _object of comparison b_ and an _explanandum property E_ which a has and b does not have.

The complexity, of course, lies on formulating a question that makes the important difference with a reference case obvious.

In many cases, the complexity is finding a good, relevant foil. As [Explaining Explanations in AI][xxai] states:

> However, choosing a relevant set of cases or events against which contrastive explanations are provided is not a straightforward challenge. The way in which information is transferred has a substantial impact on the quality and psychological acceptability of explanations (Hilton, 1990).

The last sentence is related to the social process of explaining, which we describe in this post (_relevance_ from Gricean Maxims).

Researchers have pointed out many heuristics used by humans to favour some candidate causes (causal hypotheses) over others: proximal over distal events (in the causal chain of events); abnormal or unexpected events; controllable events, deviation from theoretical ideals, model, predictive power, responsibility, and so forth.

But those are taken care of by _contrastive why-questions_ which compare the event to be explained to a reference case (particular instance or general case). In this regard, [Hesslow][causal_selection_problem] states (bold is mine):

> Many of the selection criteria listed in Section 3 can be construed as the result of **choosing different objects of comparison or reference classes**. Let us consider again the fire in the barn, and let us suppose that we have in the back of our minds the picture of a normal barn. (...) the normal barn has not caught fire, it follows that an explanatorily relevant condition for this barn's catching fire must be abnormal. Thus, selection of **abnormal conditions** can be viewed as the result of comparing the explanandum object with a normal object.

And also most other causal selections are contained:

> (...) the difference between this barn now and this barn yesterday, i.e. we would be selecting a **precipitating** cause [proximal in the list above]. Selection of the **unexpected** may be viewed as the result of explaining the difference between an expected and an actual outcome. Selection according to **responsibility** follows from a comparison between actual and morally ideal behaviour. Selection of conditions which cause a **deviation from a theoretical ideal** involves a comparison between an actual and a theoretically ideal situation, and so on (cf. Hesslow, 1983).

Here is yet another illustration by Hesslow, of how contrasts cases narrow down possible causes:

> For instance, if we want to explain why the fly Ml has shorter wings than Nl, then the temperature in which the flies were raised is explanatorily irrelevant, since the temperature was the same in both cases. The mutated gene on the other hand was present in one case and absent in the other.It is, therefore, explanatorily relevant.


## Social Process (Communication)

We have gone through the _cognitive process_ and how contrastive questions can aid the generation and selection of a hypothesis or a cause.

The second process is that of communication. This isn't just the _transfer of knowledge_; in the best cases, it involves an exchange between the participants (explainer and explainee), as in a e.g. dialogue.

The communication can be aided by the [gricean maxims][gricean_maxims]: rules of _effective_ communication.

- **Informative** (Quantity): right amount of context and details,
- **Truthful** (Quality, or Fidelity): the explanation should be true,
- **Relevance** (Relation): avoid presumed-known or superfluous details, focus on what provides insight,
    - One example given earlier is to focus on unexpected events, whilst ignoring what is presumed to be known by the listener.
- **Manner** (clarity): express it in elegant terms.

In some cases, humans also tend to prefer concrete over abstract explanations, so "concreteness" could be added to the list.

_Relevance_ is primarily related to the _causal selection problem_ in relation to an audience, as [Malle et. al., state][autonomous_intelligent_systems]:

> How do people solve this problem? They determine what exact question the audience is interested in (McClure and Hilton 1998); they take into account what their audience member already knows (Slugoski et al. 1993); and they offer elements of explanations that build bridges between presumed knowledge and novel information (Korman and Malle 2016). In short, they offer explanations that generate coherence in a knowledge structure of old and new information (Thagard 1989).

_Contrastive explanations_ can also take care of many of these aspects automatically, by selecting a contrast that is relevant or understood by the audience.

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
1. [How People Explain Action (and Autonomous Intelligent Systems Should Too)][autonomous_intelligent_systems] (2017). Argues that Agents will necessarily have initiative, planning, decision making and people will regard them as intentional agents. They will explain them (and expect the system to do so) as if it were a human.
1. [Explaining Explanations in AI][xxai] (2019), a fantastic paper, from the perspective of "explanation sciences" (philosophy, cognitive sciences, social sciences). Defines terms clearly (XAI, Explanation in XAI, Interpretability/Explainability), distinguishes the main areas (transparency and post hoc interpretability), and names important post-hoc methods.
1. Blog Posts: [What is Explainable AI?][what_is_xai] (2022) and from [IBM][xai_ibm].
1. [Good Explanations in Explainable Artificial Intelligence (XAI): Evidence from Human Explanatory Reasoning][byrne_human_explanations] (2023). This paper discusses certain aspects of human explanations and understanding. For example: the illusion of understanding, thinking fast (intuitive, heuristic) and slow (deliberate, methodical), and explanatory stances. It also discusses counterfactual and causal explanations.

</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[abductive_logic]:https://www.ijcai.org/Proceedings/73/Papers/017.pdf

[autonomous_intelligent_systems]: https://aaai.org/papers/16009-16009-how-people-explain-action-and-autonomous-intelligent-systems-should-too/

[beware_inmates_asylum]: http://arxiv.org/abs/1712.00547

[byrne_human_explanations]: https://doi.org/10.24963/ijcai.2023/733

[causal_selection_problem]: https://www.researchgate.net/publication/232592695_The_problem_of_causal_selection

[explanations_social]: https://doi.org/10.1016/j.artint.2018.07.007

[gricean_maxims]: https://effectiviology.com/principles-of-effective-communication/

[logic_of_expl_hempel]: https://fitelson.org/woodward/hempel_oppenheim.pdf

[lombrozo]: https://fitelson.org/few/few_08/lombrozo_reading.pdf

[scriven]: https://fitelson.org/woodward/scriven_epl.pdf

<!-- [XAI for whom]: http://arxiv.org/abs/2106.05568 -->
[wikipedia_gricean]: https://en.wikipedia.org/wiki/Cooperative_principle

[what_is_xai]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/

[xai_ibm]: https://www.sei.cmu.edu/blog/what-is-explainable-ai/

[xxai]: https://dl.acm.org/doi/10.1145/3287560.3287574

<!-- ### Pragmatism -->
<!---->
<!-- Notably, accuracy may not be preferred in an explanation; rather, usefulness, simplicity, generality and consistency with prior knowledge are. -->
<!---->
<!-- Many of these results come from work by Tania Lombrozo. (This section will eventually be expanded.) -->

<!-- - The hypothesis is clarifying an _explanandum_ (that which is to be explained), and answers a question about it. -->
<!-- The process may repeat and update during the interaction. Sometimes it's during an explanation that we find errors in the understanding. Hence, explanations can provide understanding!  -->
<!-- Besides the cognitive and social process, this post focuses on  _contrastive explanations_, _causal selection_ and _social_. We will dive into each of those aspects in the remaining sections. -->
