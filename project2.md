# Project 2

## Describe continuous, ordinal and nominal data. Provide examples of each. Describe a model of your own construction that incorporates variables of each type of data. You are perfectly welcome to describe your model using english rather than mathematical notation if you prefer. Include hypothetical variables that represent your features and target.

Continuous data: Data that represents measurements. Length of an object in centimeters would be an example of continuous data. 
Ordinal Data: Data that is ordered by rank (1st, 2nd, 3rd, etc.). Any numerical ranking system is considered ordinal data.
Nominal Data: Categorical data that is labled with numbers. Zip codes are nominal data. 

*Model?*

## Comment out the seed from your randomly generated data set of 1000 observations and use the beta distribution to produce a plot that has a mean that approximates the 50th percentile. Also produce both a right skewed and left skewed plot by modifying the alpha and beta parameters from the distribution. Be sure to modify the widths of your columns in order to improve legibility of the bins (intervals). Include the mean and median for all three plots.

To do this, 
```
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



















