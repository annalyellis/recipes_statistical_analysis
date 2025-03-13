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

NEED TO INCLUDE HEAD OF RECIPES CLEANED DATAFRAME

## Univariate Analysis
INCLUDE PLOTLY PLOTS AND EXPLANATION - USE DISTRIBUTION OF COOKING TIME AND PROTEIN

## Bivariate Analysis
INCLUDE PLOT OF PROTEIN PDV vs. COOKING TIME and explanation

## Interesting Aggregates
include pivot table and explanation

# Assessment of Missingness


