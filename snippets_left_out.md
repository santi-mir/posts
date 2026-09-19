<!-- BELOW THERE IS A TON OF SNIPPETS I REMOVED TO KEEP IT SHORT -->

<!-- ### Brief Aside: Neural Netwoks -->
<!---->
<!-- This post assumes a working idea of what deep learning models or neural networks are. A simple definition is provided in the paper [Can we open the black box of AI?][open_ai_black_box] (Section "Good Trip"). -->
<!---->
<!-- But what exactly do these networks _learn_? ["Scientific discovery in the age of artificial intelligence"][ai_aided_discovery] states that: -->
<!---->
<!-- > [AI methods] includes deep representation learning (Box 1), particularly multilayered neural networks capable of identifying essential, compact features that can simultaneously solve many tasks that underlie a scientific problem. -->
<!---->
<!-- So a key aspect of understanding and explaining will be to decode those "essential, compact features" into domain concepts. What concepts, if any, are stored there, in the synapses? -->
<!---->
<!-- It's also useful to have in mind a general idea of where are neural networks models being used, and how: -->
<!---->
<!-- 1. Domain-specific (Narrow AI): these are small or large models but trained on a specific domain (protein folding, generating new molecules, predicting spectra and so forth). These models benefit from XAI, inductive biases and constrains, and would ideally be interpretable. -->
<!-- 2. Domain-general (Foundation Models): there is a spectrum between networks trained for a task in a domain, and for a whole domain (e.g. chemistry). These models are usually very large, pre-trained in some unsupervised way and then need to be fine tuned to specific tasks, where they reuse the learnt building blocks. -->
<!-- 3. AI agents: These are clusters of models working together to carry out many parts of the scientific process of discovery (hypothesis generation, reading literature, suggesting experiments and running code simulations etc.) In some cases they may also have access to robotics platforms and run real world experiments. The difference to other approaches is that these models are reasoning, and to some extent work like a team of scientists. -->
<!---->
<!-- Here we are concerned with `1.` primarily, and with the possibility to explain them, design them such that they are interpretable and finally understand them better. -->

<!-- explain also that there are are clear reasons companies may prefer black box models (in two senses): proprietary helps to profit (and restricts gaming them), black box helps avoid accountability / responsibility. -->
<!-- Simpler models are also less expressive and may use less variables than the original, making it easier to understand. -->

<!-- The explanations may still be _local_ (explains a particular prediction) or global (explains the full model). The question is rather _how faithful_ it needs to be. Combination of local explanations may also give a global understanding of the model. -->

<!-- > [!NOTE] -->
<!-- > Not all models need an explanation model, some may use explanation techniques that still look at them as black boxes, such as contrastive or counterfactual explanations. -->
<!-- As noted in the previous post, the "questions" may be implicit; and it's common that the question, implicit or explicit is a _contrastive why-question_. -->

<!-- As I read it, _explainability_ and _interpretability_ are also considered synonyms by [Explaining Explanations in AI][xxai] stating "the xAI community investigates interpretability (or explainability) ...". The paper also defines _interpretability_ as: -->
<!---->
<!-- > "Interpretability" refers to the degree of human comprehensibility of a given 'black-box' model or decision (Lisboa, 2013; Miller, 2017). -->

<!-- Our definition of explanation is more detailed and was given in [this previous post](./explanation.md). -->
<!-- It's interesting to consider, that we ourselves can't really inspect our own models within the brain. We a human explains a model, there is still the "human black box", but one which we trust, maybe because of human-human similarities. -->

<!-- Since there are many definitions and goals of XAI we should always define the term (even approximately) or to cite a definition, and to state _which problems_ our ideas aim to solve. -->
<!-- ## Real World Objectives-->
<!---->
<!-- Partly based on the paper [The Mythos of Model Interpretability][mythos] we want to:-->
<!-- 1. Trust. In which sense? Accuracy deployment robustness, human-performance? -->
<!-- 2. Causality. They are usually trained to just make correlations/associations, and they may learn to use proxy-variables, confounders (X-Y may have both an underlying Z-cause), shortcuts; we would want causal relationships instead. Bayesian Networks and Regression Trees? How can we infer causal relations from observational data (Pearl, Causality) -->
<!-- Transferability: This isn't just about Out Of Distribution, but that the training environment correctly reflects the deployment one (for example, programmers may misinterpret the meaning of some column, or it may even be wrong, which could still happen in accurate models! So this should be broken down into database trust (which is also mentioned by Rudin though in terms of data poisoning rather than errors) and data-task correctly understood, and model generality / performance OoD.
Unclear why this item is about interpretability.
-->
<!-- Informativeness: Interesting. Besides or along with the primary training objective it may be possible to extract extra information from the model, to help (inform) the user. This may be provided with posthoc or intrinsic XAI as well. Rudin et.al., created a "classifier-by-similarity" CNN that outputs which images in the dataset where used to decide, compared to. Or point to similar cases. Counterfactuals / Contrasts seem another way (Juergensen).
-->
<!-- Ethics: Right to explanation (GDPR), Conform to ethical standards,..-->
<!-- 4. Improve debugging / troubleshooting? -->
<!-- 5. Get more useful information from the model. -->

