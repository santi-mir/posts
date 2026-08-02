# The Explanation Spectrum

This post just explores what kind of explanations we can expect based on the complexity of a model or agent.

-------------------

## Human To Human

How do humans explain things to each other? At which level of description do they do it?

We have explored the first of those questions; important aspects being _contrastive explanations_, comparison, and logical deduction.

Humans can explain phenomena to each other, it is not required that we get access to each others' brain processes. And we ourselves do not have that level of detail accessible by introspection.

We may say that the brain uses "communication" processes that possibly "look at" decision processes (see Marvin Minsky, [The Emotion Machine][minsky]). Then the statement is interpreted by another agent and it can be tested, or compared to other previous statements that we consider true, searching for inconsistencies or contradictions.

## DL Models as Scientific Models

DL models are mathematical functions. Both the architecture, or the trained model can be considered scientific models or theories. In this case, it may be expected that they can be communicated and described in certain domain-local terms.

There are also societal reasons for this expectation (since many models are used on decision making and high-stakes scenarios).

In this case, for simple, or narrow-AI models, we may expect to peek into the black box, and to analyze their input-output relations to get insight into their inner workings.

They're expected to be decomposable in domain-level concepts (just as a theory is).

In other words, we want to answer: _What did it learn? Which concepts is the network using for their decision making?_

## DL Models as Scientists

General-purpose models may explain decisions in a human-like way, and be as hard to inspect as the brain is. Treating these models as a scientific theory of a domain, or a narrow AI model, may be a counter-productive, or even a category error. We may still learn from them, but a detailed explanation process could be as hard to extract as it is from a brain.

So how can we do it? In this case, it may be better to expect what we expect from a human. Take an explanation in natural language and test it and compare it to other established statements.

## The Explanation Spectrum

It is possible that DL models will fill the whole spectrum from scientific models and theories to _generators_ of scientific models and theories (just as humans are).

With this in mind, we could suggest the concept of an _explainability spectrum_.

- On one end, it has agents that can't explain their inner workings in detail, but can still output a certain explanation (e.g. humans).
- Near the middle models that can't give reasons, but we can study as black boxes.
- On the opposite end models that can give reasons and we can both study as black boxes, and also see what they learnt internally (a bit like CNNs' layers).

This isn't necessarily a fixed spectrum. As science advances, some models may become more explainable, or an architecture that is much more explainable will be found (Capsule Networks were an effort in this direction).

In both cases, an architecture of how humans explain subjects, what the expectations are for a context, audience and even a model-kind, should be useful.

<details>
<summary>Sources</summary>
1. [The Emotion Machine][minsky] &mdash; Marvin Minsky: This book is a theory suggesting that the mind is a hierarchy of processes, and makes theories of how each layer may work.
</details>
[minsky]: https://web.mit.edu/dxh/www/marvin/web.media.mit.edu/~minsky/index.html
