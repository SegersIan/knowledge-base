---
bookCollapseSection: true
title: "AI & ML"
math: true
tags: ["AI"]
---
# AI & ML

## General Concepts

### Natural Language Processing (NLP)
> The branch of AI that makes computers capabable of understanding the human language (spoken & written).

### NLP Tasks

* **Text Classification** - Classify text in one or more predefined classed (Politics, War, Science, ...)
* **Sentiment Analysis** - Understand and classift emotion exprees in text (Positive, Neutral, Negative)
* **Question Answering** - Answering a question based on a refernce text
    * Ex: Ian is buying chocolate in the shop, where is Ian? - In the shop
* **Part of Speech (POS) tagging** - Classify each word in a text into grammatical categories (noun, verb, ...)
* **Named Entity Recognition (NER)** - Identify named entities in a text (people, locations, organizations, ...)
    * Ex: Ian is in Spain. - Ian is a person, Spain is a location.
* **Text Summarization**
    * *Extractive* - Summerize using existing sentences of the reference text.
    * *Abstractive* - Summerize using new sentences not present in the reference text.
* **Machine Translation** - Translate from one language to another (French to English)

### Text Preprocessing
> The process of cleaning (normalizing) textual data and prepare it for modelling. 
> WHY? Data in real life is messy, so garbage in, garbage out.
> By normalizing the data, you remove anything that might be noise or stand in the way.

Preprocessing steps depend on the context and use case, but to give some examples:

* **Capatilization** - Often we don't care about capatlization in text, so we make all text lowercase.
* **URLS** - Do you need to keep URLS?
* **HTML Tags** - Remove any HTML tags and code if irrelevant
* **Expand Contractions** - Expand short versions of text to normalize it. If they have the exact same meaning, there is value to consider them as "2 seperate" values.
    * Ex: `won't => will not` 
* **Punctuations** - Often have no segmantic significance, remove them if irrelevant.
* **Stop Words** - Often stopwords in sentences have no segmantic significance, remove them if irrelevant.
* **Remove Numbers** - Often numbers in sentences have no segmantic significance, remove them if irrelevant.
* **Interpretate Emojis** - Often used as expression of feeling, so replace them with their corrolating emotions.

### Data Transformation
> Done after preprocessing.
> Additional transformations that will further enhance the data for better modelling.
> These techniques are linguistic in nature, often break down sentences or words to reduce complexity.

* **Tokenization** - Breaking down sentences into smaller units (like words).
    * *By Whitespace* is the simplest decompensition technique.
    * Other techniques exist.
* **Lemmatization** - Reduce bords into their base form (aka `lemmas`)
    * Thanks to *POS Tagging* you know the grammatical category for each token, allowing for proper lemmatization.
    * Ex: `am, is, are, was, were, been, beeing` => `be`
    * Ex: `run, runs, running, ran` => `run`
* **Stemming** - Reduce bords into their base form/stem.
    * Samme goal as lemmatization, but another approach.
    * Done by chopping of prefixes and suffixes to get the base form/stem.
    * This approach is less CPU intensive, so if no high accuracy is neccessary, this might be a better approach.

### Supervised & Unsupervised Training

* **Supervised** = learning with answers given.
    * The training data includes both the input and the correct answer (output).
* **Unsupervised** = learning to find patterns without answers.
    * The data only includes inputs, with no correct answers given.

### Generative AI
> The field of AI which is used to freate content of any format (text, images, videos, ...)

### Foundation Models
> Model trained on vast amount of data (unsupervised) which is applicable to a lot of tasks and is not task-centric.

## Language Model
> Models that can predict the next token based on the previous sequence of tokens (context) are Language Models.

* Mathemeticall a language model is a probability distribution over *all the words that occur in a language*
* Chain Rule of probility
    * Calculating the most probable next word based on the previous tokens.

## Corpus Of Data
A corpus is just the body of data you feed into a system so it can learn from it.

## Word Embeddings
* aka `word2vec`
* Vector representation of words in a high dimensional space (many dimensions in othr words).
* Such a vector representation would contain the semantic (meaning) and syntactic (grammar) relationship between words based on the usage of the words found in the data corpus.
    * Semantic (meaning): `god` and `puppy` are related
    * Syntactic (grammar): `run` and `running` are the same word.

### Architecture Types 
There are different Architecture Types To Train/Get Word Embeddings.    

* **Continious Bag Of Words (CBOW)**
    * predicts the missing word from its neighbors
    * Better for when data is limited
    * Faster to train.
* **Skip-Gram Architecture**
    * predicts the neighbors from the center word. 
    * Better for when data is large

## RRN and LSTM

* **Recurrent Neural Network (RRN)**
* **Long short-term Memory**

## Compute Unified Device Architecture (CUDA)

### CUDA
CUDA is a parallel computing platform and programming model developed by NVIDIA that lets developers use the GPU (graphics processing unit) for general-purpose computing.
It allows coordination between the CPU and GPU, but the GPU — not the CPU — is what does the parallel computation.t Te CPU manages tasks, the GPU does the heavy parallel lifting.

