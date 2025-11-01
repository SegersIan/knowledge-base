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
    * Then for each Token ID their corresponding embedding (\\( E(\text{token}_i) \\)) can be retrieved.
        * `How` -> tokenId `1234` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} 0.8 & -1.8 & 0.6 & -0.5 \end{bmatrix} {{< /katex >}}
        * `Are` -> tokenId `456` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} -1.6 & 1.3 & -1.9 & 0.4 \end{bmatrix} {{< /katex >}}
        * `You` -> tokenId `23` -> {{< katex >}} \mathbf{x}_i = \begin{bmatrix} -0.3 & 0.7 & -1.4 & -0.9 \end{bmatrix} {{< /katex >}}
    * At this stage, all the tokens that are the same, would have the same embedding. However, the position of the token in the input sequence has also influence and relevance. So for each token, the original embedding is taken and "manipulated" to reflect also the position in the sequence.
        * \\( x_i = E(\text{token}_i) + P(\text{position}_i) \\)

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
    * The embedding for an input token is expressed as \\( \mathbf{x}_i \\) (which includes the positional encoding already)
    * For each token we need the following vector representations:
        * **Query vector** (\\( \mathbf{q}_i \\)) : what this token is asking for?
            * What am I looking for in other tokens?
        * **Key vector** (\\( \mathbf{k}_i \\)) : what this token offers?
            * What kind of information do I have that others might need?
        * **Value vector** (\\( \mathbf{v}_i \\)) : the actual information content that can be shared?
            * Here’s the stuff you can take from me if you attend to me.
    * Illistruative example
        * Imagine you’re in a classroom with students working on a group discussion.
        * Each student is a token (a word in a sentence).
        * They’re all trying to listen to each other and decide who has the information they need.
             * **Query vector** - “What am I looking for in other students?”
                * Think of your Query as the question you have in your mind.
                * Example: You’re the student “dog” in the sentence “The dog chased the ball.”
                * “Who tells me what I’m doing?” (You’re looking for the verb.)
                * So your Query describes what kind of information you want from others.
             * **Key vector** - “What kind of information do I have that others might need?”
                * Example: The student “chased” (the verb) has a Key that says:
                * “I can tell others what action is happening.”
                * So if another token is looking for an action (like “dog”), they’ll notice that your Key matches what they’re querying.
             * **Value vector** - “Here’s the actual information I can share.”
                * if a student decides that another student’s Key is relevant, they attend to that student and take their Value — the actual content.
                * Example: Once “dog” realizes “chased” has the Key it was looking for, it takes its Value — maybe information like “the action is chasing” — to understand the full meaning.
    * The model has 3 different Weight matrices:
        * \\( \mathbf{W}_Q \\) - The **Query** weight matrix.
        * \\( \mathbf{W}_K \\) - The **Key** weight matrix.
        * \\( \mathbf{W}_V \\) - The **Value** weight matrix.
    * Now we can calculate each vector by multiplying our token embedding \\( \mathbf{x}_i \\) with the respective weight matrix (Q, K or V).
        * **Query vector** \\( \mathbf{q}_i = \mathbf{x}_i \mathbf{W}_Q \\)
        * **Key vector** \\( \mathbf{k}_i = \mathbf{x}_i \mathbf{W}_K \\)
        * **Value vector** \\( \mathbf{v}_i = \mathbf{x}_i \mathbf{W}_V \\)
    * Now can calculate the **similarity score** (which we need for calculating the **attention score**).
        * Defintion: Raw measure of how well each key aligns with a query
        * Large positive values mean “highly related,” small or negative values mean “unrelated.”
        * These scores are the core signals telling the model which tokens (keys) should pay more attention to which current token (query).
        * Fomula for calculating the similarity betweenany 2 arbitrary vectors of the same length.
        ```katex
        similarity(a, b) = 
        \text{similarity}_{ab} = \frac{Q_a \cdot K_b}{\sqrt{d_k}}
        ```
        

* TODO... Similarity Score

#### Multi-Head Attention

### Positional Encoding

### Add and Norm

### Feed-Forward Network

### Encoder and Decoder

## Types Of Transformers

## Resources
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)
