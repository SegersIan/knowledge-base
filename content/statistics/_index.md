---
bookCollapseSection: true
title: "Statistics"
---
# Statistics

Statistics (or statistical analysis)   is a lot like good detective work. The data yields clues and patterns that can ultimately lead to meaningful conclusions.

## Why statistics

This allows to determine answers to questions which are not economical to answer. You can not count every homeless in a country, thats expensive and time consuming. You can take a small **quality sample** (quality is key!) to then interfere or project the probably number.

Even in best of circumstances, statistical analysis rarely unveils "the truth". We are usually building circumstantial based based on imperfect data. As a result, there are numerous reasons that intellectually honest people may disagree about statistical results or their implications.

Statistics can give some insight who the best baseball player is, but that's not perse what makes up being "the best",  cause there is no *objective* definition of what a "the best baseball player" means.

Smart and honest people will often disagree about that data re trying to tell us.

### Why Learn?

* To summarize huge quantities of data.
* To make better decisions.
* To answer important social questions.
* To recognize patterns that can refine how we do everything from selling diapers to catching criminals.
* To evaluate the effectiveness of policies, programs, drugs, medical procedures, and other innovations.
* To spot those who use statistics for nefarious ends (and lying).


## Basic Experiments

In a good experiment you have "one variable" that differs between your "experiment group" and your "control group". The control group shares everything with the experiment group, except for one variable. For example, the experiment group eats everyday 1 apple, and the other group eats everyday 1 pear.

## Statistical Significance

The analysis has uncovered an association of 2 variables that ia not likely to be product of chance alone. Regression analysis can for example find a relation between 2 variables and how likely that relationship is by accident or not. If there is a relationship, and it doesn't seem very accidental, it's statistically significant.

## Regression Analysis

The tool to isolate the relationship between to variables, such as smoking and cancer, while holding constant (or "controlling for") the effects of other important variables (such as diet, exercise, weight, ...)

Regression analysis is primarily used to assess the strength and nature of relationships between variables, but it does not directly establish causation. This is also the limitation, we can identify strong relationships, but we cant determine causality, or in other words "WHY?".

Usually you start with a hypotheses, "I think these 2 variables have a relationship" and then use regression analysis to validate that hypothesi.

### Example

#### The Conclusion

> Eating a bran muffin every day will reduce your chances of getting colon cancer.

#### The Methodology

First they gather detailed information on thousands of people, including how frequently they eat brand muffin's and then apply regression analysis:

1. Quantify the association observed between eating bran muffins and contracting colon cancer.
  * E.g. Hypothetical finding that people who eat bran muffins have 9% lower incidence of colon cancer, controlling for the other factors that may affect the incidence of the disease.
2. Quantify the likelihood that the association (relation) between bran muffin's and a lower rate of colon cancer observed is merely a coincidence (a quick in the data for this sample of people), rather than a meaningful insight about the relationship between diet and health.

## Descriptive Statistic (aka Summary Statistic)

A simplification of a complex data set or array of data. We perform calculations that reduce a complex array of data into a handful of numbers that describe those data. These descriptive statistics give us a manageable and meaningful summary of the underlying phenomenon. But simplification invites abuse.

Examples Descriptive Statistic:
  * The health of the Belgian middle class
  * Olympic gymnastics performance

## Statistical Measures

### The Mean

What most people understand as "average", although, more specific its the *Arithmetic Mean* that most people assume what is referred to.

## The Median
What is the middle value? 50% of values are below and 50% of values are above the median.

* The median is the middle value in a dataset when the data points are arranged in ascending or descending order. If there is an even number of observations, the median is the average of the two middle numbers.
* *The median is useful when the data has outliers or is skewed, as it is not affected by extreme values.*

## The Mode
For what value is the highest concentration? Let's say, there is no bigger group than the group that earns 5000 EUR.

* The mode is the value that appears most frequently in a dataset. A dataset can have more than one mode (bimodal, multi-modal) if multiple values appear with the same highest frequency.
* *The mode is particularly useful for categorical data where we wish to know which is the most common category.*

## Percentiles

Tells you what percentage of a dataset falls below a certain point.

For example:

If you're in the 90th percentile in a test, that means you scored higher than 90% of the people who took the test.
Similarly, if a value is at the 25th percentile, it means that 25% of the data points are below that value.

 The 50th percentile is also known as the median, meaning half the data is below it and half is above.

