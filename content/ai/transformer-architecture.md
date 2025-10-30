---
title: "Transformer Architecture"
---
# Transformer Architecture

The transformer architecture is the current mainstream architecture used for these new foundational models, originally published in the "Attention is all you need" paper.

![omg](../assets/transformer_arch_1.png)

## Components

### Self-Attention Mechanism

### Definition
> Self-attention is a way for the model to look at all the words in a sentence at once and decide which ones are important to each other when figuring out meaning.

* Captures context, relationships, and meaning across whole sentences or paragraphs.
* Each word looks at all the other words.
* The model assigns attention scores — higher scores mean “this other word is important for understanding me.”
* The model then combines information from all the words, weighted by how much attention it gives to each.

> “The cat sat on the mat because it was tired.”

* You know that “it” refers to “the cat”, not “the mat.”

#### How it works




#### Multi-Head Attention

### Positional Encoding

### Add and Norm

### Feed-Forward Network

### Encoder and Decoder

## Types Of Transformers

## Resources
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)

## Katex test

$$
\int_{-\infty}^{\infty} e^{-x^2} dx = \sqrt{\pi}
$$

```katex
f(x) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi
```
$$
f(x) = \int_{-\infty}^\infty\hat f(\xi)\,e^{2 \pi i \xi x}\,d\xi
$$
