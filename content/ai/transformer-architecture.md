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
    * Goal: The self-attention mechanism allows each token in an input sequence to determine how much attention it should pay to every other token in the same sequence when computing its representation.
    * The embedding for an input token is expressed as \\( \mathbf{x}_i \\) (which includes the positional encoding already)
    * For each token we need the following vector representations:
        * **Query vector** \\( \mathbf{q}_i \\) : what this token is asking for?
            * What am I looking for in other tokens?
        * **Key vector** \\( \mathbf{k}_i \\) : what this token offers?
            * What kind of information do I have that others might need?
        * **Value vector** \\( \mathbf{v}_i \\) : the actual information content that can be shared?
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
            * Conclusion: When you go through all tokens in a sequence, we need to deterine for each token how much attention it will pay (relatively) to each other token of that same sequence. So you go through each token, for the token you are processing, you need the "query" vector, cause this is your "search query" you could say, and from all other tokens you use the "key vector" cause that key is used to match the query token (e.g. my query token is "beer", what other tokens have a key "beer, meaning they have something to say about beer.). Eventually later the value vector can be used to get actually the content of related token (e.g. "Trampist" , "Pils", ...).
    * The model has 3 different Weight matrices:
        * \\( \mathbf{W}_Q \\) - The **Query** weight matrix.
        * \\( \mathbf{W}_K \\) - The **Key** weight matrix.
        * \\( \mathbf{W}_V \\) - The **Value** weight matrix.
    * Now we can calculate each vector by multiplying our token embedding \\( \mathbf{x}_i \\) with the respective weight matrix (Q, K or V).
        * **Query vector** \\( \mathbf{q}_i = \mathbf{x}_i \mathbf{W}_Q \\)
        * **Key vector** \\( \mathbf{k}_i = \mathbf{x}_i \mathbf{W}_K \\)
        * **Value vector** \\( \mathbf{v}_i = \mathbf{x}_i \mathbf{W}_V \\)
    * To calculate for a token, to which other tokens it should pay most attention to, we can use the concept of "Similarity Between Vectors" in maths. To calculate the similarity between vector `a` and `b` of dimension `k` we use the following formula
    ```katex
    similarity(a, b) = \frac{a \cdot b}{\sqrt{k}}
    ```
        * The reason we divide by \\(similarity(a, b) = \frac{a \cdot b}{\sqrt{k}}\\) is a normalization trick to prevent very large dot products (especially in high-dimensional spaces) from causing the attention weights to become unstable or skewed.
        * This normalization is not ALWAYS done, so it could be that it's not a part, but usually it does.
    * So we use this concept of "Similarity Between Vectors" to calculate the **Attention Score**, that score tells how much a token should pay attention to other tokens. We do this by calculturing the similarity between the query vector of the current token and the key vector of a given other token.
        * The normal similarity function:
        ```katex
        similarity(a, b) = \frac{a \cdot b}{\sqrt{k}}
        ```
        * Becomes now as attention score formula between token `i` and token `j`.
        ```katex
        \text{attention score}_{ij} = \frac{Q_i^{\top} \cdot K_j}{\sqrt{d_k}}
        ```
        * The `T` in \\(Q_i^{\top} \\) means "transpose", cause that's how you can do mathemetically the dot product, it's just a maths thing.
    * Now we have the **attention SCORE**, but we want the **attention WEIGHT**. Attention scores tell how similar they are but now yet how much attention we should give them, By weighing, it becomes very clear, cause all the weights add up to 1. So you could say, I should give 74% of my attention to this token.
        * We apply `softmax` to our attention scores.
        ```katex
            \text{weights}*{i,j} ;=; \frac{e^{\text{scores}*{i,j}}}{\sum_{j'} e^{\text{scores}_{i,j'}}}
        ```
            * Exponentiate to make all numbers positive.
            * Normalize so each row sums to 1.
            * Result: a probability-like distribution saying “how much should token (i) listen to token (j)?”
            * Example: Suppose one token compares to three tokens and gets scaled scores \\([2,;1,;0]\\).
                * (e^2 \approx 7.39,; e^1 \approx 2.72,; e^0 = 1).
                * Sum (= 7.39 + 2.72 + 1 \approx 11.11).
                * Weights (= [7.39/11.11,; 2.72/11.11,; 1/11.11] \approx [0.665,; 0.245,; 0.090]).

#### Multi-Head Attention

![img](../assets/transformer_arch_2.png)

Think of multi-headattention with "h" different copies of a single self-attention head. Each attention head focusses on another aspect of the language, making its understanding richer.

> I want to visit Rome, the capital city of Italy.

This answers multiple questions, like who wants to visit rome? where is romem situated? What is the capital of italy? so there is a lot of different things happening, so different heads will capture different contexts and focus to a variert of information.

* Each head
    * has its own set of linear projections for Q, K, V;
    * focuses on a different aspect of the token relationships.
* So when you’re processing *token i:
    * head 1 might focus on syntactic roles (like “who’s the subject?”),
    * head 2 might focus on semantic relatedness,
    * head 3 might look for position or structure, etc.
* In practices
    * Remember that we had a weight matrix in the model.
        * \\( \mathbf{W}_Q \\) - The **Query** weight matrix.
        * \\( \mathbf{W}_K \\) - The **Key** weight matrix.
        * \\( \mathbf{W}_V \\) - The **Value** weight matrix.
        * We would calculate the Q, K, and V vectors by
            * **Query vector** \\( \mathbf{q}_i = \mathbf{x}_i \mathbf{W}_Q \\)
            * **Key vector** \\( \mathbf{k}_i = \mathbf{x}_i \mathbf{W}_K \\)
            * **Value vector** \\( \mathbf{v}_i = \mathbf{x}_i \mathbf{W}_V \\)
    * For a single token, you create per "head" basically another Q, K and V vectors. That means that "per head" there is another weight matrix. So if you want 5 heads, the models needs to have 5 different weight matrixes for Q, K and V. That means, the head count is set and defined at training stage.

### Positional Encoding

* The word embedding for a token would be exactly the same as the word embedding of another token that shares the same tokenID. Position in a sequence matters. So therefore we use positional encoding.
* We take the word embedding vector is added to a positional embedding vector. The sum will be the input vector used for all the other processing (e.g. for self attention).
* Sunusoidal functions are used to calculate position emmbeddings, cause it can handle varying input length and capture the relative distance between words. 

### Add and Norm

* This block is added after every sublayer (in the orignal transformer architecure)
* The block implements 2 techniques (add and norm) for making the training process more efficient.
* **Add**
    * "Residual Connection"
    * Idea: Add the `input` to the `output` of the sublayer.
* **Normalization**
    * Idea: Normalize the output generate after each layer.
        * Computes the mean and standard deviation across the word embedding deimension.
        * Result: Ensures a proper flow of gradients during training and stability of the model.
* The combination of **Residual Connection"** and **layer normalization** solves the vanishing gradient problem which is common in deep learning.


### Feed-Forward Network

In a Transformer, the Feed-Forward Network is a small two-layer neural network applied to each token separately — it refines the token’s representation after attention and gives the model more learning power.

### Encoder and Decoder

* **Encoder** component is used for taking plain languge and convert it to a vector presentation.
* **Decodeer** component is used for taking the generated output (vector presentation) to human interpretable language.

#### Encoder


The encoder is composed of a stack of 6 identical layers. Each layer has two sub-layers. The first is a multi-head self-attention mechanism, and the second is a simple, position-wise fully connected feed-forward network. We employ a residual connection around each of the two sub-layers, followed by layer normalization. That is, the output of each sub-layer is `LayerNorm(x+Sublayer(x))` , where `Sublayer(x)` is the function implemented by the sub-layer itself. To facilitate these residual connections, all sub-layers in the model, as well as the embedding layers, produce outputs of dimension d model = 512 .


#### Decoder

The decoder is also composed of a stack of 6 identical layers. In addition to the two sub-layers in each encoder layer, the decoder inserts a third sub-layer, which performs multi-head attention over the output of the encoder stack. Similar to the encoder, we employ residual connections around each of the sub-layers, followed by layer normalization. We also modify the self-attention sub-layer in the decoder stack to prevent positions from attending to subsequent positions. This masking, combined with fact that the output embeddings are offset by one position, ensures that the predictions for position i can depend only on the known outputs at positions less than i.

## Types Of Transformers

## Resources
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)

