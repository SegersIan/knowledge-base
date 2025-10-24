---
bookCollapseSection: true
title: "AI & ML"
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





