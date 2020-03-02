# Understanding Movies (Show me the movies!)

### Collaborators
Andrew Eckes, Brian Abbe, Jason Peterson, Paula Caudilla


## Project Topic
What is the recipe for a successful movie? This is an age-old question that we are sure most people in the movie industry have asked countless of times. Our project endeavors to answer this question by creating a Machine Learning model to determine the most important features of a movie’s box office success based on relationship between genre, star power of the cast, director and other parameters.


## Data Sets
[Rotten Tomatoes Dataset](https://www.kaggle.com/stefanoleone992/rotten-tomatoes-movies-and-critics-datasets)

[IMDB Top 1000 Actors/Actresses](https://www.imdb.com/list/ls058011111/?sort=list_order,asc&mode=detail&page=1)

[Movielens (Revenue)](https://www.kaggle.com/rounakbanik/the-movies-dataset)

[Consumer Price Index](https://www.minneapolisfed.org/about-us/monetary-policy/inflation-calculator/consumer-price-index-1913-)


## Data Processing 
We have gathered a movie dataset from Rotten Tomatoes that includes a list of movies, genres, directors, actors, release date, runtime, vote count and vote average. Another dataset from Movielens included the movies' revenue, budget and popularity. The relevant columns are joined in one CSV. The Budget and Revenue columns are adjusted for inflation, which was done by scraping the CPI (Consumer Price Index) from the Federal Reserve Bank of Minneapolis and using that to calculate for inflation. The Star Power column came from counting the actors in the cast included in the IMDB Top 1000 List of Actors and Actresses, which was scrapped from the IMDB website as well.


## Model Selection

#### Linear Models ([Link to Notebook](https://github.com/brian1581/final-project/blob/master/Jupyter_notebooks/ridge_regression_scaled.ipynb))

To predict a movie's potential box office revenue (the widely used metric of success), we must determine which features have an important positive effect on the target. Outliers were removed from the dataframe for movies where box office and revenue were greater than three standard deviations above the mean.  Removing these outlier movies increased training and test scores roughly 10%. Models that penalized certiain coeficient values to create better fit were tried (Ridge, Lasso, ElasticNet), but our highest test scores were derived from a simple linear model (ordinary least squares regression).

Using the OLS model, size of budget, genre, run time, and Starpower seem to be the important positive precursors to box office success. 
![Coefficient](https://github.com/brian1581/final-project/blob/master/Output/images/linear_reg_coefs.png)
![Residual Plot](https://github.com/brian1581/final-project/blob/master/Output/images/linear_reg_residuals.png)

Training score = 0.50

Testing score = 0.59

Interestingly, it appears that the genres "Drama" and "SciFi" have some of the most negative effects on revenue. I also would have expected the Action and Adventure genre to have a more positive relationship to revenue given the popularity of modern Superhero films.









