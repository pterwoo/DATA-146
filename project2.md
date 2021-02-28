# Project 2

## Describe continuous, ordinal and nominal data. Provide examples of each. Describe a model of your own construction that incorporates variables of each type of data. You are perfectly welcome to describe your model using english rather than mathematical notation if you prefer. Include hypothetical variables that represent your features and target.

Continuous data: Data that represents measurements. Length of an object in centimeters would be an example of continuous data. 
Ordinal Data: Data that is ordered by rank (1st, 2nd, 3rd, etc.). Any numerical ranking system is considered ordinal data.
Nominal Data: Categorical data that is labled with numbers. Zip codes are nominal data. 

*Model?*

## Comment out the seed from your randomly generated data set of 1000 observations and use the beta distribution to produce a plot that has a mean that approximates the 50th percentile. Also produce both a right skewed and left skewed plot by modifying the alpha and beta parameters from the distribution. Be sure to modify the widths of your columns in order to improve legibility of the bins (intervals). Include the mean and median for all three plots.

To do this, 
```
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt

n = 1000
a = 5
b = 5
#np.random.seed(10)
dataset = np.random.beta(a, b, size = n)
```
We can examine whether or not the mean lies in the 50th percentile by graphing. 
```
plt.figure(figsize = (8, 8))
plt.hist(dataset, rwidth = 0.8)
plt.show()
```
We can see that the distribution follows a standard bell curve, and therefore the mean does approximate the 50th percentile

To create a right skewed plot:
```
n = 1000
a = 0.5
b = 1
#np.random.seed(10)
rskew = np.random.beta(a, b, size = n)

plt.figure(figsize = (8, 8))
plt.hist(rskew, rwidth = 0.8)
plt.show()
```
To create a left-skewed plot:
```
n = 1000
a = 1
b = 0.5
#np.random.seed(10)
lskew = np.random.beta(a, b, size = n)

plt.figure(figsize = (8, 8))
plt.hist(lskew, rwidth = 0.8)
plt.show()
```
Here are the means of each of the plots:
```
np.mean(dataset)
np.median(dataset)

np.mean(rskew)
np.median(rskew)

np.mean(lskew)
np.median(lskew)
```
## Using the gapminder data set, produce two overlapping histograms within the same plot describing life expectancy in 1952 and 2007. Plot the overlapping histograms using both the raw data and then after applying a logarithmic transformation (np.log10() is fine). Which of the two resulting plots best communicates the change in life expectancy amongst all of these countries from 1952 to 2007?

First, read in the data and slice out the desired values
```
df = pd.read_csv('gapminder.tsv', sep="\t")

idx_df52 = df['year'] == 1952
lifeExp52= (df[idx_df52])['lifeExp']

idx_df07 = df['year'] == 2007
lifeExp07= (df[idx_df07])['lifeExp']
```
Then, create bins to make the intervals consistent for both years and plot 
```
min_year = df['lifeExp'].min()
max_year = df['lifeExp'].max()

min_exp = df['lifeExp'].min()
max_exp = df['lifeExp'].max()
n_bins = 10
my_bins = np.linspace(min_exp, max_exp, n_bins + 1)

plt.figure(figsize=(6, 6))
plt.hist(lifeExp52, rwidth=0.9, label= '1952', alpha=0.5, bins = my_bins)
plt.hist(lifeExp07, rwidth=0.9, label= '2007', alpha=0.5, bins = my_bins)
plt.xlabel('Life Expectancy')
plt.ylabel('Number of Countries')
plt.show()
```
The resulting plot looks like this:

![](52_07_life_exp.PNG)

To get the ```numpy.log10``` transformation plot:

```
log_lifeExp07 = np.log10(lifeExp07)
log_lifeExp52 = np.log10(lifeExp52)

log_min_exp = np.log10(df['lifeExp'].min())
log_max_exp = np.log10(df['lifeExp'].max())
n_bins = 10
my_logbins = np.linspace(log_min_exp, log_max_exp, n_bins + 1)

plt.figure(figsize=(6, 6))
plt.hist(log_lifeExp52, rwidth=0.9, label= '1952', alpha=0.5, bins = my_logbins)
plt.hist(log_lifeExp07, rwidth=0.9, label= '2007', alpha=0.5, bins = my_logbins)
plt.xlabel('$\log_{10}$ Life Expectancy')
plt.ylabel('Number of Countries')
plt.show()
```
The resulting plot: 

![](52_07_log_life_exp.PNG) 

Comparing the two, you find that the second plot is the better visual representation of overall change. 
The relatively high variances of the first plot's distributions make it slightly more difficult to gauge
the difference, whereas the second plot's distributions are easier to spot out the difference.

## Using the seaborn library of functions, produce a box and whiskers plot of population for all countries at the given 5-year intervals. Also apply a logarithmic transformation to this data and produce a second plot. Which of the two resulting box and whiskers plots best communicates the change in population amongst all of these countries from 1952 to 2007?

To create a boxplot of population of all countries at all the years in the dataset: 
```
import seaborn as sns

plt.figure(figsize=(6, 6))
sns.boxplot(x=df['year'], y=df['pop'], color='blue')
plt.ylabel('Population')
plt.show()
```
The plot looks like this:

![](pop_box.PNG)

The same plot with logarithmic transformation using ```numpy.log10()```
```
plt.figure(figsize=(6, 6))
sns.boxplot(x=df['year'], y=np.log10(df['pop']))
plt.ylabel('Population')
plt.show()
```
This is the result:

![](log_pop_box.PNG)

Again, the boxplot with the log transform communicates the change in population better, but this time the difference between the two graphs are very apparent. The raw data plot shows the outliers increasing by the years and the actual boxes are squeezed into the bottom of the plot, making it impossible to tell how most populations generally changed. This is due to the large outliers that deviate significantly from the mean/median; the outliers are so much bigger than the average that the averages are all squeezed into the bottom and not legible. The log transform data reduces the difference between the mean and the large outliers, and display the boxplots in a legible, easy to read manner. 
