## **Data Question 1: An Exploration of UN data**

### Guided Practice:
1. Create a folder called `data` in your local `Data Question 1` repository.

2.	Download two CSV files and place them in this folder:
    
    a.	Gross Domestic Product (GDP) per capita: http://data.un.org/Data.aspx?d=WDI&f=Indicator_Code%3aNY.GDP.PCAP.PP.KD  
    **DO NOT APPLY ANY FILTERS**
     - rename the file to gdp_per_capita.csv
     - open it with a text editor (not excel) and take a look
    
    b.	Percentage of Individuals using the Internet: http://data.un.org/Data.aspx?d=ITU&f=ind1Code%3aI99H  
    **DO NOT APPLY ANY FILTERS**
    - rename the file to internet_use.csv
    - open it with a text editor (not excel) and take a look

3. Create a Jupyter Notebook and name it `UN_Data_Exploration`.
 - _*You are likely to get errors along the way. When you do, read the errors to try to understand what is happening and how to correct it.*_
  - Use markdown cells to record your answers to any questions asked in this exercise. On the menu bar, you can toggle the cell type from 'Code' to 'Markdown'. [Here](https://www.markdownguide.org/cheat-sheet/) is a link to a cheat sheet showing the basics of styling text using Markdown.

4.	In the first cell of your notebook, import the required packages with their customary aliases as follows:

    `import pandas as pd` 
    
    `import numpy as np` 
    
    `import matplotlib.pyplot as plt` 
    
    `import seaborn as sns`
    
    `import scipy.stats as stats`
    
    `import statsmodels.api as sm`
    
    Keep all imports in this cell at the top of your notebook.
    
5.	At the bottom of your imports cell, use the `%matplotlib inline` magic command so that your plots show in the notebook _without_ having to call `plt.show()` every time.

6.	Using the pandas `read_csv()` function, read the GDP dataset into your notebook as a DataFrame called `gdp_df`. 
* Take a look at the first 10 rows. 
* Look at the last 5 rows. Do you see a problem?
* Redo the read_csv() call to correct this issue - **do not** modify the original csv file.

7. How many rows and columns does gdp_df have? What are the data types of its columns?

8. Drop the 'Value Footnotes' column, and rename the remaining columns to ‘Country’, ‘Year’, and ‘GDP_Per_Capita’.

9. Read in continents.csv into a new dataframe called `continents`. We will be using this dataframe to add a new column to our dataset. However, we must first do a little preparation of the country names in `gdp_df` so that we can merge the two correctly:
* Change "CÃ´te d'Ivoire" to "Ivory Coast"
* Change "CuraÃ§ao" to "Curaçao"
* Change "SÃ£o TomÃ© and Principe" to "Sao Tome and Principe"
* Change "Sint Maarten (Dutch part)" to "Sint Maarten"

9. Merge gdp_df and continents. Keep only the countries that appear in both data frames. Save the result back to gdp_df. 

10. Continent is currently stored as an "object" type. Since there are only five possible values for continent, we can convert it to categorical to save some memory usage. Do the following: 
    * Use `.info()` on gdp_df. Note the memory usage. 
    * By chaning type to categorical, we can not only save on memory usage, but can save on CPU time. To see this, we will use the `%%time` cell magic. In a new cell, run the following commands:  
    `%%time`    
    `gdp_df.groupby('Continent').GDP_Per_Capita.mean()`  
    This will return the average GDP_Per_Capita by continent, across all years and will measure how long it took to run.
    * Change the type of the Continent column to 'category'. 
    * Run `.info()` again and note the drop in memory usage.
    * Redo the aggregation about and note how the amount of CPU time dropped.

11. Determine the number of countries per continent. Create a bar chart showing this.

12. How many countries are represented in this dataset? What range of years are represented?

13. Create a new dataframe by subsetting `gdp_df` to just the year 2014. Call this new dataframe `gdp_2014`.

14. Use `.describe()` to find the summary statistics for GDP per capita in 2014. 

15. Which country had the highest GDP per capita in 2014? Which had the lowest? Find the top 5 counties by GDP per capita in 2014.

16. Add a column to your 2014 dataframe called 'GDP_Group'. In this column, assign each country to one of three categories: "Low" if the country is in the first quartile of GDP Per Capita, "Medium" if it is between the 25th and 75th percentile, and "High" if it is above the 75th percentile. How do the continents differ in terms of numbers of countries in each group?

15. Create a histogram of GDP Per Capita numbers for 2014 (you may wish to adjust the number of bins for your histogram). What can you say about the distribution of GDP per capita figures in 2014? 

17. Using the scipy function, find the skewness of the GDP per Capita values for 2014. You may not be familiar with this particular statistic, so if you're not, do a little research. Does the value you got make sense considering the histogram you plotted above?

18. Creat a seaborn boxplot showing GDP per capita in 2014 split out by continent. What do you notice?

19. Pivot the data (using the pandas `.pivot()` method) so that we can calculate % change in GDP Per Capita from 1990 to 2017 - drop any countries that are missing GDP numbers for at least one of these two years.

20. What percentage of countries or areas experienced a positive % change in GDP per capita? What percentage experienced a negative % change?

21. Which country had the highest % change in GDP per capita? Create a line plot showing this country's GDP per capita from 1990 to 2017.

22. Create another showing the country with the second highest % change in GDP. How do the trends in these countries compare?

<!-- 23. Do the same for the country with the lowest % change in GDP. -->

24. Read in internet_use.csv into a DataFrame called `internet_df`. You will most likely get an error message when doing this - figure out what is going wrong and fix it. Take a look at the first and last five rows and make any corrections to your `read_csv()` call to fix this. Again, **do not** modify the original datasets. 

25. How many rows and columns does this new dataset have? What are the types of its columns?

26.	Change the columns for the Internet Users data frame to ‘Country’, ‘Year’, and ‘Internet_Users_Pct’.

27.	Merge the two DataFrames to one. Keep only countries and years that appear in both tables. Call the new DataFrame `gdp_and_internet_use`.

28.	Look at the first five rows of your new data frame to confirm it merged correctly. Also, check the last five rows to make sure the data is clean and as expected.

29. What is the mean internet users percentage in 2014? How many countries have at least 90% internet users in 2014?

30. Find the countries that had the top 5 largest GDP per capita figures for 2014. Create a seaborn FacetGrid showing the change in internet user percentage over time for these five countries. What trends do you notice?

31. Create a scatter plot of Internet Use vs GDP per Capita for the year 2014.

32. Find the correlation between GDP per Capita and Internet Use for the year 2014. What is the meaning of this number?

33. Using the statsmodels library, create an ordinary linear regression model with independent variable GDP per capita and dependent variable internet users percentage. Be sure to include an intercept term. Print the model summary. What $R^2$ value do you get for this model? What is the meaning of this number?

34. Add a column to your dataset and calculate the logarithm of GDP per capita. Find the correlation between the log of GDP per capita and internet users percentage. Run an ordinary linear regression with response variable internet users and explanatory variable the log of the GDP per capita, and view the model summary. What is the meaning of the coefficients you get? Which of the two models that you created appears to do a better job?

35. Filter the original dataset down to just the United States for all available years. Calculate correlation between internet use and gdp per capita. Is this meaningful or useful?



<!--
16.	Subset the combined data frame to keep only the data for 2004, 2009, and 2014. Check that this happened correctly.
17.	Create three new data frames, one for 2004, one for 2009, and one for 2014. Give them meaningful names that aren't too long.
18.	Which country had the highest percent of internet users in 2014? What was the percentage? (Try typing the first 3 letters of your DataFrame name and hitting the tab for auto-complete options).
19.	Which country had the lowest percent of internet users in 2014? What was the percentage?
20.	Repeat for 2004 and 2009.
21.	Which country had the highest gdp per capita in 2014? What was the gdp per capita?
22.	Which country had the lowest gdp per capita in 2014? What was the gdp per capita?
23.	Create some scatterplots:  
    a.  2004 Percent Using the Internet vs gdp per capita  
    b.	 2009 Percent Using the Internet vs gdp per capita  
    c.	 2014 Percent Using the Internet vs gdp per capita  
24.	Are there differences across years? What do the plots tell you about any relationship between these two variables? Enter your observations as a markdown cell.
25.	Look at the distribution of gdp per capita values for 2014. Is it unimodal?
26.	Look at the distribution of Internet Use for 2014. Is it unimodal?
27.	What are the top 5 countries in terms of internet use in 2014?
28.	Create a data frame called top_5_internet from the combined data frame that has all three years for these 5 countries. You should have 15 rows. Check that this is true.
29.	Create a seaborn FacetGrid to show the internet usage trend over time for these 5 countries. Which country had the greatest growth between 2004 andd 2014? If you have time, try to figure out how to fix the plotting issue with Bermuda.
30.	Repeat the steps above to look at the trend for 5 countries with the lowest 2014 internet usage. WHich country has consistently had the least internet use?
31.	Get the top 5 countries for 2014 in terms of GDP per capita; create a dataframe to look at 10-year trends in gdp per capita. Use a seaborn facet grid for this.
32. Repeat this one more time to look at 10-year trend for the bottom 5 countries for 2014 in terms of GDP per capita.
33.	Is there anything surprising or unusual in any of these plots? Searching on the internet, can you find any possible explanations for unusual findings?


### In class practice 2:
1.	Import stats from scipy:

     `from scipy import stats`

2.	Print the docstring for stats:

     `print(stats.__doc__)`

    Try shift + tab + tab to see the documentation too!

3.	Create a set of 500 randomly generated numbers called iq_scores with a mean = 100 and standard deviation = 15.
4.	Using the example at the bottom of this webpage as a guide (https://docs.scipy.org/doc/numpy-1.13.0/reference/generated/numpy.random.normal.html), plot the distribution of your iq_scores.  Does it look normally distributed?
5. Create a boxplot of these iq_scores -->

### Solo Exploration and Presentation:
1. Choose and download another data set from the UN data (http://data.un.org/Explorer.aspx) to merge with your data and explore.
1. Prepare a short (< 5 minute) presentation of your findings. Report any interesting correlations you find. Include visualizations and consider adding interactivity with `ipywidgets`. This presentation can be done either in a Jupyter Notebook or using another presentation software, such as PowerPoint. (Check out Jupyter Slides if you have time. This allows you to turn your jupyter notebook into a slideshow: https://medium.com/learning-machine-learning/present-your-data-science-projects-with-jupyter-slides-75f20735eb0f)
2.    Look through the bokeh gallery (https://bokeh.pydata.org/en/latest/docs/gallery.html#gallery) and if time allows create a bokeh visualization using the UN data.
