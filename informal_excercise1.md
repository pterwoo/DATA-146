# **Informal Excercise Response**

## Get a list of all the years in this data, without any duplicates. How many unique values are there, and what are they?
To find a list of all the years in this data:
```
data['year'].unique()
```
it returns [1952, 1957, 1962, 1967, 1972, 1977, 1982, 1987, 1992, 1997, 2002, 2007]. 

To find the number of unique values: 
```
len(data['year'].unique())
```
There are 12 unique years.

## What is the largest value for population (pop) in this data? When and where did this occur?
To obtain the largest value for population in this data, 
```
max_pop = data['pop'].max()
```
max_pop equals to 1318683096, which is the largest population in the dataset. 

To locate when and where this occurred: 
```
max_pop_idx = data['pop'].idxmax()
data.loc[max_pop_idx]
```
Running this code shows that the largest population in the dataset occurred in China, 2007. 

## Extract all the records for Europe. In 1952, which country had the smallest population, and what was the population in 2007?
First, to subset records for Europe, 1952
```
idx_europe = data['continent'] == 'Europe'
data_europe = data[idx_europe]
idx_52eu = data_europe['year'] == 1952
data_52eu = data_europe[idx_52eu]
```
Then, we can find which of these countries from Europe 1952 had the smallest population:
```
minpop_52eu_idx = data_52eu['pop'].idxmin()
mipop_52eu = data_52eu.loc[minpop_52eu_idx]
```
The country with the smallest population in Europe 1952 was Iceland. 

```
iceland_data_idx = data_europe['country'] == 'Iceland'
iceland_data = data_europe[iceland_data_idx]
icelandpop2007 = (iceland_data[iceland_data['year'] == 2007])['pop']
```
The code returns 301931, which is the population of Iceland in 2007. 