## Standard Deviation

How spread out the values in a dataset are from the mean (average). It measures the dispersion of the values.

* If the standard deviation is small, it means the data points are close to the mean, or the values are clustered tightly around the average.
  * If the test scores in a class have a small standard deviation, most students scored around the same as the average score.
* If the standard deviation is large, it means the data points are more spread out, or the values vary widely from the average.
  * If the standard deviation is large, students' scores vary a lot—some did much better or worse than the average.


## P-Valu

### What’s a p-value?

A **p-value** helps you decide if something you’re testing in an experiment is just a coincidence or if it’s likely a real effect. It’s basically a number that tells you how surprising your results are if the thing you’re testing isn’t actually doing anything.

### Imagine this:

Let’s say you’re flipping a coin, and you think the coin might be biased (like maybe it lands on heads more than tails). Normally, a fair coin should land on heads **50% of the time** and tails **50% of the time**, right?

Now, you flip the coin 10 times and get **8 heads**. This seems like a lot of heads, but before saying the coin is unfair, you want to know: “Could this just happen by chance?”

### Here’s where the p-value comes in:
- The **p-value** is a number that answers the question: **If the coin is really fair (no bias), how likely would it be to get 8 heads (or something even more extreme)?**
- If the p-value is very small (like 0.01 or 0.001), it means getting 8 heads (or more) by pure chance would be very rare if the coin were truly fair. So you’d suspect the coin might actually be biased.
- If the p-value is bigger (like 0.3 or 0.5), it means getting 8 heads could easily happen just by chance, and there’s no good reason to think the coin is unfair.

### How do you use it?

Scientists pick a cutoff number (usually **0.05**) to decide:
- If the **p-value** is **smaller** than 0.05, you say: “This is unlikely to be a coincidence. There might be something real happening here,” and you reject the idea that the coin is fair.
- If the **p-value** is **bigger** than 0.05, you say: “This could easily be a coincidence,” and you don’t reject the idea that the coin is fair.

### In short:
- **Small p-value** (like 0.01): Your results are surprising, and something interesting might be going on.
- **Big p-value** (like 0.3): Your results aren’t surprising, and it could just be random chance.

Hope that makes it clearer! Let me know if you need more examples. :)

## How to Lie with statistics

### The Sample With the Built-In Bias

When there is a poll or statistic, one must scrutinize the sample which was used to calculate the statistic. Getting an unbiased sample is extremely hard or near to impossible?

Example: The avg salary of a Yale student of the 1924 graduate is now earning 25000 Dollar/Year. Did they send a questionnaire to all students (did they have their address), maybe those who they don't have the address of are the super successful, or they all passed away and so on. Next, those with known addresses are now already a biased set that might miss out on significant higher or lower earners. How many respond? Maybe 10% ? What differentiates the onces who feel like responding from the others? When they do respond, are they being honest. People dare to lie , a lot, on questionnaires, interviews and poll. Consciously or subconsciously.

Just going on the street and interview people is biased, based on the place, time and maybe who the interviewers feels attracted to.

**A purely random sample is hard, almost impossible to come by. Ask yourself how a sample can be biased.**

### The Well Chosen Average

There are different types of averages that one can "conveniently" use and not lie.

* **The Mean**: What most people understand as "average", although, more specific its the *Arithmetic Mean* that most people assume what is referred to.
    * The Mean has 3 variations again:
        * Arithmetic:
        * Geometric:
        * Harmonic:
* **The Median**: What is the middle value? 50% of values are below and 50% of values are above the median.
    * The median is the middle value in a dataset when the data points are arranged in ascending or descending order. If there is an even number of observations, the median is the average of the two middle numbers.
    * *The median is useful when the data has outliers or is skewed, as it is not affected by extreme values.*
* **The Mode**: For what value is the highest concentration? Let's say, there is no bigger group than the group that earns 5000 EUR.
    * The mode is the value that appears most frequently in a dataset. A dataset can have more than one mode (bimodal, multi-modal) if multiple values appear with the same highest frequency.
    * *The mode is particularly useful for categorical data where we wish to know which is the most common category.*

