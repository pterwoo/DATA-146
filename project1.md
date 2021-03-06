# Project 1 

## Describe what is a package? Also, describe what is a library? What are the two steps you need to execute in order to install a package and then make that library of functions accessible to your workspace and current python work session? Provide examples of how you would execute these two steps using two of the packages we have used in class thus far. Be sure to include an alias in at least one of your two examples and explain why it is a good idea to do so.
A package can be seen as a group of modules, or python files. Libraries are a collection of packages. They usually provide convenient functionalities that allow for users to not have to type out commonly used functions that are not built-in. 
To install a package we would execute the following code (*pandas* and *numpy* will be used as examples):
```
pip install numpy
pip install pandas
```
Then, to import the package/library into into the local workspace: 
```
import numpy 
import pandas
```
alternatively, if I wanted to abbreviate numpy as np and pandas as pd, I would:
```
import numpy as np
import pandas as pd
```
You would want to do this so that when you are calling a function that belongs in the library, you wouldn't have to fully type out "pandas" or "numpy."
```
pd.readcsv() 
```
as opposed to 
```
pandas.readcsv()
```
## Describe what is a data frame? Identify a library of functions that is particularly useful for working with data frames. In order to read a file in its remote location within the file system of your operating system, which command would you use? Provide an example of how to read a file and import it into your work session in order to create a new data frame. Also, describe why specifying an argument within a read_() function can be significant. Does data that is saved as a file in a different type of format require a particular argument in order for a data frame to be successfully imported? Also, provide an example that describes a data frame you created. How do you determine how many rows and columns are in a data frame? Is there an alternate terminology for describing rows and columns?
Dataframes are data structures akin to spreadsheets. The *pandas* library is the most commonly used to handle and work with dataframes in python. 
To read a file (csv as an example) remotely and import it into the local work session, first you must specify the directory of the file being imported. It is convenient to save the directory to a variable. Then, you would use the read_csv function in the pandas library to read in the actual data, taking in the directory as an argument and specifying the separator
```
path_to_data = #directory
df = pd.read_csv(path_to_data, sep = ',')
```
Specifying what comes after the read_ in the function is important, since there are different ways data is stored. The example above deals with a csv (comma separated values) file that have values that are separated by commas, while other forms of data such as tsv (tab separated values) files have values that are separated by tabs. 
To continue on with the example, you can determine how many rows and columns are in the dataframe by executing:
```
df.shape
```
The output lists the rows and columns. Rows and columns combined form the *shape* of the dataframe. 

## Import the gapminder.tsv data set and create a new data frame. Interrogate and describe the year variable within the data frame you created. Does this variable exhibit regular intervals? If you were to add new outcomes to the raw data in order to update and make it more current, which years would you add to each subset of observations? Stretch goal: can you identify how many new outcomes in total you would be adding to your data frame?
Import the gapminder.tsv dataset (will assume that the file is a local folder):
```
path_to_data = gapminder.tsv
df = pd.read_csv(path_to_data, sep = '\t')
```
to examine the year variable: 
```
df[year]
```
This reveals that data was collected in a regular interval of 5 years. The most recent observations were from 2007, therefore data from 2012 and 2017. Since for each row there are 6 columns (country, continent, year, lifeExp, pop, and gdpPercap), it is likely that there will be 12 new outcomes added to the dataframe. 

## Using the data frame you created by importing the gapminder.tsv data set, determine which country at what point in time had the lowest life expectancy. Conduct a cursory level investigation as to why this was the case and provide a brief explanation in support of your explanation.
```
df.loc[df['lifeExp'].idxmin()]
```
Executing this shows that the lowst life expectancy recorded in this dataframe is from Rwanda in 1992, with a life expectancy of 23.599. This could have happened due to the lives lost during the Rwandan Civil War that took place from 1990 to 1994. 

## Using the data frame you created by importing the gapminder.tsv data set, multiply the variable pop by the variable gdpPercap and assign the results to a newly created variable. Then subset and order from highest to lowest the results for Germany, France, Italy and Spain in 2007. Create a table that illustrates your results (you are welcome to either create a table in markdown or plot/save in PyCharm and upload the image). Stretch goal: which of the four European countries exhibited the most significant increase in total gross domestic product during the previous 5-year period (to 2007)?
I'm going to call the new column *gdp* since we are multiplying gdp per capita to the population. To create this column:
```
i = 0
gdp = []
for pop in df['pop']:
    a = (pop * (df['gdpPercap'].iloc[i]))
    gdp.append(a)
    i += 1
df['gdp'] = gdp
```
Then, to subset to follow the criteria mentioned then sort: 
```
countries = df['country'].isin(['Italy', 'Spain', 'France', 'Germany'])
years = df['year'] == 2007
criteria = countries & years
newdf = df[criteria]
newdf = newdf.sort_values(by=['gdp'], ascending = False)
```
![](project1_subsetdf.JPG)
This is the result. 

## You have been introduced to four logical operators thus far: &, ==, | and ^. Describe each one including its purpose and function. Provide an example of how each might be used in the context of programming.
&: bitwise AND operator. The overlap (intersection in venn diagram) of the values being compared.
    ```
    True & False
    True & True
    ```
    The first operation returns False, since True and False are two different values with no overlap
    The second operation returns True, since both values are exactly the same and have overlap
==: compares values of two objects. If they are equivalent, the operation returns a boolean value True
    ```
    (1+1) == 2
    ```
    Returns True since 2 equals 2
|: bitwise OR operator. Union of arguments/values being compared
    ```
    ("cat" != "dog") | (2 > 1)
    ```
    Returns True since both the arguments are equal. If at least one of the arguments above are to be true, the operation will         return True.
^: bitwise XOR (exclusive OR) operator. Values exclusive/distinct to each argument
    ```
    ("cat" != "dog") ^ (2 > 1)
    ```
    Returns False since there are no exclusive parts in each argument as they are equivalent. 

## Describe the difference between .loc and .iloc. Provide an example of how to extract a series of consecutive observations from a data frame. Stretch goal: provide an example of how to extract all observations from a series of consecutive columns.
.loc indexes using a label, in that you have top specify the names of the rows or columns while .iloc indexes using an integer value. To illustrate this:
```
newdf.iloc[0]
newdf.loc[575]
```
The name of the row with values from Germany is 575 (integer), and the index value for that is 1. 

## Describe how an api works. Provide an example of how to construct a request to a remote server in order to pull data, write it to a local file and then import it to your current work session.
API stands for Application Programming Interface. It involves accessing a remote computer to install packages into the local workspace. 
```
import requests
url = 'https://url'
r = requests.get(url)
filename = 'data_folder'
with open(file_name, 'w') as f:
    f.write(r.content)
df = pd.read_csv(name_of_file)
```
This will take in the data from the API in the url, write it onto a local file and read it into the workspace.

## Describe the apply() function from the pandas library. What is its purpose? Using apply) to various class objects is an alternative (potentially preferable approach) to writing what other type of command? Why do you think apply() could be a preferred approach?
apply() allows you to use lamda functions. It offers a shorter and more convenient way of iterating your data instead of having to write out loops which can take longer time and longer lines of code. They are usually used for functions that are only going to be used once and not have to be called again. 

## Also describe an alternative approach to filtering the number of columns in a data frame. Instead of using .iloc, what other approach might be used to select, filter and assign a subset number of variables to a new data frame?
There are many ways you can subset data other than using the `.iloc` function. `df.filter` can subset rows/columns by the specified index. Calling columns directly can also achieve the same goal, simply executing `df['index']`.



















