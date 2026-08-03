# Explainability Cases

One of the main questions explored is: Should we accept DL models' predictions without "peeking into the black box", just as we do with another human statement (without peeking into their brain)? If so, when?

-------------------

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

In other words, we want to answer: _What did it learn? Which concepts is the network using for their decision making?_

_But, what if the metaphor used for a complex DL model is that of a scientist, or a human, rather than a machine?_

## DL Models are Scientists

General-purpose models may explain decisions in a human-like way, and be as hard to inspect as the brain is. Treating these models as a scientific theory of a domain, or a narrow AI model, may be a counter-productive, and even a category error.

In this case, a detailed explanation process could be as hard to extract as it is from a brain.

So what do we do? In this case, it may be better to expect what we expect from a human: Take an explanation in natural language and test it and compare it to other established statements.

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

</details>

[minsky]: https://web.mit.edu/dxh/www/marvin/web.media.mit.edu/~minsky/index.html
