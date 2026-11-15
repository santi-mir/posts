# Machine Understanding

This post, and the next one, explore the topic of _machine understanding_.

------

## The Imitation Game

The paper [Computing Machinery and Intelligence][turing] (Alan Turing, 1950) describes a game with three participants. In the first scenario the participants are:

- A woman: tasked to be authentic,
- A man: tasked to play the part of (imitate) a man,
- A human interrogator: tasked to guess which of the other members is a man and which is a woman (interacting via text interface).

In the second scenario, a computer takes the role of the man, and we ask: _Can the computer pass as a woman with the same skill a man does?_

Turing called this "The Imitation Game".

A simplified version of the game is referred to as the "Turing test"; it takes the second set up and asks: _Can the interrogator distinguish which participant isn't a human?_. In this post either name will be used, unless the details become relevant.

Turing's test avoids two complexities:

- Defining _thinking_,
- Comparing more closely brains and digital computers.

Turing was aware of many objections and some are addressed in the paper. However, he dismisses an objection which recently became more important:

> May not machines carry out something which ought to be described as thinking but which is very different from what a man does? (...) if, nevertheless, a machine can be constructed to play the imitation game satisfactorily, we need not be troubled by this objection.

## Strong AI and the Turing Test

In [Is the Brain's Mind a Computer Program?][searle_simple] (1990) Searle states that _Strong AI advocates_ take the Turing test as a test for machine thinking:

> The Turing test, as currently understood, is simply this: if a computer can perform in such a way that an expert cannot distinguish its per formance from that of a human who has a certain cognitive ability&mdash;say, the ability to do addition or to understand Chinese&mdash;then the computer also has that ability.

The Strong AI advocates seem to interpret that _if the machine performs like a human, then it thinks_; but even Turing seems more sceptical:

> The feature of using electricity is thus seen to be only a very superficial similarity [between brains and digital computers]. If we wish to find such similarities we should look rather for mathematical analogies of function.

On ["Could a machine think?"][churchlands] the Strong AI assumption seems implicit and agrees with Searle's description of the view (the part in quotes is Searle's main axiom):

> (...) "Syntax by itself is neither constitutive of nor sufficient for semantics." (...) to assume its truth is tantamount to begging the question against the research program of classical AI, for that program is predicated on the very interesting assumption that if one can just set in motion an appropriately structured internal dance of syntactic elements, appropriately connected to inputs and outputs, it can produce the same cognitive states and achievements found in human beings.

Other related quotes being:

> Chinese room makes axiom 3 tempting to the unwary, (...)

And:

> Even though Searle's Chinese room may appear to be "semantically dark," he is in no position to insist, on the strength of this appearance, that rule-governed symbol manipulation can never constitute semantic phenomena, (...)

The Chinese Room may be argued to be an intuition pump or metaphor that eases the way into Searle's **Axiom 3**, that "_programs are neither constitutive nor sufficient for minds_". But.., was Searle right?

### Arguments Against Strong AI

- **The Chinese Room**: Searle's Chinese Room Argument (CRA for short; from "Brains, Minds and Programs", 1980) is a thought experiment aiming to show the absurdity of the Strong AI view.

  Here only Searle's conclusions will be quoted:

  > Now let me add the point that the Chinese Room demonstrated. Having the symbols by themselves&mdash;just having the syntax&mdash;is not sufficient for having the semantics. Merely manipulating symbols is not enough to guarantee knowledge of what they mean.

  According to Searle if a computer passes the Turing test we can't guarantee that it thinks. A program may read as thoughtful, pass the Turing test, but it wouldn't know the meaning of the symbols it is manipulating.

  An equivalent statement by Searle is:

  > You can't get semantically loaded thought contents from formal computations alone, (...)

  A similar argument by [Koller and Bender][nlu] is that machines can't learn intents from _form_ alone (symbols) though they may if trained on e.g. meaning pairs. They also describe their own _Octopus test_ for language understanding and comment on Searle's Chinese Room:

  > Searle's thought experiment begins from the premise that it is possible to manipulate forms well enough to be indistinguishable from a system that understands the meaning of the forms, reasons about it, and responds appropriately. We observe that much recent work in NLP claims to be building systems where not only the runtime system but in fact also the process for building it only has access to form.

- **False Positives**: Searle's argument aside, the record shows that simple programs can be _mistakenly assumed to be thinking_ by human evaluators.

  Humans anthropomorphise language easily (assigning a mind behind it), as the [ELIZA effect][eliza] has shown. A similar case was [Clever Hans][hans]; Hans was a horse assumed to understand arithmetic, but was using social queues to guess the result as it was shown later on (still impressive, but a different capability).

  This has happened in recent times as well, [with LLMs][melanie_talk_cognitive]; for example, a model taken to have learnt "a world model" was later on shown to be memorising (or using local rules and heuristics).

<!-- And trusting output generated without an actual reasoning behind can be dangerous. -->

The take aways seem to be that:

- We aren't very good evaluators of simulated capabilities;
- Internal mechanisms of a network may help us do precisely that;

## Meaning

A central part of the issue of machine understanding and thinking involves _meaning_. Let's now step back and ask: _But what is meaning?_