<!-- <details> -->
<!-- <summary>Sources</summary> -->
<!---->
<!-- </details> -->

<!-- Posthoc is the sort of interpretability / explainability that applies to humans (which are otherwise black boxes). -->
<!-- There are many methods to identify causes or relevant properties on models, that help explain how they work. Some of them include counterfactuals and comparison. -->

<!-- [^literal]: The suffix "-ability" simply means "the degree to which" so _explainability_ is the degree to which a phenomenon or event is explainable, and _Model explainability_ simply adds a bit more context to what the words themselves mean together (which is already "the degree to which a model is explainable"). -->

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
<!-- ## Model Insights from Comparisons -->
<!---->
<!-- How many ways do we have to make comparisons? Probably dozens. Analogies, metaphors, counterfactuals, a reference case (opposite or similar), a prototype or class-assignment (generalisation uses comparison). -->
<!---->
<!-- _Counterfactuals_ What would have happened with an alternative input (a hypothetical case counter to the fact). It's most informative to use the minimum changes that change an output class. They are also similar to _What ifs_ (as the question shows). -->
<!---->
<!-- Counterfacturals and other comparisons can help to explain models without opening the box. -->
<!---->
<!-- For a model, _counterfactuals_ are yet another inference from another input, but the comparison is helpful because that is one way humans understand things. We can use them as a proxy to "understand how the model is thinking" (that is, by comparing results or inferences). -->
<!---->
<!-- In a similar fashion to counterfactuals, we can compare with reference inputs. -->

<!-- (A logic-inference section could be added, but at the moment I don't see it adding much useful information.) -->

<!-- ## Higher-Level Aspects of Networks -->
<!---->
<!-- The recognition of higher level patterns in graph can also span across methods. -->
<!---->
<!-- These can even be inspired by other networks or graphs; for example, insect colonies can be considered as graphs of insect-nodes and pheromone-edges, and certain nodes have roles and tasks they specialise on. A similar situation can be postulated to happen in human networks, and in neural (biological and artificial) networks, where the node is affected by, and also affects other nodes. -->
<!---->
<!-- A basic description of graph and networks and how there can be transfer learning between the different areas can be found in [Siemens - Connectivism][connectivism_siemens] and particularly in [Downes - Connectivism][connectivism_downes]. -->
<!-- A **deduction** (proof) is e.g. "All cats are animals (I); animals are big (II); then cats are big (III)", whereas **abduction** (hypothesis) would be "III; I; maybe II" notice the _maybe_ (anti-clockwise rotation). Another anti-clockwise rotation takes us to **induction** (generalisation,hypothesis): "II; III; maybe all I". -->

<!-- For example: Can we create a deep learning model, or a model-explanation algorithm that best fits ordinary people's requirements? Can we adapt pre-existing ones for this purpose? Can we create or adapt models or explanation models that are suitable for specific audiences (with different requirements)? When can we trade _truth_ or _accuracy_ of an explanation, for _simplicity_? -->

<!-- >[!NOTE] -->
<!-- > The problem of causal _connection_ and _selection_ (`1.`) are well known, complex problems in psychology. -->

<!-- > [!NOTE] -->
<!-- > This post is mostly jargon-free. Technical articles about topics such as _abductive inference_ are linked in the "Sources" at the bottom of this post. A brief discussion of logic inference in AI is given [in this article][logic_substack] by Gordon Brander. -->

<!-- The definition of "Explanation" given above is unclear regarding what "_explains_" means. We could just as well define "Interview" as "Someone interviews someone about something". Though even in this vague form, it still highlights an exchange between two agents. -->
<!-- The authors also state that contrastive explanations are usually preferred by humans to other kinds of explanations (e.g. fuller causal-chain explanations). -->

<!-- Notice also that we have different formulations an answers. -->

<!-- Contrastive questions simply use a fact and a foil. This can help generate counterfactual / causal answers. -->
<!---->
<!-- Anomalies are usually a case when contrastive explanations are requested, against a normal or expected case (foil). -->
<!---->
<!-- [Explaining Explanations in AI][xxai] also adds an interesting analysis about the value of contrastive explanations: -->
<!---->
<!-- > While the utility of contrastive theories remains debated, the fact that contrastive explanations address a particular event or case and are thus simpler to generate than complete or global explanations of model functionality suggest they worth further consideration in xAI (Lipton, 1990). -->
