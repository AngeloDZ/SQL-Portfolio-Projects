# IMDB Top 250 SQL Analysis

## 1) Overview
This project explores the 250 top rated IMDB movies of all time using some basic SQL queries.

## 2) Exploring and Filtering Data (Basic queries)

### 2.1) Select all the data.

````sql
SELECT * FROM imdb_top_250_movies
ORDER BY year DESC
````

|rank|title                        |year  |rating                                       |duration|imdb_url                              |image_url                                                                                                    |
|----|-----------------------------|------|---------------------------------------------|--------|--------------------------------------|-------------------------------------------------------------------------------------------------------------|
|128 |One Battle After Another     |2025  |8.3 |2h 41m  |https://www.imdb.com/title/tt30144839/|https://m.media-amazon.com/images/M/MV5BMzBkZmQ0NjMtNTZlMy00ZjdlLTg5ODUtYWFlNGM0YzE3MTg0XkEyXkFqcGc@._V1_.jpg|
|172 |Demon Slayer: Kimetsu no Yaiba- The Movie - Infinity Castle|2025 |8.5 |2h 35m  |https://www.imdb.com/title/tt32820897/|https://m.media-amazon.com/images/M/MV5BOGQ3YWUzYjEtMTJiYy00ZjQ0LWI0YjktYjhiNGVhNGExYTM3XkEyXkFqcGc@._V1_.jpg|
|220 |Maharaja                     |2024  |8.3 |2h 21m  |https://www.imdb.com/title/tt26548265/|https://m.media-amazon.com/images/M/MV5BOTFlMTIxOGItZTk0Zi00MTk2LWJiM2UtMzlhZWYzNjQ4N2Y3XkEyXkFqcGc@._V1_.jpg|
|58  |Dune: Part Two               |2024  |8.4 |2h 46m  |https://www.imdb.com/title/tt15239678/|https://m.media-amazon.com/images/M/MV5BNTc0YmQxMjEtODI5MC00NjFiLTlkMWUtOGQ5NjFmYWUyZGJhXkEyXkFqcGc@._V1_.jpg|
|180 |The Wild Robot               |2024  |8.2 |1h 42m  |https://www.imdb.com/title/tt29623480/|https://m.media-amazon.com/images/M/MV5BZWNiZjVlZTUtNGUwYi00MjJmLTg2MDctNWEzYTJiMzY1ODc4XkEyXkFqcGc@._V1_.jpg|
|44  |Spider-Man: Across the Spider-Verse|2023  |8.5 |2h 20m  |https://www.imdb.com/title/tt9362722/ |https://m.media-amazon.com/images/M/MV5BNThiZjA3MjItZGY5Ni00ZmJhLWEwN2EtOTBlYTA4Y2E0M2ZmXkEyXkFqcGc@._V1_.jpg|
|122 |Oppenheimer                  |2023  |8.3 |3h 0m   |https://www.imdb.com/title/tt15398776/|https://m.media-amazon.com/images/M/MV5BN2JkMDc5MGQtZjg3YS00NmFiLWIyZmQtZTJmNTM5MjVmYTQ4XkEyXkFqcGc@._V1_.jpg|
|70  |12th Fail                    |2023  |8.7 |2h 27m  |https://www.imdb.com/title/tt23849204/|https://m.media-amazon.com/images/M/MV5BNTE3OTIxZDYtNjA0NC00N2YxLTg1NGQtOTYxNmZkMDkwOWNjXkEyXkFqcGc@._V1_.jpg|
|149 |Top Gun: Maverick            |2022  |8.2 |2h 10m  |https://www.imdb.com/title/tt1745960/ |https://m.media-amazon.com/images/M/MV5BMDBkZDNjMWEtOTdmMi00NmExLTg5MmMtNTFlYTJlNWY5YTdmXkEyXkFqcGc@._V1_.jpg|
|195 |Spider-Man: No Way Home      |2021  |8.2 |2h 28m  |https://www.imdb.com/title/tt10872600/|https://m.media-amazon.com/images/M/MV5BMmFiZGZjMmEtMTA0Ni00MzA2LTljMTYtZGI2MGJmZWYzZTQ2XkEyXkFqcGc@._V1_.jpg|

(Output limited for readability.)

### 2.2) Order all films by rating descending.

````sql
SELECT title, rating FROM imdb_top_250_movies
ORDER BY rating DESC
````

|title                                            |rating|
|-------------------------------------------------|------|
|The Shawshank Redemption                         |9.3   |
|The Godfather                                    |9.2   |
|The Dark Knight                                  |9.1   |
|The Lord of the Rings: The Return of the King    |9     |
|12 Angry Men                                     |9     |
|Schindler's List                                 |9     |
|The Godfather Part II                            |9     |
|The Lord of the Rings: The Fellowship of the Ring|8.9   |
|Forrest Gump                                     |8.8   |
|Fight Club                                       |8.8   |
|Inception                                        |8.8   |
|Pulp Fiction                                     |8.8   |
|The Good, the Bad and the Ugly                   |8.8   |

(Output limited for readability.)

### 2.3) Find movie(s) with the highest rating.

````sql
SELECT title, rank, rating FROM imdb_top_250_movies
WHERE rating = (SELECT MAX(rating) FROM imdb_top_250_movies)
````

