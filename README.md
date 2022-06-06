# CodeAlong: From Distributions to Hypotheses

## Learning Objectives

- To be able to use probability density functions to calculate probability of specific values.

- To identify normally distributed features.
- To perform a hypothesis test to compare numeric data between 2 groups.


```python
import pandas as pd
import numpy as np

import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
from scipy import stats

sns.set_context('talk')
mpl.rcParams['figure.figsize'] = [12,6]
```

## Exploring Distributions 

Dataset: https://archive.ics.uci.edu/ml/datasets/student+performance


```python
pd.set_option('display.max_columns',100)
```


```python
## read in the Data/student/student-mat.csv (it uses ";" as the sep)

# display info and .head

```


```python
## Calculate an Avg Grade column by averaging G1, G2,G3, 
# then divide by 20, and * 100 (to make %'s')

```


```python
## plot the distribution of Avg Grade 

```

> Is it normally distributed?


```python
## use scipy's normaltest

```

- We have our p-value for our normaltest, but what does it mean??
    - Check the docstring for the normaltest to find out the null hypothesis of the test.

### Calculating Probabilities with Scipy's  Probability Density Functions


```python
## Get the mean, std, min, and max for the Avg Grade column

```


```python
## generate a linearly-spaced array of values that span the min to the max

```


```python
## use stats.norm.pdf to get the PDF curve that corresponds to your distribution's values

```


```python
## Plot the histogram again AND then plot the pdf we calculated.

```

> Looks pretty normal! But can we confirm for a fact that its normal?

### Q1: what is the probability of a student getting a score of 90 or above?


```python
## Plot the histogram again AND pdf again

## Add a vpsan to the plot showing the region we want to calc prob for

```

> How can we calculate this probability? Can we use the PDF?


```python
## try making a list of values from 90-100 and getting the pdf values


## Sum the values to get the total probability. 

```

> Whats the flaw to this approach?


```python
## Use the cumulative density function to find prob of 90 OR lower.

```

> Now, we want the opposite probability, probability of being GREATER Than 90.



```python
# calc 1-prob of 90 or lower.

```

- Answer: there is a 2.4% chance of having a score greater than 90.

# Hypothesis Testing

## Q: Do students with internet access have different average grades than students who do not have internet access?

### State The Hypothesis 

- $H_0$ (Null Hypothesis): Students with internet access have the same average grades as students who do not. 
- $H_A$ (Alternative Hypothesis): Students with internet access have significantly different average grades compared to students who do not. 

### Visualize and Separate Groups

- Visualize the histogram of Avg Grade again, but separate it into groups based on the "internet" column.
- Note: when comparing 2 groups with seaborn's histplot, you will want to add `common_norm=False`


```python
## visualize the histobram of Avg Grade again, but separate it by "internet"

```


```python
## Plot a bar plot of the Avg Grade for students with internet vs those that do not have it

```


```python
## Separate the 2 groups into 2 varaibles

```

### T-Test Assumptions

- Since we are comparing a numeric measurement between 2 groups, we want to run a 2-sample (AKA independent T-test).

- The Assumptions are:
    - No significant outliers
    - Normality 
    - Equal Variance 

#### Assumption: No Sig. Outliers


```python
## check yes group for outliers using z-score >3 rule.

```


```python
## check no group for outliers using z-score >3 rule.

```

> No outliers to worry about! Assumption met.

#### Assumption: Normally Distributed Groups


```python
## use normaltest to check if yes group is normally distributed

```


```python
## use normaltest to check if no group is normally distributed

```

>- Did we meet the assumption of normality?

#### Assumption: Equal Variance


```python
## use Levene's test to check if groups have equal variance

```

> Did we meet the assumption of equal variance?

### Perform Final Hypothesis Test (T-Test)

- Since we met all of the assumptions for the test we can proceed with our t-test.
    - Next class we will discuss what we would do if we did NOT meet the assumptions.


```python
## run stats.ttest_ind on the 2 groups

```

> What is our p-value? Is it less than our alpha of .05? What does this mean?

>Our T-Test returned a p-value of `____`. Since p `</>`.05, we `can reject/fail to reject` the null hypothesis that students with internet access have the same average grades as students who do not. 

We therefore conclude that there `is/is not` a significant difference in Average Grades between students who do/do not have internet access.

Our visualization below shows that students with internet access have `HIGHER/LOWER/EQUAL` average grades.


```python
## Add a summary visual to support our results.

```

 
