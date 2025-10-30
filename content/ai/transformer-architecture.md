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

> “The cat sat on the mat because it was tired.”

* You know that “it” refers to “the cat”, not “the mat.”

#### How it works

* Each word looks at all the other words.
* The model assigns attention scores — higher scores mean “this other word is important for understanding me.”
* The model then combines information from all the words, weighted by how much attention it gives to each.

#### Detailed

* We have an **input sequence** (e.g. a prompt)
    * Example `How Are You` (and for the sake of simplicity in the explanation, `one word == one token`)
* **Each token** in the input sequence must be **converted to a "word embedding"**
    * A word embedding is a vector representation of a token in a highly dimensional space.
    * Computers can only work with numbers, so vectors are used for all processing.
* Assign **3 vectors to each token** in an input sequence.
    * All vectors have the same fixed length.
    * Vector length is set by the model at training.
    * For our example the vector length is `4`.
    * Example of the word embeddings of our input sequence.
        * `how` 

$$
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
$$

```katex
\begin{bmatrix}
a & b \\
c & d
\end{bmatrix}
```


#### Multi-Head Attention

### Positional Encoding

### Add and Norm

### Feed-Forward Network

### Encoder and Decoder

## Types Of Transformers

## Resources
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)
