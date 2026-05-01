# Machine learning for molecular and materials science

Very compressed bits from the paper [Machine learning for molecular and materials science][Nature] (2018).

## Representations of atoms, molecules, materials

The process of converting raw data into a format more suitable for an algorithm is called _feature engineering_.

> The more suitable the representation of the input data, the more accurately can an algorithm map it to the output data.
>
> Selecting how best to represent the data may require insight into both the underlying scientific problem and the operation of the learning algorithm, since it is not always obvious which choice of representation will give the best performance.

### Examples

- Coulomb Matrix: atomic nuclear repulsion information.
- Graphs: Connectivity of molecules.
- String representations: SMILES, SELFIES,..
- Solid-state unit-cells: Representations based on radial distribution functions, Voronoi tessellations, and property-labelled materials fragments (...)
    > In the solid-state, the conventional description of crystal structures by translation vectors and fractional coordinates of the atoms is **not appropriate for ML**, since a lattice can be represented in an infinite number of ways by choosing a different coordinate system.

## List of a few ML algorithms

Naive Bayes, Nearest Neighbour, Decision Trees, Kernel methods, a family including support vector machine (SVM) and kernel ridge regression (KRR). Artificial neural networks (ANNs) and deep neural networks (DNNs).

[Nature]: https://www.nature.com/articles/s41586-018-0337-2