### CUDA COre
* A CUDA Core is basically a single processing unit inside an NVIDIA GPU that executes one part of a parallel task.
* A CPU has a few powerful cores that handle complex tasks one after another.
* A GPU has thousands of smaller CUDA cores that handle many simple tasks at the same time — perfect for graphics rendering and AI computations.

### Tensor Core

* A Tensor Core is a specialized type of core inside newer NVIDIA GPUs, designed to speed up matrix and tensor (multi-dimensional array) math, which is the backbone of deep learning.
* CUDA Cores → handle general parallel math (like adds, multiplies, etc.).
* Tensor Cores → handle matrix multiplications and accumulations (the heavy stuff in neural networks) much faster and with mixed precision.
* Tensor Cores are specialized hardware units in NVIDIA GPUs built to accelerate deep learning computations far beyond what regular CUDA cores can do.

---

## History Of LLMs

* **Rule-Based Language Models** - Rules & Regex (but extremely hard for an entire language)
* **Statistical Language Models** - Based on patterns learned from huge data sets.
    * **N-Gram Model** 
        * Used conditional probability to generate next token.
        * More scaleable thant Rule Based Language models (could ingest huge amounts of data)
        * Used an idea of "context window"
    * N-Gram Types
        * *Unigram (1-gram)* - Each word im a sequence is considered an individual token with no dependency.
        * *Bigram (2-gram)* - Sequence consists of a pair of items where the occurance of the latter depend on the former. 
            * It's like a sliding window with a size of 2 items going through the whole sequence.
            * Ex: `She likes icecream the most` -> `she likes`, `likes icrecream`, `icecream the`, `the most`,
        * *Trigram (3-gram)* - Like 2-gram, but the sliding window size is 3.
            * Ex: `She likes icecream the most` -> `she likes icrecream`, `likes icrecream the`, `icecream the most`
        * *n-gram* - A sliding window if size n.
    * The challenge: If you have a bigram, the context window is too small, so it's not aware of the a relation between a word at the beginning and end of the sentence.
* **Neural Language Models**
    * Meant to address limittions of *n-gram* models.
    * To caputre semantic relationship between words it uses: 
        * Feed-forward neural architecture
        * Distributed word respresentation (*word embeddings*)
    * The word embeddigns/vectors were fed into the neural architecture.

---

## Foundation Models 

### Parameters
> The size of a model is measured by the amount of parameters.

### Training Process
* Big Data + Transformer Architecture allows to Train a model now
* **Training Types**
    * *Pre-Training* - Model takes the raw data as input - with an **objective function** - and performs self-supervised learning that doesn't require labels.
        * *Objective Function* is the rule that tells the model how wrong it is and helps it learn to make better predictions.
            * For most LLMs, the objective function is the cross-entropy loss — it measures how far off the model’s predicted word probabilities are from the actual correct word.
            * Other non language models might have "predicting the right next pixel".
    * *Fine-tuning* - Customize the pre-trained model to become good at a specific task (without changing the weights significantly that came from pre-training)
        * Pre-training was general school, fine tuning is specializing.
        * During fine tuning, the new model transfers knowledge from its pretraining (basic school).

### Benefits

* **Reusability** - The pre-training is the heavy lifting, which can then be reused for finetuning to a specific domain which is less expensive and intensive.
* **Elimination Of Annotation** - No need to have labeled data (cause of self supervision), making the data preparation much easier.
* **Multimodality** - Capability to take information in varios formats and generate output in any format.

### Risks

* **Environmental Impact**
* **Inherent Bias** - The available data does not express all opinions and ideas, causing bias
* **Privacy & Security** - Used data can contain IP and sensitive content that is not intended to be shared
* **Hallicunations** - Models are trained to predict the best nest word, not the truth.
* **Explainability** - Hard to decode and understand the output that is generated

## Tips

1. Extract Strategic Insights

"Act like a strategy consultant. Identify the 5 most valuable insights and explain what decisions each one informs."

AI becomes your McKinsey analyst.

2. Turn Information Into Action

"Translate this into a 5-step plan with clear owners, quick wins, and measurable results."

AI becomes your project manager.

3. Surface Hidden Assumptions

"Reveal the unstated assumptions or blind spots shaping this argument - and what changes if they're wrong."

AI becomes your devil's advocate.

4. Compare Opposing Views

"Map this idea against two competing perspectives. Show where they align, where they differ, and which context fits each."

AI becomes your debate moderator.

5. Distill for a Specific Role

"Filter this through the lens of a [role]:

- Marketer → What drives reach or conversion
- Founder → What affects cash flow or growth
- Analyst → What changes the metrics"

AI becomes your specialist advisor.

6. Build a Reusable Model

"Extract the repeatable framework hidden in this text. Label each stage, its input, and output."

AI becomes your systems architect.

7. Extract Contrarian Takeaways

"Find insights that would challenge smart peers - still credible, but unexpected. Write each as a sharp one-liner."

AI becomes your thought provocateur.

8. Identify Leverage Points

"Highlight the 3 leverage points where small actions could create outsized results. Explain why each one matters."