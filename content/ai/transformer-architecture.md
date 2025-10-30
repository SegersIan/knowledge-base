---
title: "Transformer Architecture"
---
# Transformer Architecture

The transformer architecture is the current mainstream architecture used for these new foundational models, originally published in the "Attention is all you need" paper.

![omg](../assets/transformer_arch_1.png)

## Basics

* **Context**
    * Computers work with numbers, not text, so they need to encode any text to numerical representations. 
    * LLMs use tokens as their basic "unit" of text. Each token has a vector representation (aka word embedding)
    * All embeddings are of the same fixed length which is set/defined before the model is trained.
        * This is called the **Embedding Dimension** {{< katex >}} d_{\text{model}} {{< /katex >}}
        * *This dimension is super important, all laywers, steps etc in the architecture will use the same dimension to do calculations*.
        * In our example we will use a length of `4`
* 1. We have an **input sequence** (e.g. a prompt)
    * Example `How Are You` (and for the sake of simplicity in the explanation, `one word == one token`)
* 2. **Each token** in the input sequence must be **converted to a "(word) embedding"**
    * A *tokenizer* converts the input sequence into tokens.
        * `[How, Are, You]`
    * Then each token is mapped to their Token ID from the model's vocabulary.
         * `[1234, 456, 23]`
    * Then for each Token ID their corresponding embedding can be retrieved.
        * `How` -> tokenId `1234` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} 0.8 & -1.8 & 0.6 & -0.5 \end{bmatrix} {{< /katex >}}
        * `Are` -> tokenId `456` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} -1.6 & 1.3 & -1.9 & 0.4 \end{bmatrix} {{< /katex >}}
        * `You` -> tokenId `23` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} -0.3 & 0.7 & -1.4 & -0.9 \end{bmatrix} {{< /katex >}}

## Components

### Self-Attention Mechanism

#### Definition
> Self-attention is a way for the model to look at all the words in a sentence at once and decide which ones are important to each other when figuring out meaning.

* Captures context, relationships, and meaning across whole sentences or paragraphs.

> “The cat sat on the mat because it was tired.”

* You know that “it” refers to “the cat”, not “the mat.”

#### How it works

* Each word looks at all the other words.
* The model assigns attention scores — higher scores mean “this other word is important for understanding me.”
* The model then combines information from all the words, weighted by how much attention it gives to each.

##### Detailed

* Calculate the **attention score** for each token:
    * The embedding for an input token is expressed as {{< katex >}} \mathbf{x}_i {{< /katex >}} 
    * For each token we need the following vector representations:
        * **Query vector** \\( \mathbf{q}_i \\)
        * **Key vector** \\( \mathbf{k}_i \\)
        * **Value vector** \\( \mathbf{v}_i \\)
    * Each of these is obtained by multiplying the embedding with a different weight matrix — parameters the model learns during training.
        * **Query vector** \\( \mathbf{q}_i = \mathbf{x}_i \mathbf{W}_Q \\)
        * **Key vector** \\( \mathbf{k}_i = \mathbf{x}_i \mathbf{W}_K \\)
        * **Value vector** \\( \mathbf{v}_i = \mathbf{x}_i \mathbf{W}_V \\)


* TODO... Similarity Score

#### Multi-Head Attention

### Positional Encoding

### Add and Norm

### Feed-Forward Network

### Encoder and Decoder

## Types Of Transformers

## Resources
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)
