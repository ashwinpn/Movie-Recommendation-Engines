# The Cold Start Problem

The cold start problem refers to the scenario faced by recommendation systems when there isn't enough information [either due to lack of users, or due to the items being new / the platform being launched just now] for the system to make a decent recommendation action.

Thus, the system cannot draw inference for users or items for which it has not yet gathered sufficient information.

- 1] ITEM CHARACTERISTICS => CONTENT BASED FILTERING. "Find another item similar to a given item".
- 2] USER's SOCIAL ENVIRONMENT / PAST BEHAVIOR => COLLABORATIVE FILTERING. "Find another user similar to a given user. Hypothesis: Similar users will buy similar items."

## Types of problems
### New Community

### New Item

### New User

#  Movie Recommendation

The use case of Movie Recommendations suffers from <ins> popularity bias </ins>. That is, we would have a minority of movies in a dataset which have been viewed / rated / favorited by a lot of people - on the other hand, most of the movies would not have been viewed / rated / favorited by a number of people significant enough for them to be recommended.

## Popularity Bias
A handful of items receive a large number of interaction, while most of the items recieve only a fraction of them.
FEW INERACTIONS => POOR RECOMMENDATIONS.

## Zipf's Law

Zipf's law (/zɪf/, not /tsɪpf/ as in German) is an empirical law formulated using mathematical statistics that refers to the fact that for many types of data studied in the physical and social sciences, the rank-frequency distribution is an inverse relation. The Zipfian distribution is one of a family of related discrete power law probability distributions. It is related to the zeta distribution, but is not identical.

The same relationship occurs in many other rankings of human created systems, such as the ranks of mathematical expressions or ranks of notes in music, and even in uncontrolled environments, such as the population ranks of cities in various countries, corporation sizes, income rankings, ranks of number of people watching the same TV channel, and so on. The appearance of the distribution in rankings of cities by population was first noticed by Felix Auerbach in 1913. Empirically, a data set can be tested to see whether Zipf's law applies by checking the goodness of fit of an empirical distribution to the hypothesized power law distribution with a <ins>Kolmogorov–Smirnov test</ins>.

![](https://github.com/ashwinpn/Movie-Recommendation-Engines/blob/master/resources/zipf.png)

## Information Retrieval (Scraping)

- Using ``` requests ``` and ``` bs4 (BeautifulSoup) ``` for static web pages (and make use of  ``` Selenium ``` for dynamic pages).
- Refer the [Scraper](https://github.com/ashwinpn/Advanced-Python/blob/master/Web%20Scraper.ipynb) for a basic shell/structure of a scraper.

Example results from bs4 processing:
```Javascript
function lockScroll() {
            var lockX = window.scrollX;
            var lockY = window.scrollY;

            function lockIt() {
                window.scrollTo(lockX, lockY);
                return false;
            }

            window.addEventListener("scroll", lockIt, false);
            return {
                stop: function () {
                    window.removeEventListener("scroll", lockIt, false);
                }
            }
        }
        window.addEventListener("load", function () {
            $('#ResultsScrollable').bind("scroll", function () {
                if ($(this).scrollTop() + $(this).innerHeight() >= $(this)[0].scrollHeight) {
                    var locker = lockScroll();
                    var loadBtn = document.getElementById('loadMoreJobs');
                    if (loadBtn) loadBtn.click();
                    locker.stop();
                } 
            });
        });
```

## Problem Statement
This project is divided into two parts: 
* **The Story of Film:** This section aims at narrating the history, trivia and facts behind the world of cinema through the lens of data. Extensive Exploratory Data Analysis is performed on Movie Metadata about Movie Revenues, Casts, Crews, Budgets, etc. through the years. Two predictive models are built to predict movie revenues and movie success. Through these models, we also aim at discovering what features have the most significant impact in determining revenue and success.
* **Movie Recommender Systems:** This part is focused around building various kinds of recommendation engines; namely the Simple Generic Recommender, the Content Based Filter and the User Based Collaborative Filter. The performance of the systems are evaluated in both a qualitative and quantitative manner.

## Approach - Workflow

The problem was divided into several steps:

1. **Data Collection:** Data was collected from the MovieLens website and through a script that queried for data from various TMDB Endpoints.
2. **Data Wrangling:** The datasets were uploaded to a dataframe and explored. Null values were filled in wherever appropriate and polluted values were discarded or wrangled.
3. **EDA:** Extensive data visualisation and summary statistics were used to extract insights and pattern from the various datasets. The history, facts and trivia behind movies were narrated through data.
4. **Machine Learning:** Gradient Boosting Classifer and Regressor were trained on our feature engineered dataset to predict movie success and revenue respectively. Their feature importances were noted to gain insights into what factors influence the revenues of a movie relative to budget.
5. **Recommendation Systems:** Four different recommendation systems were built using various ideas and algorithms such as IMDB's Weighted Rating, Content Based Filtering and Collaborative Filtering.

## Final Results 

A Gradient Boosting Regressor and Classifier were built to predict Film Revenue and Success respectively with a Score of 0.84 and 0.88 respectively.

In addition, four recommendation engines were built based on different ideas and algorithms:

* **Simple Recommender:** This system used overall TMDB Vote Count and Vote Averages to build Top Movies Charts, in general and for a specific genre. The IMDB Weighted Rating System was used to calculate ratings on which the sorting was finally performed.
* **Content Based Recommender:** I built two content based engines; one that took movie overview and taglines as input and the other which took metadata such as cast, crew, genre and keywords to come up with predictions. I also devised a simple filter to give greater preference to movies with more votes and higher ratings.
* **Collaborative Filtering:** I used the powerful Surprise Library to build a collaborative filter based on singular value decomposition (SVD). The RMSE obtained was less than 1 and the engine gave estimated ratings for a given user and movie.
* **Hybrid Engine:** I brought together ideas from content and collaborative filtering to build an engine that gave movie suggestions to a particular user based on the estimated ratings that it had internally calculated for that user.


## Repository Structure

1. **movies_eda.ipynb:** The Jupyter notebook that contains the EDA and narrates the Story of Film.
2. **movies_recommender.ipynb:** The Jupyter notebook containing code for the recommendation engines
3. **scrapers:** The folder containing all the scrapers used to gather data from TMDB.

## Extension - Currently working on:
- Use XGBoost for classification + Visualization using ```Bokeh``` and ```Plotly.JS```.
- Implement basic recommendation models in ``` R ``` and use ``` shiny App ``` for building a web-app.
- Try **Deep collaborative filtering** : The matrix factorization model can be represented as a neural network. Can also try (traditional collaborative filtering models) + (auto-encoders).
- [A Reinforcement Learning Framework for Explainable Recommendation, ICDM 2018](https://ieeexplore.ieee.org/abstract/document/8594883/)
