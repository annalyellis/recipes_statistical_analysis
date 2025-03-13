# Statistical Analysis of Recipes
An Introduction To the Dataset:

This dataset contains a collectin of recipes from Food.com, originally gathered and used in a research paper on recommender systems. It consists of two primary components: recipes and interactions. The recipes dataset includes details such as ingredients, preparation time, and nutrition information, while the interactions dataset provides a record of reviews and ratings for the recipes. Due to the large quantity of data, these data are a subset of the original dataset, focusing on recipes and reviews posted since 2008. By merging the recipes and interactions datasets, one can analyze the popularity of recipes and identify trends in recipe charactersitics. The data provides valuable insightinto user preferences, rating behaviours, and recipe features, making it a useful resource to explore recipe trends.

Information About the Dataset:
Number of rows in the recipes dataset: 83782
Number of rows in the ratings dataset: 731927
Number of rows in the left merged recipes and interactions: 234429

Relevant Columns:
'minutes' - minutes to prepare recipe
'n_steps' - number of steps in recipe is useful as it could be indicative of how complex a recipe is which could lead to more time creating it
'nutrition' - Nutrition information in the form [calories (#), 
total fat (PDV), sugar (PDV), sodium (PDV), protein (PDV), saturated fat 
(PDV), carbohydrates (PDV)]; PDV stands for “percentage of daily value”

The nutrition column contains lots of valuable information, for example I have extracted the protein (PDV) from the nutrition column and created a protein
column

One of the most relevant things to people when they choose a recipe to create is the amount of time it will take. Personally, if a recipe is going to take a lot of time I simply will not make it and choose something else. I also find it difficult to consume enough protein sometimes, as I have noticied that it often takes longer to make meals that have large quantities of protein in them. This begs the question, what is the relationship between the protein (as a percentage of daily value) a recipe has, and the cooking time of the recipe?
