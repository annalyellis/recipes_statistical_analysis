# Statistical Analysis of Recipes
## Introduction:

This dataset contains a collectin of recipes from Food.com, originally gathered and used in a research paper on recommender systems. It consists of two primary components: recipes and interactions. The recipes dataset includes details such as ingredients, preparation time, and nutrition information, while the interactions dataset provides a record of reviews and ratings for the recipes. Due to the large quantity of data, these data are a subset of the original dataset, focusing on recipes and reviews posted since 2008. By merging the recipes and interactions datasets, one can analyze the popularity of recipes and identify trends in recipe charactersitics. The data provides valuable insightinto user preferences, rating behaviours, and recipe features, making it a useful resource to explore recipe trends.

### Information About the Dataset:
- Number of rows in the recipes dataset: 83782
- Number of rows in the ratings dataset: 731927
- Number of rows in the left merged recipes and interactions: 234429

### Relevant Columns:
- 'minutes' - minutes to prepare recipe
- 'n_steps' - number of steps in recipe is useful as it could be indicative of how complex a recipe is which could lead to more time creating it
- 'nutrition' - Nutrition information in the form [calories (#), 
total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat 
(PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”

**Note:** The nutrition column contains lots of valuable information, for example I have extracted the protein (PDV) from the nutrition column and created a protein
column

One of the most relevant things to people when they choose a recipe to create is the amount of time it will take. Personally, if a recipe is going to take a lot of time I simply will not make it and choose something else. I also find it difficult to consume enough protein sometimes, as I have noticied that it often takes longer to make meals that have large quantities of protein in them. This begs the question, what is the relationship between the protein (as a percentage of daily value) a recipe has, and the cooking time of the recipe?

## Data Cleaning and Exploratory Analysis
### Data Cleaning
The first step I took in cleaning the dataset was creating a 'protein' column in my dataset, as this would become relevant for answering my question on the relationship between protein and time it takes to prepare a recipe. In order to do so, I first turned all of the values in the nutrition column into lists and turned the ints into floats in the lists. I then created a protein column by getting the fourth element of each list in the nutrition column. 

At this point, I realized there were a few peculiar outliers - for example a recipe titled "How To Preserve a Husband" that was said to take around 1 million minutes. This sort of recipe is irrelevant for my analysis, so I filtered the recipes to include only those with a cooking time under 10 hours, as this is where the vast majority of the recipes are. The number of outliers that did not meet this criteria was about 671, about 0.0126% of the total amount of recipes. I then also realized that there were some irregularities in the protein column (a hot cocoa mix recipe with a protein PDV of 4356% does not make much sense), so I filtered the recipes to include only with under 400% PDV protein. The number of outliers which did not meet this critereia was 19, aobut 0.00106% of the total amount of recipes.

|   ID   | Name                           | Minutes | Steps | Ingredients                                                                                   | Num Ingredients | Avg Rating | Protein |
|--------|--------------------------------|---------|-------|-------------------------------------------------------------------------------------------------|----------------|------------|---------|
| 111    | 1 brownies in the world best ever | 40      | 10    | ['bittersweet chocolate', 'unsalted butter', '...']                                      | 9                | 4.0        | 3.0     |
| 115    | 1 in canada chocolate chip cookies | 45      | 12    | ['white sugar', 'brown sugar', 'salt', 'margar...']                                     | 11              | 5.0        | 13.0    |
| 118    | 412 broccoli casserole                | 40      | 6      | ['frozen broccoli cuts', 'cream of chicken sou...']                                 | 9                | 5.0        | 22.0    |
| 119    | millionaire pound cake                | 120    | 7      | ['butter', 'sugar', 'eggs', 'all-purpose flour...']                                  | 7                | 5.0        | 20.0    |
| 125    | 2000 meatloaf                                | 90      | 17    | ['meatloaf mixture', 'unsmoked bacon', 'goat c...']                               | 13              | 5.0        | 29.0    |


### Univariate Analysis
<iframe
  src="assets/cooking_time_dist.html"
  width="800"
  height="600"
  frameborder="0"
></iframe>
Cooking times are predominantly relatively short, as shown by the skewed distribution. The most range for a cooking time to be in is 20-39 minutes.

<iframe
  src="assets/protein_dist.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>
The heavily skewed distribution reveals that the vast majority of recipes do not have that much protein. Most commonly, recipes contain less than 10 PDV of protein.


### Bivariate Analysis
<iframe
  src="assets/protein_vs_time.html"
  width="800"
  height="400"
  frameborder="0"
></iframe>
Due to a large amount of data, this plot makes it difficult to see a relationship between protein and cooking time. The least squares line reveals that there is, in fact, a positive relationship.

![Density Plot of Protein PDV vs. Cooking Time](assets/seaborn_plot.png)
This density plot reveals the large amount of data centered around low amounts of protein.

### Interesting Aggregates
Although the scatterplot is somewhat inconclusive, finding the average (mean, median, mode) amount of protein in each time range reveals that protein is strictly increasing as time increases. 

| time_bin  | mean protein | median protein | count protein |
|-----------|--------------|----------------|---------------|
| 0-10 min  | 13.99        | 6.0            | 11043         |
| 11-30 min | 30.00        | 18.0           | 26268         |
| 31-60 min | 34.77        | 22.0           | 25415         |
| 61-120 min| 40.03        | 24.0           | 12328         |
| 120+ min  | 52.26        | 33.0           | 8726          |

# Assessment of Missingness
## Not Missing at Random (NMAR) Analysis
 The columns with null values are 'name', 'description', and 'avg_rating'. It seems that none of them are likely to be NMAR as 'name' is likely MCAR, while 'description' and 'avg_rating' could easily be linked to other columns in the dataset. For example, the average rating on recipes that have less steps or take less time could be higher as people are more likely to complete the recipe efficiently and feel satisified with their results. The description on less complex recipes with less steps might be missing as simple recipes may not require a description.

 ## Missingness Dependency


