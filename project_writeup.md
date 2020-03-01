# Understanding Movies (Show me the movies!)

### Collaborators
Andrew Eckes, Brian Abbe, Jason Peterson, Paula Caudilla


## Project Topic
What is the recipe for a successful movie? This is an age-old question that we are sure most people in the movie industry have asked countless of times. Our project endeavors to answer that question by creating a Machine Learning model to figure out how popular, revenue-wise, a movie would be based on relationship between genre, actor, director and other parameters.


## Data Processing 
We have gathered a movie dataset from Rotten Tomatoes that includes a list of movies, genres, directors, actors, release date, runtime, vote count and vote average. Another dataset from Movielens included the movies' revenue, budget and popularity. The relevant columns are joined in one CSV. The Budget and Revenue columns are adjusted for inflation (CPI table was scraped to calculate for inflation), and the Star Power column came from counting the actors in the cast included in the IMDB Top 1000 List of Actors and Actresses.


## Data Sets
[Rotten Tomatoes Dataset](https://www.kaggle.com/stefanoleone992/rotten-tomatoes-movies-and-critics-datasets)

[IMDB Top 1000 Actors/Actresses](https://www.imdb.com/list/ls058011111/?sort=list_order,asc&mode=detail&page=1)

[Movie Revenues](https://www.kaggle.com/rounakbanik/the-movies-dataset)

[Consumer Price Index](https://www.minneapolisfed.org/about-us/monetary-policy/inflation-calculator/consumer-price-index-1913-)


## Project Track & Stack
* Downloaded Rotten Tomatoes and Movielens datasets from Kaggle
* Used Python Pandas and Matplotlib to clean relevant columns and join everything to one CSV 
* Used Tableau for more data visualization
* Created website regarding project and deployed to Github Pages







