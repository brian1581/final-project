# Understanding Movies (Show me the movies!)
[Link to PowerPoint Presentation](https://1drv.ms/p/s!AvE7ZETSDzAGhr0IAdU7ePcQ9RYBdQ?e=340f1t)

### Collaborators
Andrew Eckes, Brian Abbe, Jason Peterson, Paula Caudilla


## Project Topic
What is the recipe for a successful movie? This is an age-old question that we are sure most people in the movie industry have asked countless of times. Our project endeavors to answer this question by creating a Machine Learning model to determine the most important features of a movie’s box office success based on relationship between genre, star power of the cast,  Vote Average and other parameters.


## Data Sets
[Rotten Tomatoes Dataset](https://www.kaggle.com/stefanoleone992/rotten-tomatoes-movies-and-critics-datasets)

[IMDB Top 1000 Actors/Actresses](https://www.imdb.com/list/ls058011111/?sort=list_order,asc&mode=detail&page=1)

[Movielens (Revenue)](https://www.kaggle.com/rounakbanik/the-movies-dataset)

[Consumer Price Index](https://www.minneapolisfed.org/about-us/monetary-policy/inflation-calculator/consumer-price-index-1913-)


## Data Processing 
We have gathered a movie dataset from Rotten Tomatoes that includes a list of movies, genres, directors, actors, release date, runtime, vote count and vote average. Another dataset from Movielens included the movies' revenue, budget and popularity. The relevant columns are cleaned and joined into one CSV using Python Pandas. The Budget and Revenue columns are adjusted for inflation, which was done by scraping the CPI (Consumer Price Index) from the Federal Reserve Bank of Minneapolis and using that to calculate for inflation. The Star Power column came from counting the actors in the cast included in the IMDB Top 1000 List of Actors and Actresses, which was scraped from the IMDB website as well. 

During model selection, data are pre-processed by using dummy variables to change categorical information to numerical (specifically the genre column), as well as scaling. Lastly, Python Matplotlib is used to plot the charts showing the vizualization of the results.


## Model Selection and Results

#### Linear Models ([Link to Notebook](https://github.com/brian1581/final-project/blob/master/Jupyter_notebooks/ridge_regression_scaled.ipynb))

To predict a movie's potential box office revenue (the widely used metric of success), we must determine which features have an important positive effect on the target. Outliers were removed from the dataframe for movies where box office and revenue were greater than three standard deviations above the mean.  Removing these outlier movies increased training and test scores roughly 10%. Models that penalized / reduced the magnitude of certain coeficient values were tried (Ridge, Lasso, ElasticNet) to create a better fit, but our highest test scores were derived from a simple linear model (ordinary least squares regression).

Using the OLS model, size of budget, genre, run time, and Starpower seem to be the important positive precursors to box office success. 
<br><br><img src="https://github.com/brian1581/final-project/blob/master/Output/images/linear_reg_coefs.png" width="400"><br>
<img src="https://github.com/brian1581/final-project/blob/master/Output/images/linear_reg_residuals.png" width="300">
<br><br>
Training score = 0.50<br>
Testing score = 0.59
<br><br>
The residual plot above does not show a random distribution (more funnel shaped) indicating possible dependence between some X feature(s) and the y target.

Interestingly, it appears that the genres "Drama" and "SciFi" have some of the most negative effects on revenue. We also would have expected the Action and Adventure genre to have a more positive relationship to revenue given the popularity of modern Superhero films.

#### Deep Neural Network evaluation ([Link to Notebook]( https://github.com/brian1581/final-project/blob/master/Jupyter_notebooks/tomato_model_deep_2_reduce.ipynb))

Results were mixed as the accuracy would change from a high +0.56 to a low of +0.13
<br><br>
Example output:
Normal Neural Network - Loss: 355.50811584013746, Accuracy: 0.1315789520740509
<br><br>
Experimentation:
Changing the number of nodes in the hidden layers had no effect. Running more epochs did not bring the network to a solution. Changing the sensitivity did not have any appreciable effect.

There was a linear relationship between the revenue and budget, based on the partial dependency of the features of the decision tree and deep neural networks.  The popularity data showed some relationship to the revenue, but this mostly related to older movies (1950s-1970s).  The newer the movie, the less relevant.  This may be because older movies that have stood the test of time will have a large, consistent following.

There is also a relationship that is mostly linear between vote count and revenue.  This makes sense, as the movies that make the most money should indicate mass popularity.  It may be worthwhile to remodel based on vote count as target.


#### Random Forest evaluation ([Link to Notebook](https://github.com/brian1581/final-project/blob/master/Jupyter_notebooks/star_forest.ipynb))

We attempted a number of variables as the target from popularity to vote_average to budget, but each yielded model scores below .10. We used binning to find the best results in our models. Star Power and Revenue offered the most promising model scores of .85. We did review out of bag results for further review, but those results for each target were .80 to .84. 

Changing the number of estimaters, bins and the random state did cause the results to fluctuate until we found the best combination.

Changing the tree depths did not have any impact

The Star Power was heavily concentrated to zero or one, 96% of all samples

Revenue scoring was scored highest relative to vote_count, which you may expect given more votes is likely due to more paying viewers. Runtime had a surprisingly high score relative to the Star Power count. This definitely requires further examination into that relationship.

The fact we found the "None" genre scored highest relative to the Star Power target is hard to decipher. Without having a better idea of a more specific breakdown, it could simply be just noise?


## Conclusion
* None of our models did a great job of explaining box office revenues with this dataset, despite joining additional features & accommodating for inflation

* Incremental features like advertising budget, season in year, economic condition factor, director starpower and others could be added to enhance the model potential predictability

* We would recommend additional information such as advertising budgets or current events/trends to also build a more accurate model


## Additional Item for Future Consideration
The Animation genre would probably have to be in a separate bucket given the runtimes are typically shorter and other variables such as critic and vote counts might be skewed.







