# Statistics

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
