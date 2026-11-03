# Machine Understanding

This is a work in progress. I am collecting views on Machine Understanding that I find historically or conceptually interesting.

Currently, it's primarily John Searle's position, and then Koller and Benders idea of meaning.

------

Usually, the Turing test (described in ["COMPUTING MACHINERY AND  INTELLIGENCE"][turing], 1950, by Alan Turing) is assumed to be a test for thinking under the assumption that only outward behaviour matters.

This isn't Turing's point, since he makes clear that we can't even define thinking. But it makes us consider: If a machine can pass as a human without being noticed by other humans, what are the consequences? Do the internal mechanisms matter? Should we call it thinking?

As humans we tend to assume a mind behind any bit of language, as the ELIZA effect has shown. And even for evaluating understanding *without* linguistic outputs, humans have been wrong about Clever Hans (a horse assumed to understand arithmetic, but later on shown to read social queues to guess, which is still impressive). This has happened in recent times as well, [with LLMs][melanie_talk_cognitive].

The take away seems to be that we should evaluate more carefully, and that looking at the internal mechanisms of a network may help us do precisely that.

In ["Is the Brain's Mind a Computer Program?"][searle_simple] (Searle, 1990) Searle describes the Strong-AI advocates' view of the Turing test:

> The Turing test, as currently understood, is simply this: if a computer can perform in such a way that an expert cannot distinguish its per formance from that of a human who has a certain cognitive ability&mdash;say, the ability to do addition or to understand Chinese&mdash;then the computer also has that ability.

Searle's Chinese Room Argument (CRA for short; from "Brains, Minds and Programs", 1980) is an intuition pump that shows the absurdity Strong AI view. The underlying point is: a program on modern computers, even if it passes the Turing test (as his experiment's subject does), is a symbol manipulator, and as such it doesn't guarantee semantics nor thinking. Searle summarises his result:

> Now let me add the point that the Chinese Room demonstrated. Having the symbols by themselves&mdash;just having the syntax&mdash;is not sufficient for having the semantics. Merely manipulating symbols is not enough to guarantee knowledge of what they mean.

Searle concludes that _no symbol manipulation program can think_, even if it has the right input-output behaviour: the system wouldn't yet know the meaning of the Chinese symbols/words it is manipulating.

A last statement, equivalent to all of the above, of his:

> You can't get semantically loaded thought contents from formal computations alone, (...)

## Meaning

But what is meaning then? Searle believes that it's what the symbols refer to, but aren't those also symbols?
One could argue that are the "symbols" of the perceptions for example. Consider a few more ideas about what meaning could be:

- "Meaning 1" comes from symbols standing for / referring to something; the symbols have mental content. I suppose that we may or not be aware of the mental content (conscious or unconscious). Or is *thinking* always a conscious process?
- "Meaning 2" is just "links between symbols".
    - A single neuron isn't complex enough for that; rather, it may simply be manipulating symbols.

A variant of "Meaning 2" includes the _grounded symbols_ that is, symbols for linked to perceptions, its parts, memories, emotions, and so forth. Something that the expression refers to, in the mind of the interpreter.

Koller and Bender, in [Climbing Towards NLU][nlu] (2021) define meaning as the set of pairs `(expressions, intents)`; expressions can be symbols, gestures and intent is what's not in the expression itself. They hold that machines can't learn intents from form alone (symbols) but don't make statements about learning from pairs, or whether it's impossible.

Beyond the above paragraph, [Climbing Towards NLU][nlu] talks about the Turing test, Searle's Chinese Room, Harnad, their own Octopus test, and so on. For example, they say:

> Searle's thought experiment begins from the premise that it is possible to manipulate forms well enough to be indistinguishable from a system that understands the meaning of the forms, reasons about it, and responds appropriately. We observe that much recent work in NLP claims to be building systems where not only the runtime system but in fact also the process for building it only has access to form. But language is used for communication about the speakers’ actual (physical, social, and mental) world, and so the reasoning behind producing meaningful responses must connect the meanings of perceived inputs to information about that world. This in turn means that for a human or a machine to learn a language, they must solve what Harnad (1990) calls the symbol grounding problem. Harnad encapsulates this by pointing to the impossibility for a non-speaker of Chinese to learn the meanings of Chinese words from Chinese dictionary definitions alone.

"Meaning 1" may involve a meta process linking some aspects of the processing to the input and the output.

But how does `Meaning 1` relate to `Meaning 2`? In my view, "Meaning 1" is built on top of symbol manipulation where the only "meaning" is how symbols are linked and represented ("Meaning 2"). However, this itself isn't enough, it may require specific ways in which the lower level processing happens, and also specific meta-processes.

The Chinese Room Argument (CRA) refutes the Strong AI claim "Meaning 1" and the right I/O implies "Meaning 2"; the Strong AI claim may come from a (mis)-interpretation of the Turing test.

In relation to *what meaning is* for Searle, besides the CRA, see:

> If, for example, I am thinking about the last presidential election, certain words will go through my mind, but the words are about the election only because I attach specific meanings to these words, in accordance with my knowledge of English. In this respect they are unlike Chinese symbols for me.

