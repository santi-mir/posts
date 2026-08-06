# Explanatory Modes

This post explores different metaphors humans use to explain objects and processes.

One question asked is: Should we explain DL models or teach them to explain themselves? The answer, to some extent, is: it depends.

-------------------

## Explanatory Stances
In the [previous post](./explanation.md) explanatory metaphors, or as Dennett calls them "stances" were described. The summary is:

1. *Mechanical* stance (which I call "Machine Metaphor/Model"),
    - Explain outcomes by considering the parts of a system and how they interact (that is, a mechanism).
2. *Design* stance,
3. *Intentional* stance (which I call "Agent Metaphor/Model").
    - Explanation uses goals, motives, feelings, intent to explain actions and/or behaviour.
    - _Unintentional_ behaviour is usually explained using the machine metaphor.


There a certain intersection between those stances, and the way deep learning models and other humans are explained.

Indeed, humans are explained using the intentional stance. We don't usually use a mechanistic interpretation because that is extremely hard; we use higher level concepts.

To a large extent humans treat other humans as black boxes, not only in terms of explaining their behaviour, but also the way they think and the ideas they communicate.

The way we usually analyse statements does not only involve beliefs about the person, and ignores what happens in the brain, but also just tests their consequences and analyse how the statement fits into our own worldview.

The sections below link these stances to how we explain statements made by another human, or those found in a book, or emitted by a deep learning model.

And it is proposed here that we use a few stances or metaphors, in many cases this is audience dependent. An example is given by [byrne_human_explanations]:

> A potential implication for XAI is the necessity to consider when a particular stance is appropriate for explaining an AI system’s decision. A question posed by a user as to why an AI system refused their loan may be a request for causal information of a mechanistic sort about how the AI system came to make that decision. Hence, it may require an explanation based on information about how the user’s input features relate to a training data set, e.g., that loans have been refused for applicants of similar salary level, occupational status, credit history, as the user. Alternatively, it may be a request for functional information of a teleological sort about the purpose of the AI’s decision. Accordingly, it may require instead information about the goal and consequences of the output, e.g., that decisions of this sort mitigate the risk of applicants defaulting from repayment. Each sort of explanation will lead users to develop a different understanding of aspects of an AI system, and impact their learning, satisfaction, and trust in it.

## Human To Human Explanations

<!-- How do humans explain things to each other? Which level of description do they expect? -->
<!---->
<!-- We have explored the first of those questions in previous posts, where the explanation process was described. -->

When humans explain phenomena to each other they use language, pictures and other media. But we don't get access to each others' brain processes (to a large extent, not even our own); and even if we did, the task wouldn't be trivial.

A brain may use "communication processes" that _look at_ "decision processes" (see Marvin Minsky, [The Emotion Machine][minsky]). Then the statement is exchanged and interpreted by another agent. The statement can be tested against reality, or for inconsistencies or compared to other statements.

In other words, we largely treat brains as black boxes.

Should we treat DL models the same, and accept predictions without "peeking into the black box", just as we do with humans? If so, under which circumstances?

The idea of this post is that there will be a level of complexity and utility at which this will also happen for DL models.

## DL Models are Scientific Models

DL models are mathematical functions. Both the architecture and the trained model can be considered scientific models or theories. In this case, they should be explainable. Here there is an underlying metaphor of "DL models as machines" and we expect them to be explainable in terms of their parts and how they interact.

There are also societal reasons for this expectation: many models are used on decision making and high-stakes scenarios, so we expect explanations or justifications for their decisions, just as we expect from humans making decisions.

For simple or narrow-AI models, we may expect to peek into the black box, and to analyze their input-output relations to get insight into their inner workings.

They're expected to be decomposable in domain-level concepts (just as a theory is).

In other words, we want to answer: _What did it learn? Which concepts is the network using for their decision making?_ But how can we extract their "baked in" knowledge?

_But, what if the metaphor used for a complex DL model is that of a scientist, or a human, rather than a machine?_

## DL Models are Scientists

General-purpose models may explain decisions in a human-like way, and be as hard to inspect as the brain is. Treating these models as a scientific theory of a domain, or a narrow AI model, may be a counter-productive, and even a category error.

In this case, a detailed explanation process could be as hard to extract as it is from a brain.

So what do we do? In this case, it may be better to expect what we expect from a human: Take an explanation in natural language and test it and compare it to other established statements.

This is what the paper [The Mythos of Model Interpretability][mythos] describes, in the section about post-hoc textual explanations:

> Humans often justify decisions verbally. Similarly, one model might be trained to generate predictions, and a separate model, such as a recurrent neural network language model, to generate an explanation.

In other words, we would treat it as a black box.

## Summary

We have explored two metaphors "DL models as Agents / Scientists" and "DL Models as Scientific Models", and the expectations for each case:

1. As Scientific Models: We can study them as black boxes, and also internal mechanisms,
1. As Scientists: We can only study them as black boxes,
    1. This includes Agents that can output a certain explanation (e.g. humans).

As science advances, some models may become explainable. Similarly, intrinsically explainable architectures may be designed, and could be preferred over black box architectures (e.g. Capsule Networks were an effort in this direction).

Now we go back to common methods used to explain mostly narrow AI algorithms.

-------------------

<details>
<summary>Sources</summary>

1. [The Emotion Machine][minsky] (2007) by Marvin Minsky: This book is a theory suggesting that the mind is a hierarchy of processes, and makes theories of how each layer may work. In his view, all layers are made out of abstract units called resources, what changes is their role.
1. [Can we open the black box of AI?][open_ai_black_box] (2016). This paper briefly explains what ANNs are, their similarities (not the differences) to the brain, and what challenges they pose to us. Primarily, the challenge is that they are hard to explain. It puts as an example a physician or patient relying in the output, but not knowing _why_ it predicts that. The author also cites Michael Tyka saying "The problem is that the knowledge gets baked into the network, rather than into us"

</details>

[minsky]: https://web.mit.edu/dxh/www/marvin/web.media.mit.edu/~minsky/index.html
[open_ai_black_box]: http://www.nature.com/news/can-we-open-the-black-box-of-ai-1.20731
[byrne_human_explanations]: https://doi.org/10.24963/ijcai.2023/733
