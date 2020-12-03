+++
title = "Statistics"
date = 2019-02-27

[taxonomies]
tags = ["Statistics"]
categories = ["Notes"]
+++

A link to notes (PDF) I had when I took a statistics unit a while ago. Not guaranteed to be correct.

<!-- more -->

# Introduction
Statistics the science of generalizing knowledge from data.
Population complete set of elements being studied.

Variations in sampling

 - Sampling variation/Intrinsic variation :: is variation caused by sampling
 - Variability :: vary from the mean

z critical
confidence interval
critical value

## Normal distribution
Why normal distribution is important:
 - Empirical rule
 - Underlies distribution of P values which are used to test hypothesis


# Measures of central tendency
## Mean

### Arithmetic mean

{% katex(block=true) %}
\bar x = \dfrac{\sum\limits^{n}_{i=1} x_i }{n}
{% end %}


### Sample mean
A point estimator of the population mean:

{% katex(block=true) %}
\bar x = \dfrac{\sum\limits^{n}_{i=1} x_i }{n}
{% end %}


### Population mean
{% katex(block=true) %}
\mu = \dfrac{\sum\limits^{n}_{i=1} x_i }{N}
{% end %}

## Mode
Most repeated

## Median
Value in the middle


# Measures of spread/variability
Spread is variance, how spread out is the graph?

## Ways to measure variation
### Range
{% katex(block=true) %}
Range = max\ value - min\ value
{% end %}
## Variance
 Applications in:
  - QA
  - Ops

 In finance risk is often another term for a stock's variance.
 Some stocks are steady (low risk) but offer lower potential returns.
 Others are swing wildly (high risk) but offer more potential upside.

### Population variance ({% katex(block=false) %}\sigma^2{% end %})
{% katex(block=true) %}
\sigma^2 = \dfrac{\Sigma (x_i - \mu)^2}{N}
{% end %}

### Sample variance ({% katex(block=false) %}s^2{% end %})
{% katex(block=true) %}
s^2 = \dfrac{\Sigma (x_i - \bar x)^2}{n-1}
{% end %}

## Standard deviation
Measures the *average* distance your data values are from the mean.
It's also \sqrt{variance}.

Closely grouped data has a large standard deviation and the opposite for spread out data.

It is:
 - never negative
 - never 0 unless there's no deviation at all in the data
 - Greatly affected by outliers

### Sample standard deviation

Lower case /s/ means *sample* standard deviation

{% katex(block=true) %}
s = \sqrt{\frac{\sum\limits^{n}_{i=1} (x_i-\bar x)^2 }{n-1}}
{% end %}

In sample standard deviation we do /n-1/ to *overestimate* the variation
because /-1/ decreases the denominator making the result, s, bigger.


Simpler formula:

{% katex(block=true) %}
s = \sqrt\frac{n\sum\limits^{n}_{i=1} x_i^2 - (\sum\limits^{n}_{i=1} x_i)^2} {n(n-1)} \\
{% end %}

or
{% katex(block=true) %}
 s = \sqrt\frac{n\sum x^2 - (\sum x)^2} {n(n-1)}
{% end %}

### Population standard deviation

Symbol for population standard deviation is \sigma. \\
\mu is population mean.

{% katex(block=true) %}
\sigma = \sqrt\frac{\sum\limits^{n}_{i=1}(x_i-\mu)^2}{N}
{% end %}

We don't divide by n-1 but N because we don't want to overestimate our population.

## Empirical rule
How much proportion or percentage of a dataset will fall within certain std devs from the mean.
Applies only to a *normally* distributed dataset.
Also called 68%, 95%, 99.7% rule. \\
If data is normally distributed then:
 - 68% of data will fall within 1 standard deviation from the mean
 - 95% of data will fall within 2 standard deviation from the mean
 - 99.7% of data will fall within 3 standard deviation from the mean


Data values /within/ 2 standard deviations are *usual*.
Data values /outside/ 2 standard deviations are *unusual*.
A data value outside of 3 standard deviations from the mean is extremely rare.

Given different standard deviations (with different units, values, samples etc), we have to find a way to represent what has more spread.
To do this we use:
  - Coefficient of variation :: translates s in comparison to \bar x as a percentage

{% katex(block=true) %}
c.v. = \frac{s}{\bar x} * 100
{% end %}

  - Z score :: The number of standard deviations away from the mean that a data value lies in. This lets to compare two datasets directly to see which has more variation.

