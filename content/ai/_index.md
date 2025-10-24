---
bookCollapseSection: true
title: "AI & ML"
math: true
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

## RRN and LSTM

* **Recurrent Neural Network (RRN)**
* **Long short-term Memory**

## Transformer
* [Attention Is All You Need - Paper](https://arxiv.org/abs/1706.03762)

