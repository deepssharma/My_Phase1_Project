# Phase1 Project
## Goal of the Project
The goal of the project is to provide three recommendations to Microsoft that will help them decide which kind of movies they should make
## Resources
We were provided with one SQL database and 5 other csv/tsv files. Below I explain first the SQL datatables followed by CSV files
### SQL Databases 
The SQL database consisted of many tables, the most important ones (as per me) are listed in order
* movie_basics 
* movie_ratings
* movie_akas
* persons
* directors
* writers
* principals
* known for
## Analysis details used for SQL database and key points
I joined the data-tables movie_basics, movie_ratings, persons , principals and directors  and made one big dataframe. I removed duplicates and NAN values. My goal was to deduce the genre information, and look at average ratings and votes for different genres. There is no clear demarcation for genres as a given movie can fall into different categories. So I just sliced the dataframes into different genres I just pick up some broad definitions like, Action, comedy, scifi, drama, romance, documentary etc).
For each of these genres, I look at mean average ratings, and mean number as well as total number of votes.
Based on the plot of these three variables my deduction is that
* The average ratings for Documentary (including Biography/history) are marginally higher than other genres (based on the genre classification that I used. It may vary somewhat if we change the definitions of genres) though the mean number of votes that such movie receives are very little. This means that movie are rich in content and are appreciated by a certain section of audience who like movies with substance.
* The anime/drama/scifi/comedy movies have more or less the same average ratings but these movies recieve more votes meaning more audience.
One can split this dataframe into foreign/domestic movies and then look at the above mentioned distributions again and see if there is any difference. I wanted to look at the directors and see if there was any relationship between success and directors, but I havent gotten to that yet

### CSV/TSV files
We were provide with 5 files:
* bom.movie_gross.csv
* tn.movie_budgets.csv
* tmdb.movies.csv
* rt.movie_info.tsv
* rt.reviews.tsv(I converted it into csv as opening tsv file was creating some issue)

## Methodology used for CSV/TSV Files and key points
bom.movie_gross.csv and tn.movie_budgets.csv conaing similar information except that the forst table does not contain production budget info and the second table has more entries. So I decided to use the second table to perform a study about profits. I defined two types of profits: worldwide profit and domestic profit. One of the points I wanted to see was that if same movies performs well in domestic market as well as intenational market. This seems to be more or less correlated as seen the correlation plot of profit_dom vs profit.

I merged tn.movie_budgets.csv with tmdb.movies.csv which contains information about popularity of the movies and vote average. After meging these two dataframes, I checked for duplicates and null values. I also cleaned it by requiring the release dates to be same in both dataframes (I had to first convert the date columns to pandas datatime and select the same format for the two tables). Further I cleaned the merged dataframe to contain only english language movies. I then copied this to a small dataframen with only a few columns ('*movie','profit','profit_dom','popularity','vote_average'*. I then sorted the dataframe in descending order based on total profit and selected first 20 values. In order to plot *'profit','profit_dom' and 'popularity* on the ame plot, I scaled each of them with their respective means. There probably is a better way but for now I am using this!!!
### Key Take-aways.
* The most profitable movie turned out to be *Avatar* followed by *Avengers: Infinity War*. Most of the movies that made to top 20 were Sci-fi/Anime.
* The Avengers series has been the most popular movie (based on popularity index) with Avengers: Infinity War being the most popular! *Why do I feel the dataset in these csv files is mostly dominated by sci-fi movies*

## Rest of two csv files
The rest of two csv files *rt.movie_info.tsv* and *rt.reviews.tsv* contain information that I havent been yet able to use. Both the tables dont contain names of movies, but have ids associated with them. Without the decoding information for ids as well as genre ids, I cant tell much. May be I can use *rt.movie_info.tsv*  to study some features about director and/or genre. 

## What else I am looking at now
I merged the dataframe that I created from SQL database as described above with the *tn.movie_budgets.csv*. This now gives me info about a subset of movies that have profit, genre, popularity and average rating info. I am going to see if I can get some meaningful insight from this. 

## Recommendations
* ***Best Genre***

The plot below shows the average profit as a function of genre and I also plotted average ratings as a function of genre.

![Best Genre](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/genres_profits_ratings.png)
I was curious to see that based on the data that we have which movie was the most profitable. So I made the below plot that shows top 20 most protoable movies.Based on this plot, ***Avatar*** turns out to be most profitable movie followed by Avengers infinity wars. However, Avengers seems to be most popular and has higher vote average. I can think of one reason for this discrepancy. Avatar was released in 2009 and Avengers in 2018. In 2009 I would guess %age of people who were social media savvy was small and so the votes garnered by Avatar are less. Just a wild guess!

Both these and the next couple of movies in order are either sci-fi or action thriller. This plot together with the genre plot above suggest that ***sci-fi/anime/action*** movies are more profitable than other genres!
![Best Movie](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_movie.png)

* ***Best Director***

 The plot below shows the top 10 most profitable directors.  Based on this plot I would suggest ***Russo brothers*** as the most profitable director duo. 
 
![Profitable Director](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_director.png)

* ***Best time of year for movie release***

The plot below shows the average profit for different time periods of an year. ***Summer months between May to July*** seem to be most profitable. This makes sense as that is the time when people are having vacations and enjoying. The second most profitable months seem to be Nov to Jan which are holiday months.
The two different bars represent two dtaframes (one is only using the Box office DB and it has more entries), the other is the merged dataframe between 
Box office DB and IMDB sql database  and it has lesser entries as compared to just Box Office DB. If I could I would like to add more data, but that is something that can be done later in the future

![Profitable Time of Year](https://github.com/deepssharma/My_Phase1_Project/blob/master/figs/most_profitable_time_of_year.png)
