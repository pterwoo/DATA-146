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
