## Sampling distribution of sample mean
When we take many samples of the same size from a *population* and find the sample means \bar x.
The means of those samples follow a normal curve when placed in their own distribution.

## Sampling distribution of sample variance
When we take many samples of the same size from a *normal population* and then fine those sample variances s^2, those sample variances don't follow a normal curve when placed in their own distribution.

They follow the chi-square \chi^2 distribution with n-1 degrees of freedom.

## Chi Squared distribution

Compares sample variance to pop variance.
We try to estimate population variance

{% katex(block=true) %}
\chi^2 = \frac{(n-1) s^2}{\sigma^2}
{% end %}

 - n :: sample size
 - {% katex(block=false) %}s^2{% end %} :: sample variance
 - {% katex(block=false) %}\sigma^2{% end %} :: population variance

A \chi^2 distribution has a tail to the right.

 1. Not symmetrical
 2. Values are non negative -  No 0 in the middle because std and variance can't be 0
 3. As degrees of freedom go up the distribution becomes more symmetrical
 4. Gives critical values for the area to the *right* - Based on area to the right

### Anatomy of the chi-square distribution
   1. There is no one chi distribution
   2. Area (probability) under the curve is 1
   3. The curve is asymptotic; never touches the x axis
   4. 1 is at the left and 0 is at the right
   5. Cumulative probability runs right to left
   6. Probabilities are found in the chi-square table in the same manner as normal curves

### Example 1
Given n = 12 and confidence level = 95%. Find the critical value which make the {% katex(block=false) %}\chi^2{% end %} distribution.

*Solution*

{% katex(block=true) %}
\alpha = 1-0.95 = 0.05 \\

\dfrac{0.05}{2} = 0.025\\

From the table:\\
Using\ 0.025\ as\ P:\ Area\ to\ the\ right \chi^2 critical\ value = 21.29\\

Using\ 0.975\ as\ P:\ Area\ to\ the\ left \chi^2 critical\ value = 3.816

{% end %}

Because we try to estimate pop variance then

{% katex(block=true) %}
\chi^2 = \frac{(n-1) s^2}{\sigma^2}
\rightarrow
\sigma^2= \frac{(n-1) s^2}{\chi^2}
{% end %}


We have two  {% katex(block=false) %}\chi^2{%end%} values A {% katex(block=false) %}\chi^2_{left}{% end %} and {% katex(block=false) %} \chi^2_{right}{% end %}.

From above it's {% katex(block=false) %} \chi^2_{left} = 3.816  \chi^2_{right} = 21.29 {% end %}.

The {% katex(block=false) %}\chi^2_{right}{% end %} is larger therefore when {% katex(block=false) %}(n-1)s^2{% end %} is divided by it, we get a smaller value. Therefore:


Variance:
{% katex(block=false) %}
  \dfrac{(n-1)s^2}{\chi^2_{right}} < \sigma^2 <  \dfrac{(n-1)s^2}{\chi^2_{left}}
{% end %}

Standard deviation:
{% katex(block=false) %}
  \sqrt{\dfrac{(n-1)s^2}{\chi^2_{right}}} < \sigma < \sqrt{\dfrac{(n-1)s^2}{\chi^2_{left}}}
{% end %}


The {% katex(block=false) %}\alpha{% end %} and confidence level are complimentary

This says our pop variance lies within this range with 95% certainty

### Example 2
We sample 10 phone chargers and we have a std dev of 0.15 volts.
Construct a 95% CI for {% katex(block=false) %}\sigma{% end %} and {% katex(block=false) %}\sigma^2{% end %}.

*Solution*

{% katex(block=true) %}
s = 0.15

n  = 10

\alpha = 0.05
{% end %}

{% katex(block=true) %}
\chi^2_{right}\ 0.025 \rightarrow 19.023

\chi^2_{left}\ 0.975 \rightarrow 2.7
{% end %}


{% katex(block=true) %}
\dfrac{(n-1)s^2}{\chi^2_{right}} < \sigma^2 < \dfrac{(n-1)0.15^2}{\chi^2_{left}}
{% end %}

{% katex(block=true) %}
\dfrac{(10-1)0.15^2}{19.023} < \sigma^2 <  \dfrac{(10-1)s^2}{2.7}

0.0105 <  \sigma^2 < 0.075
{% end %}

For voltage specifically use the sqaure root to get: {% katex(block=false) %} 0.1031 < \sigma < 0.2738{% end %}

