# Phase1 Project
## Goal of the Project
The goal of the project is to provide three recommendations to Microsoft that will help them decide which kind of movies they should invest/produce.
## Resources and description of files
We were provided with various files from different sources: ***IMDB, Rotton Tomatoes, BOX office Mojo, The Numbers, and TheMovieDB***.
* The IMDB is an SQL database and had different tables connected by movie_id, and/or person id. These tables have lot of information like average ratings, directors, actors, etc etc. 
* The Box office Mojo and The Numbers files contain the production budget and box office earnings. The Number files supersedes the Box Office Mojo files since it contained more that and also the production budget info that is needed to calculate profits. So my analysis is based on ***The Numbers*** file.
* The rotton tomatoes and TheMovieDB contained info about ratings, votes, reviews etc etc. However, they used keywords for genres,and movie names and in order to properly decode them I need to probably download more data or use API from their websites. I spent an extensive amount of time to get some results from these files, but without further inormation, and merging the dataframes using *release dates* or *other parameters* made it cumbersome, as well as, generated wrong information. So the results presented below are mostly derived from ***IMDB and The Numbers*** files. The jupyter file contains all the different things that I tried wiith these datafiles.


## Some analysis details
I joined the data-tables movie_basics, movie_ratings, persons , principals and directors  and made one big dataframe. I removed duplicates and NAN values. 
I had to merge some entries where you have multiple directors for the same movie. 
My goal was to deduce the genre information, and look at average ratings and votes for those genres. First of all,  There is no clear demarcation for genres as a given movie can fall into different categories. So I sliced the dataframes into different genres based on my definitions like, Action, comedy, scifi, drama, romance, documentary etc).
For each of these genres, I look at mean average ratings, and mean number of votes as well as total number of votes. 
Based on the plot of these three variables my deduction is that
* The average ratings for Documentary (including Biography/history) are marginally higher than other genres (based on the genre classification that I used. It may vary somewhat if we change the definitions of genres) though the mean number and total number of votes that such movie receives are very little. This means that movie are rich in content and are appreciated by a certain section of audience who like movies with substance. 
* The anime/drama/scifi/comedy movies have more or less the same average ratings but these movies recieve more votes which translated to larger audience.
One can split this dataframe into foreign/domestic movies and then look at the above mentioned distributions again and see if there is any difference.

* ***I abandoned the strategy to use average ratings as my classifier for finding out the movie recommendations as it didnt seem to provide a clear difference ***

#### The Numbers file

This contained the information that allowed me to calculate profits and merging this with IMDB files allowed to have genres, average ratings and directors information as well.

## Data cleaning
Some of the general things that I did everytime I have a datafile/table
* Look for duplicate entries
* Look for NAN entries
* Look for release dates
* Look for movie ids
* If there are multiple entries for a given movie, look for the reason.
* One of the reason e.g. is to have multiple directors for a given movie. In this case I merged the rows and director column was joined to have all the names

## Recommendations
* ***Best Genre***

The plot below shows the average profit as a function of genre and I also plotted average ratings as a function of genre.

![Best Genre](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/genres_profits_ratings.png)
I was curious to see that based on the data that we have which movie was the most profitable. So I made the below plot that shows top 20 most protoable movies.Based on this plot, ***Avatar*** turns out to be most profitable movie followed by Avengers infinity wars. However, Avengers seems to be most popular and has higher vote average. I can think of one reason for this discrepancy. Avatar was released in 2009 and Avengers in 2018. In 2009 I would guess %age of people who were social media savvy was small and so the votes garnered by Avatar are less. Just a wild guess!

Both these movies and the next couple of movies in order are either sci-fi or action thriller. The values on y-axis are normalized values by mean for the given variable (i.e. profit, popualrity, vote average). What I mean by this is as follows: e.g. profit for each movie was divided by average profit dervied by all the movies, and likewise for popularity, vote average etc. I did this so that I can overlay all three variables on the same plot. Afterwards I relaised that I could use the normalize function from numpy.

This plot together with the genre plot above suggest that ***sci-fi/anime/action*** movies are more profitable than other genres!
![Best Movie](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_movie.png)

* ***Best Director***

 The plot below shows the top 10 most profitable directors.  Based on this plot I would suggest ***Russo brothers*** as the most profitable director duo. 
 
![Profitable Director](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_director.png)

* ***Best time of year for movie release***

The plot below shows the average profit for different time periods of an year. ***Summer months between May to July*** seem to be most profitable. This makes sense as that is the time when people are having vacations and enjoying. The second most profitable months seem to be Nov to Jan which are holiday months.
The two different bars represent two dataframes (one is only using the Box office DB and it has more entries), the other is the merged dataframe between 
Box office DB and IMDB sql database  and it has lesser entries as compared to just Box Office DB. If I could I would like to add more data, but that is something that can be done later in the future

![Profitable Time of Year](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_time_of_year.png)

### Conclusions:
Based on my analysis, I have found that **sci-fi/animation** movies are most profitable and popular movies. This can be seen from the plots that show average profit as a function of profit, and also the plot showing the most profitable movie, **Avatar followed by Averngers Infinity wars**, both of which belong to sci-fi and/pr anime category. **Russo brothers**, on average, are most profitable director duo, and movies released during summer months, **May to July** are on average are more pofitable.

So I would suggest based on these findings to make a **sci-fi/anime movie with Russo brothers and release it during the months from May to July** to maximize the chances of profitabilty 

### Future work
* First of all I would like to get my hands on more data. The websites listed certainly have lot more data. I would use API or if possible direct download the data.
* Figure out the keys for Rotton tomatoes data and repeat the analysis to see if I get same results as above! This is important since a lot of times results from large dataset are not what you get from a small data sample!
* Look more at the average ratings and or popularity  and profits and see if they are correlated !
* Check if the foreign market behaves differently than the US market.
* Also look at the  actors and writes as a fuction of profits and ratings
* And probably some more