### Compressed View
Searle captures his overall view in this paragraph:

> First, I have not tried to prove that "a computer cannot think." Since any thing that can be simulated computationally can be described as a computer, and since our brains can at some levels be simulated, it follows trivially that our brains are computers and they can certainly think. But from the fact that a system can be simulated by symbol manipulation and the fact that it is thinking, it does not follow that thinking is equivalent to formal symbol manipulation.

That is, some computers can think (brains are computers and can think), but the simulation of thought (right IO) through symbol manipulation does not guarantee any meaning or thought.

Here something seems strange: Searle believes computers _can_ think, but symbol manipulation can't have semantics (needed for thinking).

In other words, semantics (or thoughts, or mental contents) are somewhat special. Let's explore why Searle may think so.

## Hardware Thoughts

Searle's questions are very interesting:

> why couldn't we give semantics to other computers?
>
> (...)
>
> What, in fact, are the differences between animal brains and computer systems that enable the Chinese room argument to work against computers but not against brains?

(What do we need, beyond the program?)

Searle continues:

> The most obvious difference is that the processes that define something as a computer&mdash;computational processes&mdash;are completely independent of any reference to a specific type of hardware implementation. One could in principle make a computer out of old beer cans strung together with wires and powered by windmills.
>
> But when it comes to brains, although science is largely ignorant of how brains function to produce mental states, one is struck by the extreme specificity of the anatomy (...)

And later on, in the replies to comments states:

> (...) formal symbols have no physical, causal powers. The only power that symbols have, qua symbols, is the power to cause the next step in the program when the machine is running. And there is no question of waiting on further research to reveal the physical, causal properties of 0's and 1's. The only relevant properties of 0's and 1's are abstract computational properties, and they are already well known.

So _even if_ we consider "the processing of a rich representation of interlinked symbols themselves linked to input (e.g. perceptions) and outputs (e.g. an action, decision or conclusion)." Searle would say _no_.

Why? He's got this covered:

> (...) the brain does not merely instantiate a formal pattern or program (it does that, too), but it also causes mental events by virtue of specific neurobiological processes.

- _Why would Searle consider that physical, causal links are required, rather than just the computation?_ He says:

> But the simulation should not be confused with duplication. The computational model of mental processes is no more real than the computational model of any other natural phenomenon.

For example simulating _a diesel car engine_ doesn't release combustion gases; nor simulating _the rain_ makes the computer wet, and so forth. Or in Searle's words:

> No one expects to get wet in a pool filled with Ping-Pong-ball models of water molecules. So why would anyone think a computer model of thought process es would actually think ?

And in Searle's words, to _think_ computers must "duplicate the specific causal powers of brains, and it could not do that just by running a formal program."

So overall his view is that a running computer program, on a standard computer, is symbol processing without meaning (exemplified by the CRA), and the difference (which also _adds meaning in_) is to be found in the physical and causal structure of the brain and the computers (as currently designed).

Also, the causal structure isn't that of wrapping _current computers_ in a robot body, but about the kind of causation in the neural network.

Fascinating stuff. But it's worth pondering here:

- _Why exactly does meaning require a particular physico-causal organisation of matter?_
- And, what if semantics / meaning are not what Searle thinks (and require certain causal structure), and all that is needed is rich representations of symbols (included grounded ones), links between them, and their processing? Note that I am not saying _form alone_ since this was robustly refuted by [Koller and Bender][nlu] but e.g. rich representations of symbols connected to multimodal perceptions. This is what they suggest in Section 7 (among other options):

>One approach to providing grounding is to train distributional models on corpora augmented with perceptual data, such as photos (...)

Searle does consider this question, once in the quote at the beginning of this section, another time below in relation to the Churchlands' ["Could a Machine Think?"][churchlands] (1990):

> (...) could not later investigation also show that semantics are entirely constituted of syntax ?


It's an interesting dilemma. It seems likely to me that Searle is right, and that the mind is physico-biological, and just as digestion, an emergent property of matter.

Simulating digestion simply isn't digestion.


## But...is it relevant?

Let's assume that we are not interested in a machine that develops a mind with an actual self, understanding, and thoughts, but that solves problems, represents things internally in a rich, and understandable (by us) way; it may even do research and discover things.

Leaving aside the important question of morality (which for Searle wouldn't seem to be a problem, since they aren't real beings), then, what would we call what these machines do?

What status would these systems have? And what are they, just useful-ish computers?

[churchlands]: https://www.sciencedirect.com/science/chapter/edited-volume/abs/pii/B9780122154959500120
[melanie_talk_cognitive]: https://www.youtube.com/watch?v=yKbeCvOKvMc
[nlu]: https://aclanthology.org/2020.acl-main.463/
[searle_simple]: https://www.beisecker.faculty.unlv.edu/Courses/PHIL%20330/Searle,%20Is%20the%20Brain's%20Mind%20a%20Computer%20Program.pdf
[turing]: https://academic.oup.com/mind/article/LIX/236/433/986238