Searle states that _meaning_ is what the symbols refer to:

> If, for example, I am thinking about the last presidential election, certain words will go through my mind, but the words are about the election only because I attach specific meanings to these words, in accordance with my knowledge of English. In this respect they are unlike Chinese symbols for me.

In [Climbing Towards NLU][nlu] (2021), Koller and Bender define _meaning_ as the set of `(expressions, intents)` pairs. _Expressions_ are symbols, gestures and intent is what's not in the expression itself (this is the _intent_).

They also highlight the _grounding problem_, the problem of connecting the symbols to perceived entities:

> But language is used for communication about the speakers' actual (physical, social, and mental) world, and so the reasoning behind producing meaningful responses must connect the meanings of perceived inputs to information about that world. This in turn means that for a human or a machine to learn a language, they must solve what Harnad (1990) calls the _symbol grounding problem_. Harnad encapsulates this by pointing to the impossibility for a non-speaker of Chinese to learn the meanings of Chinese words from Chinese dictionary definitions alone.

Symbol grounding and understanding (in LLMs) are also an important part of [this presentation][chalmers] by David Chalmers (2023).

### Meaning and Hardware

Searle asks some interesting questions:

> why couldn't we give semantics to other computers?
>
> (...)
>
> What, in fact, are the differences between animal brains and computer systems that enable the Chinese room argument to work against computers but not against brains?

Searle continues:

> The most obvious difference is that the processes that define something as a computer&mdash;computational processes&mdash;are completely independent of any reference to a specific type of hardware implementation. One could in principle make a computer out of old beer cans strung together with wires and powered by windmills.
>
> But when it comes to brains, although science is largely ignorant of how brains function to produce mental states, one is struck by the extreme specificity of the anatomy (...)

And later on, in the replies to comments states:

> (...) formal symbols have no physical, causal powers. The only power that symbols have, qua symbols, is the power to cause the next step in the program when the machine is running. And there is no question of waiting on further research to reveal the physical, causal properties of 0's and 1's. The only relevant properties of 0's and 1's are abstract computational properties, and they are already well known.

The processing of a rich representation of interlinked symbols themselves linked to input (e.g. perceptions) and outputs (e.g. an action, decision or conclusion) wouldn't be enough; for Searle would say the important differences, where meaning may be found, are in the organisation (architecture) and causal powers of the hardware.

> (...) the brain does not merely instantiate a formal pattern or program (it does that, too), but it also causes mental events by virtue of specific neurobiological processes.

- _Why would Searle consider that physical, causal links are required, rather than just the computation?_ He says:

> But the simulation should not be confused with duplication. The computational model of mental processes is no more real than the computational model of any other natural phenomenon.

For example (again Searle's words):

> No one expects to get wet in a pool filled with Ping-Pong-ball models of water molecules. So why would anyone think a computer model of thought process es would actually think ?

He says that, to _think_ computers must "duplicate the specific causal powers of brains, and it could not do that just by running a formal program."

So overall his view is that a running computer program, on a standard computer, is symbol processing without meaning (exemplified by the CRA), and the difference (which also _adds meaning in_) is to be found in the organisation and causal structure of the brain which computers (as currently designed) lack.

Also, the causal structure isn't about adding a robotic body, but about the kind of causation within the neural network.

Fascinating. But it's worth pondering here:

- _Why is about meaning that require a particular organisation and causal powers (such as that of brains)?_
- Conversely, we can push on the Strong AI view: What if all that is needed is a rich representations of (grounded)-symbols, links between them, and appropriate input-output mapping (processing)? Form alone does seem insufficient, and was refuted by [Koller and Bender][nlu] but what about rich representations of symbols connected to multimodal perceptions? This is what they suggest in Section 7 (among other options):

> One approach to providing grounding is to train distributional models on corpora augmented with perceptual data, such as photos (...)

## But...is it relevant?

Let's assume that we are not interested in a modern computer that develops a mind with an actual self, understanding, and thoughts, but a modern computer that carries out the computations of those processes, solves problems, represents things internally in a rich, and understandable (by us) way and so forth.

It may even do research and discover things.

What would we call what these machines do? What are the limits of it? Would they be more than just useful-ish computers?

[chalmers]: https://consc.net/papers/groundingdebate.pdf
[churchlands]: https://www.sciencedirect.com/science/chapter/edited-volume/abs/pii/B9780122154959500120
[eliza]: https://en.wikipedia.org/wiki/ELIZA_effect
[hans]: https://en.wikipedia.org/wiki/Clever_Hans
[melanie_talk_cognitive]: https://www.youtube.com/watch?v=yKbeCvOKvMchttps://www.cell.com/trends/cognitive-sciences/fulltext/S1364-6613(26)00077-X
[nlu]: https://aclanthology.org/2020.acl-main.463/
[searle_simple]: https://www.beisecker.faculty.unlv.edu/Courses/PHIL%20330/Searle,%20Is%20the%20Brain's%20Mind%20a%20Computer%20Program.pdf
<!-- [semantic_net]: https://en.wikipedia.org/wiki/Semantic_network -->
[turing]: https://academic.oup.com/mind/article/LIX/236/433/986238
