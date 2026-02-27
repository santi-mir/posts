# Distributed Representations

Distributed representations are the technical name for the vectors (for atoms, compounds, words,..) we have talked about. They can be continuous or discrete, sparse or dense.[^1]

Which ways are there to create vector-representations of atoms?

| Random | One-Hot | Atom2Vec | Mat2Vec | SkipAtom|
|--------|---------|----------|---------|----------|
| From Random Distributions  | One 1, rest 0s | SVD of Atom-Group matrix  | Embedding (Word2Vec)| Embedding (Skip-gram) |
| $(0.4,\ldots,0.6)$ | $(0,\ldots,1,\ldots,0)$| as random | as random | as random |
|dense|sparse|sparse|dense|dense|

## Comments

- **Atom2Vec**: any matrix (square or not) has SVD; but does this improves over co-occurences vector?
- **Mat2Vec**: The projection matrix, initially random, ends up storing embeddings.
    - Task: context-words predict centre-word. Example: `The cat ___ on the mat.`
- **SkipAtom**: In the same paper of Word2Vec there is the Skip-gram algorithm, which is adapted for chemistry in this paper.
    - Task: centre-word predicts context-words. Example: `___ ___ sat __ ___ ____` (same sentence).

## Embeddings

Embeddings are vectors in real ($R^n$) non-random vector-space, representing an object. _Real_ here implies continuous.

Not all vector or distributed representations are embeddings.

For embeddings, similar objects have similar vectors, according to some metric.

## Representations of Compounds (Pooling)

The analogy to NLP is that _words are like atoms_, and _sentences are like compounds_. Hence, distributed representations of atoms can be combined (pooled) into a vector representing a compound.

Vector-pooling options are:

- _sum_: $\sum s_i \vec{a}_i$ where $s_i$ is the stoichiometry (can be fractional),
- _mean_: $\frac{\sum s_i \vec{a}_i}{\sum s_i}$, i.e. divided by total number of atoms (can be fractional too).
- _max_: $\mathrm{max}(M_i)$, reduces material matrix $\mathrm{M}$ to vector. Selects max value of each column, each row being an atom in the compound.

The resulting compound representation is then used for training a feed-forward NN on different tasks. Also benchmarked using MatBench.

The pooling can also be done with hot-encoded vectors. This is done in ElemNet (mean pooling), and in Bag-of-atoms (sum pooling). In these cases, the result is a _sparse_ vector.

[^1]: This are just my definitions and may be wrong!