|title                                            |rank|rating|
|-------------------------------------------------|----|------|
|The Shawshank Redemption                         |1   |9.3   |

I could have just used a `WHERE` clause to select the row with the number 1 rank, however I wished to use a basic subquery for the purposes of practice. Additionally, if the data contained more than one movie with the highest rating, those additional movies would be displayed too.

### 2.4) Find the top 10 movies of all time.

You can either use the `WHERE` clause with regards to the rank.

````sql
SELECT title, rank FROM imdb_top_250_movies
WHERE rank <= 10
ORDER BY rank
````
|title                                            |rank|
|-------------------------------------------------|----|
|The Shawshank Redemption                         |1   |
|The Godfather                                    |2   |
|The Dark Knight                                  |3   |
|The Godfather Part II                            |4   |
|12 Angry Men                                     |5   |
|The Lord of the Rings: The Return of the King    |6   |
|Schindler's List                                 |7   |
|The Lord of the Rings: The Fellowship of the Ring|8   |
|Pulp Fiction                                     |9   |
|The Good, the Bad and the Ugly                   |10  |

Or simply order by rating, then use `LIMIT`.

````sql
SELECT title, rating FROM imdb_top_250_movies
ORDER BY rating DESC
LIMIT 10;
````

|title                                            |rating|
|-------------------------------------------------|------|
|The Shawshank Redemption                         |9.3   |
|The Godfather                                    |9.2   |
|The Dark Knight                                  |9.1   |
|The Lord of the Rings: The Return of the King    |9     |
|The Godfather Part II                            |9     |
|Schindler's List                                 |9     |
|12 Angry Men                                     |9     |
|The Lord of the Rings: The Fellowship of the Ring|8.9   |
|The Good, the Bad and the Ugly                   |8.8   |
|Pulp Fiction                                     |8.8   |

### 2.5) Find all the movies with a rating of 9 or higher.

````sql
SELECT title, year, rating FROM imdb_top_250_movies
WHERE rating >= 9
ORDER BY rating DESC
````

|title                                            |year|rating|
|-------------------------------------------------|----|------|
|The Shawshank Redemption                         |1994|9.3   |
|The Godfather                                    |1972|9.2   |
|The Dark Knight                                  |2008|9.1   |
|The Godfather Part II                            |1974|9     |
|12 Angry Men                                     |1957|9     |
|The Lord of the Rings: The Return of the King    |2003|9     |
|Schindler's List                                 |1993|9     |

## 3) Aggregating and Analyzing Data (Intermediate Queries)

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

|average_rating                                   |decade|count|
|-------------------------------------------------|------|-----|
|8.35                                             |2020s |14   |
|8.25                                             |2010s |46   |
|8.31                                             |2000s |47   |
|8.41                                             |1990s |39   |
|8.28                                             |1980s |26   |
|8.36                                             |1970s |18   |
|8.34                                             |1960s |16   |
|8.28                                             |1950s |21   |
|8.25                                             |1940s |11   |
|8.28                                             |1930s |6    |
|8.15                                             |1920s |6    |

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

|title                                            |max_rating|decade|
|-------------------------------------------------|----------|------|
|12th Fail                                        |8.7       |2020s |
|Inception                                        |8.8       |2010s |
|The Dark Knight                                  |9.1       |2000s |
|The Shawshank Redemption                         |9.3       |1990s |
|Star Wars: Episode V - The Empire Strikes Back   |8.7       |1980s |
|The Godfather                                    |9.2       |1970s |
|The Good, the Bad and the Ugly                   |8.8       |1960s |
|12 Angry Men                                     |9         |1950s |
|It's a Wonderful Life                            |8.6       |1940s |
|Modern Times                                     |8.5       |1930s |
|City Lights                                      |8.5       |1930s |
|Metropolis                                       |8.3       |1920s |

For this query, I thought I would use some sort of self join. My thought was to first find the highest ratings for each decade, then perform a JOIN on the original table to then match both the ratings and decades to select the corresponding titles.

I first altered the query for 3.1, changing the `AVG` function to a `MAX`, to find the maximum rating for each decade. I then used it as a CTE to perform a join on the original table, and it seemed to do the trick!

## 4) Key Takeaways

From this analysis, we can determine a few insights on the data:

The highest rated film of all time is "The Shawshank Redemption", which was released in 1994 and received a rating of 9.3.

The decade with the highest average rating per film in the IMDB Top 250 list was the 1990s, which scored an average rating of 8.41 amongst 39 films.

Only 7 films have ever been rated a score of 9 or higher.

There seemed to be higher rated films between the 1970s up to the early 2000s, with a slight dip in the 1980s.

## 5) What I learned

This first mini-project helped me learn how to use PostgreSQL and how to present SQL projects on GitHub.  

I practiced basic SQL clauses such as `SELECT`, `WHERE`, and `ORDER BY`, as well as aggregation functions like `AVG` and `MAX`. I also learned to use subqueries and CTEs to perform more advanced queries, including combining aggregated results with the original table using joins. I have also learned that certain functions, in this case `ROUND`, can only take a certain numerical data type as an input, as well as how to convert numerical types into the required type.