**When there is a perfect bell shape distribution, these 3 types of averages would have the exact same value. If the distribution has another shape, these can be widely different and misleading. How these 3 differ exactly from each other, tells something about the distribution.**

#### Distributions

Distributions describe the pattern of data points. Distributions can be of any shape, but there are a few key types.

* **Normal**: Bell Shaped and symmetric around the mean
* **Skewed**: Higher concentration on one end or the other.
    * **Left / Negative Skew**: Long tail on the left. Most data points concentrated on the right side.
    * **Right / Positive Skew**: Long tail on the right. Most data points concentrated on the left side.
* **Bimodal**: There are 2 peaks (modes) instead of one.
* **Multi-modal**: More than 2 peaks.
* **Uniform**: All outcomes are equally likely.
* **Exponential**: Right skewed with rapid decrease in frequency as you move away from the mode.
* And many more, here are some visualizations of them
    * [Set 1](../assets/distributions_1.png)
    * [Set 2](../assets/distributions_2.png)
    * [Set 3](../assets/distributions_3.png)

#### Extra Average Types

* **Weighted Mean** accounts for varying significance of data points.
* **Trimmed Mean** reduces the influence of outliers.
    * Calculated by removing a certain percentage of the smallest and largest data points before calculating the arithmetic mean.
* **Midrange offers** a basic central value but is not robust against outliers.
    * The average of the maximum and minimum values in a dataset. It provides a simple measure of central tendency but is highly sensitive to outliers.
    * Formula: (Max Value + Min Value) / 2

### Critically think about statistics

Following are some types on how to analyze critically any statistics.

* (Who Says So) Look for bias:
  * A laboratory with something to prove for the sake of a theory, reputation or a fee.
  * A newspaper whose aim is a good story.
  * Conscious bias:
    * Direct misstatement or ambiguous statements that serves well and cannot be "convicted".
      * E.g. Selecting favorable data (dentist company retrying till they have a study with favorable results)
      * E.g. Favorable measure (use mean instead of a median or .... when they just say "average")
  * Unconscious bias:
    * By using "big names" like "cornel university" but then the conclusion was from the writer, not from the referenced study.
* (How Does he know?) Biased Samples:
  * The sample which was used can be biased, if a questionnaire is sent out and only 10% responses, this creates a very real risk that the sample is biased.
  * Reported correlation:
    * Is the correlation big enough to have meaning? Is it significant enough?
* (What's missing) What key data, information or context is missing from provided information?
  * Is this a mean, median or mode average?
  * What is the probable error or standard error
  * What is the distribution?
  * Bigger picture data ?
    * e.g. This week the deaths was 60% than average, but maybe that's normal ? Seasonal peaks ? Context and distribution and past trends might be missing to contextualize it.
* (Did somebody change the subject)
  * Switch somewhere between the raw figure and the conclusion.
  * Confusion between one thing and the other.
  * E.g. More reported cases of a disease is not the same as more cases of the disease. Reporting could have been bad before or lacking. So it can be easily "switched" to give the wrong impression.
  * What people "say or report" is not perse the same as "what they actually do". They might not be enough self aware of their actual behavior or they lie to present themselves etc... Risk with self reporting.
  * E.g. The price for a prison is more than the price of a luxury hotel. Well you switch here between the rent you pay versus the TOTAL MAINTENANCE COST of a prison cell.
  * "Be the first in" can be done very easy, if you make it unique enough. (e.g. hottest 2nd of June since 1948)
  * Switch between revenue and net profit casually
* (Does it make sense?)
  * I guess, look at the context, life expectancy will be very different based on your birth date.
  Therefore
  * OVerly specific numbers for a mean can be misleading, as it might give wrong sense of accuracy.
  * E.g. A person needs 100$ to have enough food to survive, so we only give 100$ unemployment support. There are key things missing!
  * Past trends might be facts, but future trends are just best estimate (like weather).
* Framing and misleading representations
  * E.g. a map that colors all stated who have a certain crime rate, big states with low population can easily dominate the whole visualization.
  * E.g. When the scales of a graph are trimmed or tweaked to make the shape look more impressive.
* A hypothesis as conclusion
  * One can find a strong relationship in data (e.g. with regression analysis), but not the causality, so they then might draw up a hypotheses. You might mistake this as the actual "reason", while it's just "a hypothesis" to explain a statistically significant relationship.
