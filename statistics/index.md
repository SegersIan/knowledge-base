# Statistics

Statistics (or statisical analysis)   is a lot like good detective work. The data yields clues and patterns that can ultimately lead to meaningful conclusions.

## Why staticis

This allowes to determine answers to questions which are not economical to answer. You can not count every homeless in a country, thats expensive and time consuming. You can take a small **quality sample** (quality is key!) to then interfere or project the probably number.

Even in best of circumstances, statistial analysis rarely unveils "the truth". We are usaully building circumstancial vased based on imperfect data. As a result, there are numerous reasons that intellectually honest people may disagree about statistical results or their impleications.

Statistics can give some insight who the best baseball player is, but that's not perse what makes up being "the best",  cause there is no *objective* definition of what a "the best baseball player" means.

Smart and honest people will often disagree about that data re trying to tell us.

### Why Learn?

* To summerize huge quantities of data.
* To make better decisions.
* To answer important social questions.
* To recognize patterns that can refine how we do everything from selling diapers to catching criminals.
* To evaluate the effectiveness of policies, programs, drugs, medical procedures, and other innovations.
* To spot those who use statistics for nefarious ends (and lying).


## Basic Experiments

In a good experiment you have "one variable" that differs between your "experiment group" and your "control group". The control group shares everything with the experiment group, except for one variable. For example, the experiment group eats everyday 1 apple, and the other group eats everyday 1 pear.

## Statistical Significance

The analysis has uncovered an association of 2 variables that ia not likely to be product of chance alone. Regresion analysis can for example find a relation between 2 variables and how likely that relationship is by accident or not. If there is a relationship, and it doesn't seem very accidental, it's statistically significant.

## Regression Analysis

The tool to isolate the relationship between to variables, such as smoking and cancer, while holding constant (or "controlling for") the effects of other important variables (such as diet, excercise, weight, ...)

Regression analysis is primarily used to assess the strength and nature of relationships between variables, but it does not directly establish causation. This is also the limitation, we can identify strong relationships, but we cant determine casuality, or in other words "WHY?".

Usually you start with a hyptheses, "I think these 2 variables have a relationship" and then use regression aanlyisis to validagte that hypthese.

### Example

#### The Conclusion

> Eating a bran muffin every day will reduce your chances of getting colon cancer.

#### The Methodology

First they gather detailed information on thousands of people, including how frequently they eat brand muffings and then apply regression analysis:

1. Quantify the association observed between eating bran muffins and contracting colon cancer.
  * E.g. Hypothethical finding that people who eat bran muffins have 9% lower incidence of colon cancer, controlling for the other factors that may affect the incidedence of the disease.
2. Quantify the likelihood that the association (relation) between bran muffings and a lower rate of colong cancer observed is merely a coincidence (a quick in the data for this sample of people), rather than a meaningful insight about the relationship between diet and health.




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
    * The mode is the value that appears most frequently in a dataset. A dataset can have more than one mode (bimodal, multimodal) if multiple values appear with the same highest frequency.
    * *The mode is particularly useful for categorical data where we wish to know which is the most common category.*

**When there is a perfect bell shape distribution, these 3 types of averages would have the exact same value. If the distribution has another shape, these can be widely different and misleading. How these 3 differ exactly from each other, tells something about the distribution.**

#### Distributions

Distributions describe the pattern of data points. Distributions can be of any shape, but there are a few key types.

* **Normal**: Bell Shaped and symmetric around the mean
* **Skewed**: Higher concentration on one end or the other.
    * **Left / Negative Skew**: Long tail on the left. Most data points concentrated on the right side.
    * **Right / Positive Skew**: Long tail on the right. Most data points concentrated on the left side.
* **Bimodal**: There are 2 peaks (modes) instead of one.
* **Multimodal**: More than 2 peaks.
* **Uniform**: All outcomes are equally likely.
* **Exponential**: Right skewed with rapid decrease in frequency as you move away from the mode.
* And many more, here are some visualizations of them
    * [Set 1](assets/distributions_1.png)
    * [Set 2](assets/distributions_2.png)
    * [Set 3](assets/distributions_3.png)

#### Extra Average Types

* **Weighted Mean** accounts for varying significance of data points.
* **Trimmed Mean** reduces the influence of outliers.
    * Calculated by removing a certain percentage of the smallest and largest data points before calculating the arithmetic mean.
* **Midrange offers** a basic central value but is not robust against outliers.
    * The average of the maximum and minimum values in a dataset. It provides a simple measure of central tendency but is highly sensitive to outliers.
    * Formula: (Max Value + Min Value) / 2

### Critically think about statistics

Following are some tipes on how to analyze critically any statistics.

* (Who Says So) Look for bias:
  * A laboratory with someting to prove for the sake of a theory, reputation or a fee.
  * A newspaper whose aim is a good story.
  * Conscious bias:
    * Direct misstatement or ambiguous statements that serves well and cannot be "convicted".
      * E.g. Selecting favourable data (dentist company retrying till they have a study with favourable results)
      * E.g. Favourable measure (use mean instead of a median or .... when they just say "average")
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
    * e.g. This week the deaths was 60% than average, but maybe that's normal ? Seasonal peaks ? Contect and distribution and past trends might be missing to contextualize it.
* (Did somebody change the subject)
  * Switch somewhere betweeen the raw figure and the conclusion.
  * Confusion between one thing and the other.
  * E.g. More reported cases of a disease is not the same as moree cases of the disease. Reporting could have been bad before or lacking. So it can be easily "switched" to give the wrong impression.
  * What people "say or report" is not perse the same as "what they actually do". They might not be enough self aware of their actual behaviour or they lie to present themselves etc... Risk with self reporting.
  * E.g. The price for a prison is more than the price of a luxury hotel. Well you swithc here between the rent you pay versus the TOTAL MAINTENANCE COST of a prison cell.
  * "Be the first in" can be done very easy, if you make it unique enough. (e.g. hotest 2nd of June since 1948)
  * Switch between revenue and net profit casually
* (Does it make sense?)
  * I guess, look at the context, life expectancy will be very different based on your birth date.
  Therefore
  * OVerly specific numbers for a mean can be misleading, as it might give wrong sence of accuracy.
  * E.g. A person needs 100$ to have enough food to survue, so we only give 100$ unemployment support. There are key things missing!
  * Past trends might be facts, but future trends are just best estimate (like weather).
* Framing and misleading representations
  * E.g. a map that colors all stated who have a certain crime rate, big states with low population can easily dominate the whole visualization.
  * E.g. When the scales of a graph are trimmed or tweaked to make the shape look more impressive.
* A hypthosis as conclusion
  * One can find a strong relationship in data (e.g. with regresion analysis), but not the causality, so they then might draw up a hypotheses. You might mistake this as the actual "reason", while it's just "a hypothesis" to explain a statistically signifcant relationship.
