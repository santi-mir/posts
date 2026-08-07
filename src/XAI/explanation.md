# Explanations

This post describes what explanations are, and forms a basis for understanding how to explain artificial intelligent systems.

<!-- For example: Can we create a deep learning model, or a model-explanation algorithm that best fits ordinary people's requirements? Can we adapt pre-existing ones for this purpose? Can we create or adapt models or explanation models that are suitable for specific audiences (with different requirements)? When can we trade _truth_ or _accuracy_ of an explanation, for _simplicity_? -->

--------------

## Definition

What is an explanation? There are many definitions. Here is one, from "[How People Explain Action (and Autonomous Intelligent Systems Should Too)][autonomous_intelligent_systems]" (2017):

> Explanation is arguably a three-value predicate: someone, a communicator, explains something to someone, an audience. The success of an explanation therefore depends on several critical audience factors—assumptions, knowledge, and interests that an audience has when decoding the explanation.

> [!NOTE]
> **Relation of Explanation to Understanding**
>
> Understanding is having a theory or idea about how something works. Usually we refine or correct these with experience. So it is a prerequisite for an explanation, and can be associated to the _cognitive process_ explained in the next section. However, the process of explaining can refine our understanding (it's a cycle).

The first definition though, is unclear regarding what "_explains_" means. But this is explored in the next section.

Inspired by [Explanation in artificial intelligence: insights from the social sciences][explanations_social], this post defines "explaining" broadly as:

> **Explaining**
>
> A two-step process involving `1.` the generation of explanatory hypotheses (cognitive process) and `2.` the communication to an audience (social process).

The cognitive process may also generate multiple hypotheses which are then compared, and one may be selected until contradicted by experience or superseded (e.g. by a simpler explanation, by being disproved, or shown to be inconsistent).

- The process may iterate and update during the interaction (or not, in a static explanation).
- Sometimes it's during an explanation that we find errors in the understanding. Hence, explanations can provide understanding!
- Also, the _explanandum_ (that which is to be explained) may be refined just as a photo-camera may gain focus with increased exposure.

<!-- >[!NOTE] -->
<!-- > The problem of causal _connection_ and _selection_ (`1.`) are well known, complex problems in psychology. -->


## Cognitive Process

### Contrastive Questions

Research has shown that _why-questions_ are usually _contrastive_. That is, they are phrased as _Why P rather than Q?_ instead of simply _Why P?_ Usually P is the real case (or fact) and Q the expected case (or foil), which may also be implicit.

As the paper [Beware of Inmates Running the Asylum][beware_inmates_asylum] states:

> For example, explaining "Why did Mr. Jones open the window?" with the response "Because he was hot" is not useful if the implied foil is Mr. Jones turning on the air conditioner, as this explains both the fact and the foil; or if the implied foil was why Ms. Smith, who was sitting closer to the window, did not open it instead, as the cited cause does not refer to a cause of Ms. Smith's lack of action.

The _foil_ focuses the explanation on the differences between the two cases (ignoring similarities). This is usually easier to explain than the standalone fact. It can also reduce confusion.

[Hesslow][causal_selection_problem] states this idea in a concise way:

> What I want to suggest, then, is that the explanandum should be construed as a relation which involves three things: an _object a_, an _object of comparison b_ and an _explanandum property E_ which a has and b does not have.

The complexity, of course, lies on knowing _which differences_ matter.

### Attributing Causes

As [Miller et al. state][beware_inmates_asylum]:

> Attribution theory is the study of how people attribute causes to events; something that is necessary to provide explanations.

We never provide a full causal chain (it is endless), but a short-enough one that explains the event in question (this is the _causal selection problem_).

Researchers have pointed out many heuristics used by humans to favour some candidate causes (causal hypotheses) over others: proximal over distal events (in the causal chain of events); abnormal or unexpected events; controllable events, deviation from theoretical ideals, model, predictive power, responsibility, and so forth.

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

We have gone through the _cognitive process_ and how contrastive questions can aid the generation and selection of a hypothesis or a cause. The second process is that of commucation.

The communication can be aided by the [gricean maxims][gricean_maxims]: rules of _effective_ communication.

- **Informative** (Quantity): right amount of context and details,
- **Truthful** (Quality, or Fidelity): the explanation should be true,
- **Relevance** (Relation): avoid presumed-known or superfluous details, focus on what provides insight,
    - One example given earlier is to focus on unexpected events, whilst ignoring what is presumed to be known by the listener.
- **Manner** (clarity): express it in elegant terms.

In some cases, humans also tend to prefer concrete over abstract explanations, so "concreteness" could be added to the list.

_Relevance_ is primarily related to the _causal selection problem_, as [Malle et al state][autonomous_intelligent_systems]:

> How do people solve this problem? They determine what exact question the audience is interested in (McClure and Hilton 1998); they take into account what their audience member already knows (Slugoski et al. 1993); and they offer elements of explanations that build bridges between presumed knowledge and novel information (Korman and Malle 2016). In short, they offer explanations that generate coherence in a knowledge structure of old and new information (Thagard 1989).

_Contrastive explanations_ can also take care of many of these aspects automatically, by selecting a contrast that is relevant or understood by the audience.


## Metaphors: The Machine and The Agent

Humans often use "explanatory stances" to explain events, as noted by Daniel Dennett. There are three common ones:

1. *Mechanical* stance (which I call "Machine Metaphor/Model"),
    - Explain outcomes by considering the parts of a system and how they interact (that is, a mechanism).
2. *Design* stance, this has different interpretations. One is of the perceived _purpose_ of something (applied to things created by humans such as tools, but also those hypothesised to be created by universal designer or god).
3. *Intentional* stance (which I call "Agent Metaphor/Model").
    - Explanation uses goals, motives, feelings, intent to explain actions and/or behaviour.
    - _Unintentional_ behaviour is usually explained using the machine metaphor.

They can be complementary when applied to the same phenomena or as [Ruth Byrne][byrne_human_explanations] puts it:

> Notably, each explanatory stance can be applied to explain the same device or action, but they have different consequences for understanding it. Each stance can lead to different kinds of insights, and to different kinds of erroneous inferences. The atypical application of a particular stance, say, a mechanical stance to explain an action more typically understood from an intentional stance, such as explaining travelers in a crowded airport as like pinballs careening around a pinball machine, may be interpreted analogically to yield new inferences [Keil, 2006].

In technical fields, many complex systems are conceptualised as _machines_: composed of parts, each with a function, a role. Many are also conceptualised as _graphs_.

Ordinary people conceptualise certain kinds of complex systems as humans or agents (wholly or in part). This may happen with systems using human language or behaving autonomously, but other times it is due to pragmatic reasons. They would use and expect the kind of explanation a human would give, if there were one.

What seems here most fundamental than the particular stances is the selection of a metaphor to structure thinking and obtaining insights.

Other metaphors and analogies could be proposed for specific problems.

Similar ideas can be found in "[How People Explain Action (and Autonomous Intelligent Systems Should Too)][autonomous_intelligent_systems]":

> For those intentional agents, we hypothesize, people will apply the same conceptual framework of behavior explanation that they apply to humans (...) a subset of AIS that people do not regard as intentional agents; and for those, they may apply a purely mechanical explanatory framework.

And more recently, in [Good Explanations in XAI][byrne_human_explanations]:

> People may tend to adopt multiple stances in their preferred explanations of an AI decision support system and its decisions, not unlike their tendencies in interacting with social robots [Clark and Fischer, 2023]. People are aware that a social robot is a machine, but interpret it as a depiction of a character, not unlike a ventriloquist dummy, and engage with it in pretense of interacting with the depicted character [Clark and Fischer, 2023]. Similarly, they may be aware that an AI decision support system is an algorithm but they may interpret its decisions as a depiction of those provided by a human, e.g., a bank loan assessor, or the organization the human represents, a bank. Hence, an intentional stance and a design stance may both be useful in different contexts for explaining how automated agents behave [Veit and Browning, 2023].


We can summarise some of these ideas (including a standard audience) in a brief table:

| Perspective      | Model is a… | Preferred Explanation style | Audience            |
| ---------------- | ----------- | --------------------------- | ------------------- |
| **Scientific**   | Machine     | Mechanistic, causal, formal | Experts             |
| **Human-facing** |Agent/Person | Intentional, narrative      | Users, stakeholders |


The post on [explanatory stances](./explanatory_stances) continues this line of reasoning and connects them with _how we explain humans and deep learning models_.

<!-- ### Classification -->
<!-- We could also classify explanations as _interactive_ (e.g. a conversation), _static_ (e.g. a book), or a mix of both. -->
<!---->
<!-- - **Interactive explanations**: a communicator and an audience interact aiming to resolve _what_, _how_ or _why_ questions posed by the audience. -->
<!-- - **Static explanations**: Same as above, but they are non-interactive. -->
<!-- - **Mix**: consider machines with pre-set questions and answers, where the audience can't always ask what it needs or wants to. -->
<!---->
<!-- In the rest of this post, the term _explanandum_ defines _that which needs clarification_. -->

<!-- Interactive explanations are similar to static explanations, just updated in real time by follow-up questions, behaviour, and other kind of feedback. -->

<!--  ; for example, DL Models may be conceptualised as machines or similarly, as scientific models. -->


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
1. [Good Explanations in Explainable Artificial Intelligence (XAI):  Evidence from Human Explanatory Reasoning][byrne_human_explanations] (2023). This paper discusses certain aspects of human explanations and understanding. For example: the illusion of understanding, thinking fast (intuitive, heuristic) and slow (deliberate, methodical), and explanatory stances. It also discusses counterfactual and causal explanations.


</details>

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

[abductive_logic]:https://www.ijcai.org/Proceedings/73/Papers/017.pdf

[autonomous_intelligent_systems]: https://aaai.org/papers/16009-16009-how-people-explain-action-and-autonomous-intelligent-systems-should-too/

[beware_inmates_asylum]: http://arxiv.org/abs/1712.00547

[byrne_human_explanations]: https://doi.org/10.24963/ijcai.2023/733

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