## F ratio and F distribution
Whether 2 sample variances are equal given the limits of random sampling
We want to know whether a difference is statistically significant or caused by a sampling error.

#### F ratio

{% katex(block=true) %}
F = \dfrac{larger\ sample\ variance}{smaller\ sample\ variance} = \dfrac{s^2_x}{s^2_y}
{% end %}

#### F distribution
The distribution of F ratios
sample df = n - 1

#### Equality of variance
Are the variances equal or not?


# Measures of relative standing
Comparing measures between or within datasets.
This lets you compare the variation of two samples or populations.

## Coefficient of variation
The ratio of standard deviation to the mean as a percentage

{% katex(block=true) %}
c.v. = \frac{s}{\bar x} * 100
{% end %}

## Z score
The number of standard deviations that data value is away from the mean.
Same for sample as well as population.
Z scores can be negative or positive.
A z score at the mean is 0
Z scores can also be usual >= -2 && <= 2 or unusual < -2 && > 2
The larger the z score in terms of absolute value the more rare the data.

Sample
{% katex(block=true) %}
z = \frac{x - \bar x}{s}
{% end %}

Population
{% katex(block=true) %}
z = \frac{x - \mu}{\sigma}
{% end %}

## Quartiles
Data has to be sorted, has to be values.
Go from left to right:
 - Q1 :: bottom 25%
 - Q2 (median) :: bottom 50%
 - Q3 :: bottom 75% of the data
There's no Q4 because that's everything.

|---|---|---|----|----|----|----|----|
| 1 | 3 | 6 | 10 | 15 | 21 | 28 | 36 |
|---|---|---|----|----|----|----|----|

In the sample above:\\
Q1 = 4.5\\
Q2 = 12.5\\
Q3 = 24.5

|---|---|---|----|----|----|----|----|----|
| 1 | 3 | 6 | 10 | 15 | 21 | 28 | 36 | 39 |
|---|---|---|----|----|----|----|----|----|

We pretend in this case that the 15 doesn't exist.\\
Q1 = 4.5\\
Q2 = 15\\
Q3 = 32

## Percentiles
Separates data into 100 parts. We have 99 parts

{% katex(block=true) %}
Percentile\ of\ x = \frac{number\ of\ values\ less\ than\ x}{total\ number\ of\ values}*100
{% end %}

## InterQuartile range (IQR)

75th percentile - 25th percentile


# Population vs sample data
## Population data
The population is defined by the researcher e.g all women, all bulbs produced by a certain company etc.
Populations can be large, it's hard to collect data on each member of a population.

