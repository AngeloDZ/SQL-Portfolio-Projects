# IMDB Top 250 SQL Analysis

## 1 Overview
This project explores the 250 top rated IMDB movies of all time using some basic SQL queries.

This is my first project, mainly for the purpose of being a starter portfolio project and practicing some SQL queries on PostgreSQL, as well as learning how to use Github to display future projects.

## 2 Exploring and Filtering Data (Basic queries)

### 2.1) Viewing all the data.

````sql
SELECT * FROM imdb_top_250_movies
ORDER BY year DESC
````

Very simple. Added `ORDER BY` clause for convenience.

### 2.2) Order all films by rating descending.

````sql
SELECT title, rank, rating FROM imdb_top_250_movies
ORDER BY rating DESC
````
Again, very simple use of the `ORDER BY` clause.

### 2.3) Find movie(s) with the maximum rating.

````sql
SELECT title, rank, rating FROM imdb_top_250_movies
WHERE rating = (SELECT MAX(rating) FROM imdb_top_250_movies)
````
I could have just used a `WHERE` clause to select the row with the number 1 rank, however I wished to use a basic subquery for the purposes of practice. Additionally, if the data contained more than one movie with the highest rating, those additional movies would be displayed too.

### 2.4) Find the top 10 movies of all time.

````sql
SELECT title, rank FROM imdb_top_250_movies
WHERE rank <= 10
ORDER BY rank
````
Two ways of doing this. First is the `WHERE` clause with regards to the rank.

````sql
SELECT title, rating FROM imdb_top_250_movies
ORDER BY rating DESC
LIMIT 10;
````
Second is by ordering by rating, then using `LIMIT`.

### 2.5) Find all the movies with a rating of 9 or higher.

````sql
SELECT title, year, rating FROM imdb_top_250_movies
WHERE rating >= 9
ORDER BY rating DESC
````
Again, simple use of the `WHERE` clause.

## 3 Aggregating and Analyzing Data (Intermediate Queries)

### 3.1) Count the number of films in each decade and find the average rating for each decade (up to 2 decimal points).

````sql
SELECT ROUND(AVG(rating)::numeric, 2) as average_rating,
	   CASE WHEN year >= 1920 AND year < 1930 THEN '1920s'
	   		WHEN year >= 1930 AND year < 1940 THEN '1930s'
			WHEN year >= 1940 AND year < 1950 THEN '1940s'
	   		WHEN year >= 1950 AND year < 1960 THEN '1950s'
	   		WHEN year >= 1960 AND year < 1970 THEN '1960s'
	   		WHEN year >= 1970 AND year < 1980 THEN '1970s'
	   		WHEN year >= 1980 AND year < 1990 THEN '1980s'
	   		WHEN year >= 1990 AND year < 2000 THEN '1990s'
	   		WHEN year >= 2000 AND year < 2010 THEN '2000s'
	   		WHEN year >= 2010 AND year < 2020 THEN '2010s'
	   		WHEN year >= 2020 AND year < 2030 THEN '2020s'
	   		ELSE NULL END AS decade,
	   COUNT(*) AS count
FROM imdb_top_250_movies
GROUP BY decade
ORDER BY decade DESC
````

To divide the data into decades, I chose to use the `CASE` clause, acting on the year column, then grouped by decade.

### 3.2) Find the highest rated movie(s) of each decade and their rating.

````sql
WITH imdb_max AS (
		SELECT MAX(rating) as max_rating,
	   	   	 CASE WHEN year >= 1920 AND year < 1930 THEN '1920s'
                  WHEN year >= 1930 AND year < 1940 THEN '1930s'
                  WHEN year >= 1940 AND year < 1950 THEN '1940s'
                  WHEN year >= 1950 AND year < 1960 THEN '1950s'
                  WHEN year >= 1960 AND year < 1970 THEN '1960s'
                  WHEN year >= 1970 AND year < 1980 THEN '1970s'
                  WHEN year >= 1980 AND year < 1990 THEN '1980s'
                  WHEN year >= 1990 AND year < 2000 THEN '1990s'
                  WHEN year >= 2000 AND year < 2010 THEN '2000s'
                  WHEN year >= 2010 AND year < 2020 THEN '2010s'
                  WHEN year >= 2020 AND year < 2030 THEN '2020s'
			      ELSE NULL END AS decade
		FROM imdb_top_250_movies
		GROUP BY decade
)
SELECT imdb.title,
	   max_rating,
	   decade
FROM imdb_max
INNER JOIN imdb_top_250_movies imdb
	ON imdb.rating = imdb_max.max_rating
	AND CASE WHEN year >= 1920 AND year < 1930 THEN '1920s'
			 WHEN year >= 1930 AND year < 1940 THEN '1930s'
			 WHEN year >= 1940 AND year < 1950 THEN '1940s'
			 WHEN year >= 1950 AND year < 1960 THEN '1950s'
			 WHEN year >= 1960 AND year < 1970 THEN '1960s'
			 WHEN year >= 1970 AND year < 1980 THEN '1970s'
			 WHEN year >= 1980 AND year < 1990 THEN '1980s'
			 WHEN year >= 1990 AND year < 2000 THEN '1990s'
			 WHEN year >= 2000 AND year < 2010 THEN '2000s'
			 WHEN year >= 2010 AND year < 2020 THEN '2010s'
			 WHEN year >= 2020 AND year < 2030 THEN '2020s'
			 ELSE NULL END = imdb_max.decade
ORDER BY decade DESC
````

For this query, I thought I would use some sort of self join. My thought was to first find the highest ratings for each decade, then perform a JOIN on the original table to then match both the ratings and decades to select the corresponding titles.

I first altered the query for 3.1, changing the `AVG` function to a `MAX`, to find the maximum rating for each decade. I then used it as a CTE to perform a join on the original table, and it seemed to do the trick!

## 4 What I learned

This first mini-project helped me learn how to use PostgreSQL and how to present SQL projects on GitHub.  

I practiced basic SQL clauses such as `SELECT`, `WHERE`, and `ORDER BY`, as well as aggregation functions like `AVG` and `MAX`. I also learned to use subqueries and CTEs to perform more advanced queries, including combining aggregated results with the original table using joins. I have also learned that certain functions, in this case `ROUND`, can only take a certain numerical data type as an input, as well as how to convert numerical types into the required type.
