# Analysis-of-Ingredients
A count of organic ingredients in common grocery store products using ETL.

# Extracting the Data
The U.S. Department of Agriculture has many datasets related to food, ingredients, and nutrition. The goal was to examine a dataset with all food, so we decided to download the CSVs provided on the USDA website. After viewing each of the files, we downloaded two particular csv files: “branded_food” and “food.” Each csv file contained 260,370 rows of data, which was then converted into a pandas dataframes.

# Transforming the Data
First, the necessary columns were copied for each of the two dataframes, dropping the columns we did not need. Next we wanted to do some work on the branded_food database. We started by separating out each of the ingredients in the column called ‘ingredients.’ With the help of ‘str.split’ (to separate by comma) and ‘melt’ (to transform the separated ingredients from columns into rows) we created a new dataframe. Since each product has a different number of ingredients, we were left with a lot of null values. The null values were dropped and we were left with nearly 3.7 million rows of data!

Meanwhile, we needed to loop through the ingredients to find which ones contained organic items. This was done using by reducing the branded_food csv into two columns: fdc_id and ingredients. Once the new dataframe was built, a regular expression was used to find the occurrences of the word “organic” (re.compile(“\W*(ORGANIC)\W*”). Using the regular expression inside a for loop all instances of organic ingredients were aggregated into two new columns. These new columns can be used later for further analytical insights.

# Loading the Data
The data was then loaded into a SQLite database. A connection to the database was established using Jupyter Notebook. Next, we checked to make sure that the connection was valid. We then did a join on our dataframes, combined_df and ingred_df.
