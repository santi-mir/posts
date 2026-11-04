# Machine Understanding

This is a work in progress, that explores the topic of "Machine Understanding", "Machine Thinking" and related ideas.

------

## Strong AI and the Turing test

The [Turing test][turing] (1950, by Alan Turing), is a remote chat where a human is tasked to tell who of the other two members of the chat is a computer.

In ["Is the Brain's Mind a Computer Program?"][searle_simple] (1990) Searle states that Strong-AI advocates take the Turing test as a test for machine thinking:

> The Turing test, as currently understood, is simply this: if a computer can perform in such a way that an expert cannot distinguish its per formance from that of a human who has a certain cognitive ability&mdash;say, the ability to do addition or to understand Chinese&mdash;then the computer also has that ability.

But, we could ask the Strong AI advocates:
- Does such machine experience the world the same than us?
- What about the internal mechanisms?
- Why only care about overt behaviour?
- Is the Turing test the best one for this purpose?

There are a few reasons that make this interpretation untrustworthy.

- First, we may be bad at evaluating this difference.
- Second, even if we evaluate correctly, it may be that the test does not provide conclusive evidence of thinking or another cognitive capacity.

## First: Are we good evaluators?
Humans anthropomorphise language easily (assigning a mind behind it), as the [ELIZA effect][eliza] has shown.

Humans have also been wrong about [Clever Hans][hans]; Hans was a horse assumed to understand arithmetic, and later on shown to guess the answer social queues (which is still impressive, but a different capability).

This has happened in recent times as well, [with LLMs][melanie_talk_cognitive].

<!-- And trusting output generated without an actual reasoning behind can be dangerous. -->

The take-away seems to be that we should evaluate behaviour more carefully, and that looking at the internal mechanisms of a network may help us do precisely that.

## Second: Turing test's usefulness

Searle's Chinese Room Argument (CRA for short; from "Brains, Minds and Programs", 1980) is a thought experiment aiming to show the absurdity of the Strong AI view. Searle summarises his result as:

> Now let me add the point that the Chinese Room demonstrated. Having the symbols by themselves&mdash;just having the syntax&mdash;is not sufficient for having the semantics. Merely manipulating symbols is not enough to guarantee knowledge of what they mean.

Searle concludes that _programs restricted to symbol manipulation can't think_. A program may have the right input-output behaviour (e.g. passes the Turing test), but the system wouldn't yet know the meaning of the Chinese symbols/words it is manipulating.

A last statement, equivalent to all of the above, of his:

> You can't get semantically loaded thought contents from formal computations alone, (...)

## General Ideas about Meaning

<!-- If the machines can fool us via syntactics only, it would be interesting to know _how_ the missing bit (meaning) works and how it fits in the picture. -->

Before considering details about meaning let's ask: What is meaning (in broad terms)? Searle states that meaning is what the symbols refer to:

> If, for example, I am thinking about the last presidential election, certain words will go through my mind, but the words are about the election only because I attach specific meanings to these words, in accordance with my knowledge of English. In this respect they are unlike Chinese symbols for me.

But this seems a bit mysterious and one may want to ask Searle: What if all we need are symbols, processing, and grounded symbols?[^1]

What about researchers other than Searle? Koller and Bender, in [Climbing Towards NLU][nlu] (2021) define meaning as the set of `(expressions, intents)` pairs. _Expressions_ are symbols, gestures and intent is what's not in the expression itself (this is the _intent_).

They hold that machines can't learn intents from form alone (symbols) though they may if trained on meaning pairs, or a similar task.

[Climbing Towards NLU][nlu] talks about all the of the above: the Turing test, Searle's Chinese Room, Stevan Harnad's grounded symbols, and they describe their own _Octopus test_ for language understanding. They say:

> Searle's thought experiment begins from the premise that it is possible to manipulate forms well enough to be indistinguishable from a system that understands the meaning of the forms, reasons about it, and responds appropriately. We observe that much recent work in NLP claims to be building systems where not only the runtime system but in fact also the process for building it only has access to form.

(Which is precisely what bare-LLMs do.) They continue:

> But language is used for communication about the speakers' actual (physical, social, and mental) world, and so the reasoning behind producing meaningful responses must connect the meanings of perceived inputs to information about that world. This in turn means that for a human or a machine to learn a language, they must solve what Harnad (1990) calls the _symbol grounding problem_. Harnad encapsulates this by pointing to the impossibility for a non-speaker of Chinese to learn the meanings of Chinese words from Chinese dictionary definitions alone.

<!-- ### Recap -->
<!---->
<!-- So far we considered the Strong AI view of the Turing test, and both practical and theoretical arguments against it. The former about a history of problems of human evaluating the output, and the latter related to the Chinese Room Argument and the training on form only. -->
<!---->
<!-- But Searle's view is a bit weirder. Searle believes that _some_ computers _can_ think (e.g. the brain). But not the programs running on silicon, since symbol manipulation can't have semantics (needed for thinking). -->

### Hardware Thoughts

Searle asks interesting questions:

> why couldn't we give semantics to other computers?
>
> (...)
>
> What, in fact, are the differences between animal brains and computer systems that enable the Chinese room argument to work against computers but not against brains?

In other words: Where does meaning (or semantics) come from, that we can't just add it in modern computers, but brains have it? Searle continues:

