
More JOIN operations

1.
List the films where the yr is 1962 [Show id, title]

SELECT id, title
 FROM movie
 WHERE yr=1962
Submit SQLRestore default
result
When was Citizen Kane released?
2.
Give year of 'Citizen Kane'.

SELECT yr FROM movie 
WHERE title = 'Citizen Kane'
Submit SQLRestore default
result
Star Trek movies
3.
List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
Submit SQLRestore default
result
id for actor Glenn Close
4.
What id number does the actor 'Glenn Close' have?

SELECT id 
FROM actor
WHERE name = 'Glenn Close' ;
Submit SQLRestore default
result

id for Casablanca
5.
What is the id of the film 'Casablanca'

SELECT id
FROM movie
WHERE title = 'Casablanca'
Submit SQLRestore default
result
Get to the point

Cast list for Casablanca
6.
Obtain the cast list for 'Casablanca'.

what is a cast list?
The cast list is the names of the actors who were in the movie.

Use movieid=11768, (or whatever value you got from the previous question)

SELECT name 
 FROM movie JOIN casting on movie.id = movieid 
                       JOIN actor ON actor.id = actorid
 WHERE movieid=11768

7.
Obtain the cast list for the film 'Alien'

SELECT name 
 FROM movie JOIN casting on movie.id = movieid 
                       JOIN actor ON actor.id = actorid
 WHERE  title = 'Alien'


8.
List the films in which 'Harrison Ford' has appeared

SELECT title
 FROM movie JOIN casting on movie.id = movieid 
                       JOIN actor ON actor.id = actorid
 WHERE actor.name= 'Harrison Ford'


9.
List the films where 'Harrison Ford' has appeared - but not in the starring role. [Note: the ord field of casting gives the position of the actor. If ord=1 then this actor is in the starring role]

SELECT title
 FROM movie JOIN casting on movie.id = movieid 
                       JOIN actor ON actor.id = actorid
 WHERE actor.name='Harrison Ford' AND casting.ord !=1;



10.
List the films together with the leading star for all 1962 films.

SELECT title, name
 FROM movie JOIN casting on movie.id = movieid 
                       JOIN actor ON actor.id = actorid
 WHERE yr =1962 AND casting.ord = 1;


Busy years for Rock Hudson
11.
Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE name = 'Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2

12.
List the film title and the leading actor for all of the films 'Julie Andrews' played in.

Did you get "Little Miss Marker twice"?
SELECT title, name
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id
WHERE casting.ord = 1  AND movieid IN 
(SELECT movieid
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id WHERE name = 'Julie Andrews')


13.
Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.

SELECT name
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id
WHERE casting.ord = 1 
GROUP BY name
HAVING  COUNT (*) >= 30


14.
List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

SELECT title, COUNT(actorid) 
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(actorid) DESC

15.
List all the people who have worked with 'Art Garfunkel'.

 SELECT  name
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id
WHERE name <> 'Art Garfunkel' AND movieid in (  SELECT  movie.id
 FROM movie JOIN casting ON movie.id=movieid
                      JOIN actor   ON actorid=actor.id
WHERE name = 'Art Garfunkel')
Submit SQLRestore default