Collecting data on all members of a population is called a [[https://en.wikipedia.org/wiki/Census][census]].

## Sample data
When we need to make a conclusion about our population we use a sample.
A small but well chosen sample can accurately represent the population.

Sample guidelines:
 - All elements in the sample should be part of the population
 - The sample should be representative of the population
 - In most cases (if not all) samples from the population should be independent of each other

Kinds of samples:
 - Random

A sample is always an approximation of the population. Therefore:
 - Sample data sets always have error built into them
 -


## Point estimate
Using a single value from a sample to approximate an entire population parameter.

{% katex(block=true) %}
p = population proportion\ of\ successes

\^{p} = sample proportion\ of\ success = \dfrac{x}{n}

\^{q} = sample proportion\ of\ failure = 1-\^{p}

\^{p} is a *point estimate* for p
{% end %}


You have no idea how accurate the point estimate is.

## Confidence interval
*Range* of numbers used to estimate a population parameter.
Estimates a population proportion from a sample proportion.

They have:
 1. Confidence level (1-\alpha): how confident you are that the actual value of the population parameter will be inside the interval.
    - \alpha is the complement of the confidence level.
    - most common confidence levels:
      * 90% \rightarrow \alpha = 0.1
      * 95% (most used) \rightarrow \alpha = 0.05
      * 99% \rightarrow \alpha = 0.01

Requirements:
 1. A random sample.
 2. Conditions for binomial
    - Fixed number of trials
    - Trials are independent
    - Two outcomes (success or failure)
    - n*p >= 5 and n*q >= 5

Example: The 95% CI for p is 0.38 < p < 0.497
I don't know what p is but I'm 95% sure that it falls between 0.38 and 0.497 of the population

## Critical value
A z score that separates the likely region from the unlikely region.

## Margin of error
Max difference between \^{p} and p.

{% katex(block=true) %}
E = Z_{\alpha/2}\sqrt{\dfrac{\hat{p}-\hat{q}}{n}}
{% end %}

### Example
 We are given that n = 670, \^{p} = 0.85, we also jusqt learned that the standard eror of the sample proportion is SE = p(1-p). Which of
the below is the correct calculation of the 95% confidence interval?

{% katex(block=true) %}
0.85 \pm 1.96 * \sqrt{\dfrac{0.85*0.15}{670}}
{% end %}

# Descriptive statistics
## z-scores
Measure of *distance* from the mean. \\
How far from the mean is a is a given data point.
How many *standard deviations* away (above or below) from the mean is a data point.
Standard deviation here is a unit of measurement like a kg, meter etc.

z-scores are standardized measures where the unit is a standard deviations.

z score of the mean is 0 because it's zero distance from itself.

Like mass of person x is 5 kgs; we can say z-score of x is 1 standard deviations.


### Formula

{% katex(block=true) %}
z_{datapoint} = \frac{data\ point - mean\ value}{standard\ deviation}
{% end %}

#### Population
{% katex(block=true) %}
z_x = \dfrac{x - \mu}{\sigma}
{% end %}


#### Sample
{% katex(block=true) %}
z_x = \dfrac{x - \bar x}{s}
{% end %}


# Correlation
Independent variable should be on the x axis while the dependent variable should be on the y axis.
Correlation seeks a statistical relationship between *two* variables or *bivariate* data.

A regression model is unique to the data it represents.
Adding data will change the regression model.
It's not proper to extrapolate above or below data being evaluated.
How much better is our line of fit compared to only using the mean of the dependent variable.

## Dependence

## Correlation and causation
It is tempting to assume that one variable causes another however, correlation doesn't imply causation.
## Uses of correlation
  - comparing models :: You compare a given model against just the mean of the dependent variable
  - prediction :: useful because they indicate a *predictive* relationship that can be exploited in practice

## Correlation coefficient (r)
Correlation coefficient is a popular way of summarizing a scatter plot into one value between 1 and -1.

  * +ve slope is +ve correlation
  * -ve slope is -ve correlation
  * 0 slope is no correlation

/A weak correlation is closer to 0; whereas a strong correlation is near 1 or -1/

## Steps
### 1. Fit line
Helps fit a straight line through the data
Minimum square distances between fitted line and individual points
###  2. Remember slope
Remembers if slope is pointing upwards or downwards
###  3. Quality of fit of the straight line for the data
Shows how well the slope fits the data based on whether the correlation is weak or strong

## Example
Trying to see whether more fertilizer leads to higher yields of beans

|------------------|---|---|---|---|---|---|---|
| Fertilizer (lbs) | 2 | 1 | 3 | 2 | 4 | 5 | 3 |
|------------------|---|---|---|---|---|---|---|
| Bushels of beans | 4 | 3 | 4 | 3 | 6 | 5 | 5 |
|------------------|---|---|---|---|---|---|---|

| x | y | x \cdot y | x^2 | y^2 |
|---|---|----------|-----|-----|
| 2 | 4 |        8 |   4 |  16 |
| 1 | 3 |        3 |   1 |   9 |
| 3 | 4 |       12 |   9 |  16 |
| 2 | 3 |        6 |   4 |   9 |
| 4 | 6 |       24 |  16 |  36 |
| 5 | 5 |       25 |  25 |  25 |
| 3 | 5 |       15 |   9 |  25 |

{% katex(block=true) %}
\Sigma x 20
\Sigma y 30
\Sigma x \cdot y 93
\Sigma x^2 68
\Sigma y^2 136

r = \dfrac{n(\Sigma x \cdot y) - (\Sigma x)(\Sigma y)}{\sqrt{(n(\Sigma x^2) - (\Sigma x)^2) (n(\Sigma y^2) - (\Sigma y)^2)}}
{% end %}

## Fit
## Residuals/errors
These are values of how far our values are from the line of best fit

## Coefficient of determination

Calculated by: r^2 = SSR/SST

When r^2*100 we get the percentage of results due to SSE





# Simple linear regression
We compare a model of the dependent variable on it's own against
a model of the dependent variable against the independent variable.

Assume:
 - normal distribution
 - both x and y are continuous
 - both x and y are numerical

## Coming up with a regression line
Get the *centroid* point made by \( (\bar x, \bar y) \).
Your line of best fit must pass through the centroid.

{% katex(block=true) %}

\beta_0 = intercept

\beta_1 = gradient

\^{y}_i = \beta_0 + \beta_1 x \rightarrow Similar\ to: y = mx + c\\[2mm]

\beta_1 = \dfrac {\Sigma (x_i - \bar x) (y_i - \bar y)}{\Sigma (x_i - \bar x)^2}\\[1mm]
{% end %}

## SSE (Sum of squared Errors)
TODO
## SST (Total Sum of Squares)
$$\Sigma (x_i - \bar x)^2$$

## SSR (Sum of squares due to regression)
SSR = Sum of squared errors of \bar y alone - Sum of squared errors of best line of fit


# Logistic regression
Dependent variable is binary
We want to link our probabilities back to 0 & 1

Logistic regression seeks to:

 1. *Model* the probability of an event occurring based on the values of an independent variable, which can be categorical or numerical.
 2. *Estimate* the prob that an event occurs for a randomly selected observation vs the prob that the event doesn't occur
 3. *Predict* the effect of a series of vars on a binary response var
 4. *Classify* observations by estimating the prob that an observation is in particular category (e.g bank loan approved or not)

## Probability
## Odds

Odds are probability of something occurring / probability of something not occurring

$$odds = \dfrac{P(occurring)}{P(not\ occurring)}$$

Probability of it not occurring is: 1 - probability of it occurring

$$odds =  \dfrac{p}{q} = \dfrac{p}{1-p}$$

/What about events that have a probability of 1 occurring? We get odds of infinity/

### Examples

#### Flipping a fair coin
Odds of getting heads:

odds(heads) = \dfrac{0.5}{0.5} = 1 or 1:1

#### Rolling a fair die
Odds of getting 1 or 2:

odds(1 or 2) = \dfrac{0.333}{0.666} = \dfrac{1}{2} = 0.5 or 1:2

#### Deck of playing cards
Odds of pulling out a diamond card:

odds(diamonds) = \dfrac{0.25}{0.75} = \dfrac{1}{3} = 0.333 or 1:3

/There are 52 cards in a deck and 4 types of cards (diamond, spade, flowers & hearts) and in equal numbers/

## Odds ratio
A ratio of two odds
We are comparing the likelihood of getting an outcome in two separate "systems"


If we want to know how much we increase the odds of getting an outcome by changing one variable and holding all others constant.
/odds ratio for a variable show how the odds change with 1 unit increase in that variable holding all other variables constant./
e.g
 - What are the odds of getting a loan approved by increasing your credit score  by 1?
 - What are the odds of getting  a heart attack when you increase your bodyweight 1 kg past a certain threshold?


#### Examples
 Say we want to start a casino and want to make some loaded coins to make sure the house wins.
 We may want to know how to load our coin so that the house wins but the players also win a few times to keep them coming.
 We want to know how many more times our loaded coin will get a certain outcome compares to a fair coin.


###### A loaded coin
P(heads) = \dfrac{7}{10} = 0.7 \\
odds(heads) = \dfrac{0.7}{0.3} = 2.333


###### A fair coin
P(heads) = \dfrac{1}{2} = 0.5 \\
odds(heads) = \dfrac{0.5}{0.5} = 1.0

Odds ratio would be:
\dfrac{2.333}{1.0} = 2.333

This means that in the loaded coin we are 2.333 more times likely to get heads than on the fair coin.
Loading the coin by 2 increases the odds of getting a heads by 2.333

## Odds ratio in logistic regression
The odds ratio for a variable in logistic regression represents how the odds change with 1 unit increase in that variable holding all other variables constant.

### Example
By increasing our credit score by one how do we affect the probability of getting a loan approved?

Body weight and sleep apnea. Categories:
 - apnea
 - no apnea

Weight variable has an odds ratio of 1.07

This means a 1 pound increase in body weight increase the odds of having sleep apnea by 1.07.\\
A 10 lbs increase in weight increase the odds to 1.98.\\
A 20 lbs increase raised odds to 3.87.

## Odds vs probability
One could have high odds but still low probability for something.
You may increase your odds of something but the probability of getting that outcome was still low to begin with.
Another may have lower odds but high probability of getting an outcome.

Take the case of people in different ages on different diets and on different drugs and their chances of them getting sick because of it. Younger people have a low probability of getting sick whether or not they do things that increase their odds of getting sick.

Odds can have a large magnitude change even if the underlying probabilities are low.

## Logit

We don't know p and we wish to estimate it. The estimate of p is written src_LANG[headers]{\hat p} (p hat).
We need a function that links the independent variable x axis with probabilities on the y axis.

{% katex(block=true) %}
ln(odds) = ln(\frac{p}{q}) = ln(p) - ln(q) = logit(p)

log_ex = ln\ x
{% end %}

## Regression equation
We are estimating an unknown p for any given linear combo of independent variables.
In the logit function we have 0 to 1 running along our x axis but we want to have them on our y axis.
We can achieve that by taking the inverse of the logit function.

{% katex(block=true) %}

logit(p) =  ln(\dfrac{p}{1-p})\\[3mm]

Where p is between 0 and 1\\[2mm]

logit^{-1}(\alpha) = \dfrac{1}{1+e^{-\alpha}} =  \dfrac{e^{\alpha}}{1+e^{\alpha}}\\[3mm]

log_ex = ln\ x\\[2mm]

logit(p) = ln(\dfrac{p}{1-p}) = \beta_0 + \beta_1 x_1\\[2mm]

\dfrac{p}{1-p} = e^{\beta_0 + \beta_1 x_1}\\[2mm]

p = e^{\beta_0 + \beta_1 x_1}(1-p)\\[2mm]

distribute\\[0.5mm]

p = e^{\beta_0 + \beta_1 x_1} - e^{\beta_0 + \beta_1 x_1} * p\\[2mm]

p +  e^{\beta_0 + \beta_1 x_1} * p = e^{\beta_0 + \beta_1 x_1}\\[2mm]

p(1 + e^{\beta_0 + \beta_1 x_1}) =  e^{\beta_0 + \beta_1 x_1}\\[2mm]

Therefore the estimated regression equation:\\[1mm]

\^p =  \dfrac{e^{\beta_0 + \beta_1 x_1}}{1+ e^{\beta_0 + \beta_1 x_1}}

{% end %}

### Example
Home owners loans
n = 1000
1 approved
0 not aprroved




# Finite math
## Permutations

*order matters*

## Combinations
The number of *different ways* that r objects can be selected from n objects.
If there are n objects, how many different ways can we select *groups* of size r?

Often said as n choose r, denoted as C(n,r)

*Order doesn't matter*
Think of sets.

### Formula
C(n,r) = \dfrac{n!}{r! (n-r)!}


# Discrete distributions
The outcomes are finite and must be integers


# The Binomial Distribution
A type of discrete distribution.

The probability of any given outcome is a combination of both the *number of trials* and the *success rate*.

Binomial Bi two and nomial is a name in our case an outcome, 2 outcomes.
We categorize our outcomes as either a *success* or a *failure*.


## Binomial experiment

### Characteristics

 1. You have to have a *fixed* number of trails.
 2. Trials must be independent - outcome of one trial doesn't affect any other
 3. Each trial has only 2 outcomes a success or a failure
 4. The probability of success remains the same in every trial

### Formula

{% katex(block=true) %}
Probability\ of\ x\ in\ n  = C(n,x) p^x (1-p)^{n-x}
{% end %}

Where (look under [[Finite math]]):
{% katex(block=true) %}
C(n,x) = {}{_n}C{_x} = \frac{n!}{x
!(n-x)!}
{% end %}

 - n: number of trails
 - x: number of successes in n trials
 - p: probability of success in a single trial
 - q: probability of a failure in any trial

### Example
In a die, what is the probability of rolling a 4 is 30%. The die is rolled 10 times.
Find the probability of rolling eight 4s.

*Solution*
{% katex(block=true) %}
p = 0.3

q = 0.7

x = 4

n-x = 10-4 = 6\\[1mm]

{}_{10}C_4 = \frac{10!}{4!(10-4!)} = 210 \\[3mm]

P(x) = C(n,x) p^x (1-p)^{n-x} = 210*0.3^4*0.7^6 = 0.2

{% end %}


# Standard Error/Standard Error of the mean

This is the estimated population standard deviation from the sample standard deviation.
Sample mean is unlikely to be equal to population mean.
Standard deviation of the means of many samples from the population mean.

{% katex(block=true) %}
s.e. = \hat \sigma = \dfrac{s}{\sqrt n}
{% end %}


# ANOVA (ANalysis Of VAriance)

This is the variability among/between sample means vs variability within each sample


{% katex(block=true) %}
H_0: \mu_1 = \mu_2 = \mu_3
{% end %}
\\
Therefore, the samples are *likely* to come from the same population. \\
*Why not multiple t-tests?* The error compounds in each t-test. \\

ANOVA is really a variability ratio:

{% katex(block=true) %}
A\ variability\ ratio = \dfrac{variability\ between\ means}{variability\ within\ distributions}
{% end %}

{% katex(block=true) %}
Variance\ Between + Variance\ Within = Total\ Variance
{% end %}

 - partitioning :: separating total variance into its component parts

If variance between the means is relatively large than within the means ratio
will be much larger than 1 and the samples likely don't come from a common population.

*Overview*

At least one  mean is an outlier and each distribution is narrow; distinct from each other
{% katex(block=true) %}
Reject\ H_0 =  \dfrac{LARGE}{small} \\
{% end %}

Means are fairly close to overall mean and/or distributions overlap a bit, hard to distinguish
{% katex(block=true) %}
Fail\ to\ reject\ H_0 = \dfrac{similar}{similar}
{% end %}

Means are very close to overall mean and/or distributions melt together
{% katex(block=true) %}
Fail\ to\ reject\ H_0 = \dfrac{similar}{LARGE}
{% end %}


## One way ANOVA
Also called single factor ANOVA (ANalysis Of VAriance).

Without getting the avg of the sum of squared deviations

SST (Sum of Squares Total)
 1. Find difference between each data point and overall mean
 2. square the difference
 3. add them up

SSC (Sum of Squares of the Columns)
 1. Difference between each group mean and overall mean
 2. Square the deviations
 3. add them up

SSE (Sum of Squares Error)
 1. Find the difference between each data point and it's own column mean
 2. square each deviation
 3. Add them up

SST = SSE + SSC

Sum of squares:
SS = \Sigma (x-\mu)^2

Sample variance:
{% katex(block=true) %}
s^2 = \dfrac{\Sigma(x-\mu)^2}{n-1}
{% end %}

### Example

H_0: \mu_1 = \mu_2 = \mu_3 \\
H_\alpha: There is at least one difference among the means
\alpha = 0.05

|---|---|---|
| 1 | 2 | 3 |
|---|---|---|
| 1 | 2 | 2 |
| 2 | 4 | 3 |
| 5 | 2 | 4 |


Means within:

{% katex(block=true) %}
\bar x{_1} = \frac{1+2+5}{3} = \frac{8}{3} = 2.67 \\
\bar x{_2} = \frac{2+4+2}{3} = \frac{8}{3} = 2.67 \\
\bar x{_3} = \frac{2+3+4}{3} = \frac{9}{3} = 3 \\
\bar{\bar x} = \frac{1 + 2 + 5 + 2 + 4 + 2 + 2 + 3 + 4}{9} = \frac{25}{9} = 2.78
{% end %}

Means between:


Degrees of freedom:\\

 - k :: number of conditions
 - N :: number of scores

{% katex(block=true) %}
df_{between}: k-1 = 3-1 = 2\\
df_{within}: N-k = 9-3 = 6 \\
df_{total}: 2+6 = 8
{% end %}

From the above we get the F_{critical} from our table.
{% katex(block=true) %}
df_{1} = df_{between}\\
df_{2} = df_{within}
{% end %}

For the above in our table we get F_{critical} of 5.14

{% katex(block=true) %}
SS_{total} = \Sigma(x-\bar{\bar x})^2
SS_{within} = \Sigma
SS_{within} = SS_{total} -SS_{within}
{% end %}

$$ANOVA = \frac{SS_{total} - SS_{within}}{SS_{within}} = \frac{SS_{between}}{SS_{within}}$$

{% katex(block=true) %}
SS_{total} = (1-2.78)^2 + (2-2.78)^2 + ... + (2-2.78)^2 + ... + (4-2.78)^2 = 13.6\\

SS_{within} = (1-2.67)^2 + (2-2.67)^2 + ... + (2-2.67)^2 + ... + (4-3)^2 = 13.34\\

SS_{between} = SS_{total} - SS_{within} = 13.6-13.34 = 0.26\\

Variance_{between} = \frac{SS_{between}}{df_{betweeen}}\\
Variance_{within} = \frac{SS_{within}}{df_{withinn}}

F = \dfrac{Variance_{between}} {Variance_{within}} = \dfrac{\dfrac{0.26}{2}{}}{\frac{13.34}{6}} = \dfrac{0.13}{2.22} = 0.059 \\



F_{critical} = 5.14 \\
F = 0.059

F < F_{critical}

0.059 < 5.14
{% end %}

Therefore, we fail to reject our H_0 \\
/Mean squared between/ is also /variance between/


## Two way ANOVA
Out of scope


# z-test, t-test & p values
How to conduct hypothesis tests on 2 population means.

## t-test

### t value
Shows the difference *within groups* and compares it to difference *between the same groups*.
In the case of the paired t-test we get the t value for *paired* data.

{% katex(block=true) %}
t-value: = \dfrac{\bar x - H_0}{\dfrac{s}{\sqrt{n}}}
{% end %}

# Independent samples (random) t-test

# Matched sample (paired) t-test
The paired t-test - also called two sample, within subjects, repeated measures and dependent samples t-test - is a statistical method used to measure the change within the same sample after an event occurs.
It uses paired or dependent data (where the data in one sample affects the data in the other sample e.g before and after a process such as taking a drug).

#### Properties of the paired t test
  - holds more statistical power as there isn't variability between subjects
  - susceptible to ordering effects
  - used where we care about the difference between each observation
  - assumes the difference between pairs is normally distributed

#### Example
  Paired t-test on the effectiveness of a weight loss drug.

  #+CAPTION: Positive values indicate weight loss and negative values indicate weight gain
   | subject | on drug | on placebo |  d_i |
   |---------|---------|------------|------|
   |       1 |     1.1 |          0 |  1.1 |
   |       2 |     1.3 |       -0.3 |  1.6 |
   |       3 |     1.0 |        0.6 |  0.4 |
   |       4 |     1.7 |        0.3 |  1.4 |
   |       5 |     1.4 |        0.7 |  0.7 |
   |       6 |     0.1 |       -0.2 |  0.3 |
   |       7 |     0.5 |        0.6 | -0.1 |
   |       8 |     1.6 |        0.9 |  0.7 |
   |       9 |    -0.5 |       -2.0 |  1.5 |
   |---------|---------|------------|------|
   |         |         |            |  7.6 |
   #+TBLFM: $4=vsum(@2$4..@10$4)


   - H_0 :: The given weight loss drug has no effect on weight loss.
   - H_1 :: The given weight loss drug leads to weight loss.
   - \alpha :: 0.05 (threshold for whether to accept H_0).
   - d_i :: difference between measurements of each subject
   - \mu_d :: mean difference between the measurements of each subject, if \mu_d = 0 there's no difference between the two measurements.
   - degrees of freedom (df) :: n - 1

{% katex(block=true) %}
\mu_d = \dfrac{\Sigma{d_i}}{n} = \dfrac{7.6}{9} = 0.8444

s = 0.72

n = 9
\bar x = 0.8

H_0 = 0  \tiny \textbf{ null hypothesis is always 0}

df = n - 1 = 9 - 1= 8

t* = \dfrac{1.0 - 0}{\dfrac{0.72}{\sqrt{9}}} = 4.17

p = 0.005

{% end %}

##### Conclusion

The result is significant at p < 0.05
Since p-value (0.005) > than \alpha (0.05), we reject H_0. Therefore, we accept H_1 that our drug is effective at weight loss because there's only 0.005 chance that the weight loss was not because of the drug.

## P values
Get them from the p tables given the z score


# Types of variables

Types of variables:
 - numerical ::
 - derived :: e.g. Body Mass Index
 - transformed :: e.g logarithm
 - qualitative :: non-numeric
   * categorical :: discrete yes or no
 - quantitivative :: numeric
   * discrete ::
   * continuous ::

Exposure and outcome variables
 - predictor ::
 - response ::


 - Cumulative frequency :: summation of frequency


## Numerical
## Binary or categorical
## Rates


# Degrees of freedom (df)

# Hypothesis testing
Testing whether a claim is valid.

# Types of studies
 - observational studies
 - case control study
 - cohort study
 - cross sectional study
 - controlled experimental study
 - before-and-after-type study
 - experimental study
 - blinded


# References

1. [[https://www.youtube.com/user/BCFoltz/][Brandon Foltz Youtube]]
2. [[https://www.youtube.com/user/professorleonard57][Professor Leonard Youtube]]
3. Kirkwood BR, Sterne JAC. 2003. Essential Medical Statistics. 2nd ed., Blackwell.
