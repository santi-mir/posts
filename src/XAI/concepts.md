# Explainable AI - Concepts

These are some of my opinions and ideas after reading a few papers:

1. [Explaining Explanations: An Overview of Interpretability of Machine Learning][XX] (2018),
2. [Interpretable and Explainable Machine Learning for Materials Science and Chemistry][XAI4MAT] (2022),
3. [A Perspective on Explainable Artificial Intelligence Methods: SHAP and LIME][SHAP and LIME] (2024).

<!-- Also, a very interesting experiment in terms of explainability was <https://distill.pub>. -->

--------------------

## Explanations

Scientific models are expected to be explainable; that is, to admit explanations of _why_ they make certain prediction, _how_ they operate, _what_ the role of certain part of it is, and so on.

So we refer to explanation as responses to questions about model "behaviour" or operation.

We can characterise explanations using:

- __Simplicity__: how easy to understand the explanation is. (The opposite term, _complexity_, could be used as well.)
        - This is correlated with how simple _the model itself_ is.
- __Completeness__: how accurately it describes the model's behaviour.

<div class="w40 center">
<a href="../assets/tradeoff.png">
<img alt="graph looking like completeness is the inverse of simplitity." src="../assets/tradeoff.png"/>
</a>
<p>Completeness v. Simplicity tradeoff.</p>
</div>

This trade-off isn't universal but just a common case, particularly in deep learning; some other models are straightforward, in which case both characteristics can be high.

### Predictive power

__Predictive power__ is a characteristic of a model, not of an explanation of a model, but is often correlated to those: more predictive models tend to be more complex and the explanation tends to be more complex.

The reason to include it here is that _predictive power_ plays an important role deciding which model to use.

In the image below, note that _understandability_ replaces _simplicity_, and _correctness_ replaces _predictive power_.

<div class="center w40"> <!--other classes: w220, w420-->
    <a href="../assets/radar_plot.png">
    <img src="../assets/radar_plot.png" alt="Plot of the three dimensions"/>
    </a>
    <p>
    Image from <a href="https://pubs.acs.org/doi/10.1021/accountsmr.1c00244">paper</a> under <a href="https://creativecommons.org/licenses/by/4.0/">CC-BY-SA 4.0</a>
    </p>
</div>

[XAI4MAT]: https://pubs.acs.org/doi/10.1021/accountsmr.1c00244
[SHAP and LIME]: https://onlinelibrary.wiley.com/doi/abs/10.1002/aisy.202400304
[XX]: http://arxiv.org/abs/1806.00069
