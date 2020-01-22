
# Analysis of Ingredients
A count of organic ingredients in common grocery store products using ETL.

<img width="550" alt="USDAresized" src="https://user-images.githubusercontent.com/46386265/72936736-d4255980-3d35-11ea-8ce4-4722f15801bf.PNG">

# Extracting the Data
The U.S. Department of Agriculture has many datasets related to food, ingredients, and nutrition. The goal of this project was to examine organic ingredients within commonly found foods. We downloaded two particular csv files from the USDA website: “branded_food” and “food.” Each csv file contained 260,370 rows of data.

<img width="700" alt="food_csv" src="https://user-images.githubusercontent.com/46386265/72935846-236a8a80-3d34-11ea-8a86-f7e73fe6e19f.PNG">

# Transforming the Data
First, the csv files were converted to pandas dataframes. Then, the necessary columns were copied for each of the two dataframes, dropping the columns which were not needed. Next we separated out each of the ingredients in the column called ‘ingredients.’ With the help of ‘str.split’ (to separate by comma) and ‘melt’ (to transform the separated ingredients from columns into rows) we created a new dataframe. Since each product has a different number of ingredients, we were left with a lot of null values. The null values were dropped and we were left with nearly 3.7 million rows of data!

Meanwhile, we needed to loop through the ingredients to find which ones contained organic items. This was done by reducing the branded_food csv into two columns: fdc_id and ingredients. Once the new dataframe was built, a regular expression was used to find the occurrences of the word “organic” (re.compile(“\W*(ORGANIC)\W*”). Using the regular expression inside a for loop, all instances of organic ingredients were aggregated into two new columns. 

# Loading the Data
The data was then loaded into a SQLite database. A connection to the database was established using Jupyter Notebook. After making sure the connection was valid, we joined the dataframes - combined_df and ingred_df. These two new SQLite files can now be queryed for further analytical insight.
