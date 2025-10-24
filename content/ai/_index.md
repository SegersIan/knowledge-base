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

### Supervised & Unsupervised Training

* **Supervised** = learning with answers given.
    * The training data includes both the input and the correct answer (output).
* **Unsupervised** = learning to find patterns without answers.
    * The data only includes inputs, with no correct answers given.

### Generative AI
> The field of AI which is used to freate content of any format (text, images, videos, ...)

### Foundation Models
> Model trained on vast amount of data (unsupervised) which is applicable to a lot of tasks and is not task-centric.



## Introduction




## Readings

* https://www.oneusefulthing.org/p/gpt-5-it-just-does-stuff
* https://userjot.com/blog/best-practices-building-agentic-ai-systems
* Prompt Engineering
  * [Claude Prompt Engineering](https://docs.claude.com/en/docs/build-with-claude/prompt-engineering/overview)
  * [Prompt Engineering Book](https://www.oreilly.com/library/view/prompt-engineering-for/9781098153427/) (Read chapter 1...3) for conceptual foundation
* https://developers.llamaindex.ai/python/framework/module_guides/workflow/#workflows
* https://research.trychroma.com/context-rot
* https://newsletter.pragmaticengineer.com/p/software-engineering-with-llms-in-2025
* https://newsletter.pragmaticengineer.com/p/mcp
* [Microsoft AI Product Manager](https://www.coursera.org/professional-certificates/microsoft-ai-product-manager/paidmedia)
* https://martinfowler.com/articles/exploring-gen-ai.html
* https://modelcontextprotocol.io/docs/getting-started/intro
* https://a2a-protocol.org/latest/topics/key-concepts/
* https://arxiv.org/abs/2510.07192v1
* [Defalte LLMS Sets](https://www.scalarlm.com/blog/llm-deflate-extracting-llms-into-datasets/)
* [Project management with Agent](https://github.com/MrLesk/Backlog.md)