> The most obvious difference is that the processes that define something as a computer&mdash;computational processes&mdash;are completely independent of any reference to a specific type of hardware implementation. One could in principle make a computer out of old beer cans strung together with wires and powered by windmills.
>
> But when it comes to brains, although science is largely ignorant of how brains function to produce mental states, one is struck by the extreme specificity of the anatomy (...)

And later on, in the replies to comments states:

> (...) formal symbols have no physical, causal powers. The only power that symbols have, qua symbols, is the power to cause the next step in the program when the machine is running. And there is no question of waiting on further research to reveal the physical, causal properties of 0's and 1's. The only relevant properties of 0's and 1's are abstract computational properties, and they are already well known.

So _even if_ we consider "the processing of a rich representation of interlinked symbols themselves linked to input (e.g. perceptions) and outputs (e.g. an action, decision or conclusion)." Searle would say _no_. Searle explains that the difference is that

> (...) the brain does not merely instantiate a formal pattern or program (it does that, too), but it also causes mental events by virtue of specific neurobiological processes.

- _Why would Searle consider that physical, causal links are required, rather than just the computation?_ He says:

> But the simulation should not be confused with duplication. The computational model of mental processes is no more real than the computational model of any other natural phenomenon.

For example (again Searle's words):

> No one expects to get wet in a pool filled with Ping-Pong-ball models of water molecules. So why would anyone think a computer model of thought process es would actually think ?

He says that, to _think_ computers must "duplicate the specific causal powers of brains, and it could not do that just by running a formal program."

So overall his view is that a running computer program, on a standard computer, is symbol processing without meaning (exemplified by the CRA), and the difference (which also _adds meaning in_) is to be found in the physical and causal structure of the brain which computers (as currently designed) lack.

Also, the causal structure isn't that of wrapping _current computers_ in a robot body, but about the kind of causation in the neural network.

Fascinating. But it's worth pondering here:

- _Why exactly does meaning require a particular physico-causal organisation of matter?_
- And, what if semantics / meaning are not what Searle thinks (and require certain causal structure), and all that is needed is rich representations of symbols (included grounded ones), links between them, and their processing? Note that I am not saying _form alone_ since this was robustly refuted by [Koller and Bender][nlu] but e.g. rich representations of symbols connected to multimodal perceptions. This is what they suggest in Section 7 (among other options):

> One approach to providing grounding is to train distributional models on corpora augmented with perceptual data, such as photos (...)

Searle does consider this question, once in the quote at the beginning of this section, another time below in relation to the Churchlands' ["Could a Machine Think?"][churchlands] (1990):

> (...) could not later investigation also show that semantics are entirely constituted of syntax ?

It's an interesting dilemma. It seems likely to me that Searle is right, and that the mind is physico-biological and, just as digestion, an emergent property of matter.

Simulating digestion simply isn't digestion.

## But...is it relevant?

Let's assume that we are not interested in a machine that develops a mind with an actual self, understanding, and thoughts, but that solves problems, represents things internally in a rich, and understandable (by us) way; it may even do research and discover things.

Leaving aside the important question of morality (which for Searle wouldn't seem to be a problem, since they aren't real beings), then, what would we call what these machines do?

What status would these systems have? And what are they, just useful-ish computers?

[churchlands]: https://www.sciencedirect.com/science/chapter/edited-volume/abs/pii/B9780122154959500120
[eliza]: https://en.wikipedia.org/wiki/ELIZA_effect
[hans]: https://en.wikipedia.org/wiki/Clever_Hans
[melanie_talk_cognitive]: https://www.youtube.com/watch?v=yKbeCvOKvMc
[nlu]: https://aclanthology.org/2020.acl-main.463/
[searle_simple]: https://www.beisecker.faculty.unlv.edu/Courses/PHIL%20330/Searle,%20Is%20the%20Brain's%20Mind%20a%20Computer%20Program.pdf
[semantic_net]: https://en.wikipedia.org/wiki/Semantic_network
[turing]: https://academic.oup.com/mind/article/LIX/236/433/986238

[^1]: Harnad's _grounded symbols_ are those linked to perceptions, memories, emotions, and so forth. And those in turn are just some input representation.


<!-- Consider a few more ideas about what meaning could be: -->
<!---->
<!-- - "Meaning A" is what the symbols stand for / refer to; and the referee is mental content (conscious or unconscious, I assume, and one may split System 1 and System 2, as Daniel Kahnemann argued). -->
<!-- - "Meaning B" is just "links between symbols". -->
<!--     - A single neuron isn't complex enough for that; rather, it may simply be manipulating symbols. -->
<!---->
<!-- " Meaning A" may involve a meta-process linking some aspects of the processing to the input and the output. -->


<!-- How does _ Meaning A_ relate to _Meaning B_? One way could be that Meaning A adds the _leaves_ to a _branch-structure_ (Meaning B). There may also be requirements specific ways in which the lower level processing happens, and also specific meta-processes. -->

<!-- All the refutation of Strong AI via CRA needs is us to accept that symbols have independent meanings. processing symbols, on their own, as CRA states, " Meaning A" and the right I/O implies "Meaning B"; the Strong AI claim may come from a (mis)-inte Harnad's _grounded symbols_ are those linked to perceptions, memories, emotions, and so forth.rpretation of the Turing test. -->
<!-- In my view one could think of meaning as a tree, the structure of branches are _symbols and their links_; the leaves are the _grounded symbols_. The structure of branches is a [semantic network][semantic_net]. -->