## Math Appendix 

### Transpose

If your query ( q_i ) and key ( k_j ) are **column vectors** (like in most linear algebra conventions):
```katex
q_i =
\begin{bmatrix}
q_{i1} \
q_{i2} \
\vdots \
q_{id_k}
\end{bmatrix},
\quad
k_j =
\begin{bmatrix}
k_{j1} \
k_{j2} \
\vdots \
k_{jd_k}
\end{bmatrix}
```
then the **dot product** is written as:
```katex

q_i^{\top} k_j =
[q_{i1}, q_{i2}, \dots, q_{id_k}]
\begin{bmatrix}
k_{j1} \
k_{j2} \
\vdots \
k_{jd_k}
\end{bmatrix}
= \sum_{\ell=1}^{d_k} q_{i\ell} k_{j\ell}
```
That “⊤” (transpose) flips ( q_i ) from a column into a row, so you can multiply it with ( k_j ) and get a **single number** (a scalar).

### Vanishing Gradient Problem

When a neural network learns, it updates its weights using **gradients** — basically little nudges that tell it *how much to change* to make the output better.

But in very **deep networks** (many layers), those gradients have to be passed **backward** through all the layers (this is called *backpropagation*).

If each layer makes the gradient a bit smaller, by the time it reaches the early layers (near the input), it’s almost **zero** — it *vanishes*.

When that happens:

* The early layers stop learning.
* The network’s training gets very slow or stuck.
* The model might only learn in the top layers.

That’s the **vanishing gradient problem**.

#### Simple analogy

Imagine you’re passing a message through a long chain of people by whispering.
Each person hears it a little quieter and passes it on.
After 50 people, the message is *barely a whisper* — or completely gone.

That’s what happens to gradients in deep networks — they fade away before reaching the start.