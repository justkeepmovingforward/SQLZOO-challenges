
# SQLZOO solutions

I’ve just completed the sixth course in the Google Data Analytics program and wanted to sharpen my SQL skills before moving on to R.
This repository contains my solutions and notes from working through the SQLZOO challenges.

## Table of Contents

- [1 SELECT basics](#select-basics)
- [2 SELECT from World](#select-from-world)
- [3 SELECT from Nobel](#select-from-nobel)
- [4 SELECT within SELECT](#select-within-select)
- [5 SUM and COUNT](#sum-and-count)
- [6 JOIN](#join)
- [7 More JOIN operations](#more-join-operations)
- [8 Using Null](#using-null)
- [9 Self join](#self-join)

### SELECT basics

#### 1.  Show the population of Germany.

    SELECT population
    FROM world
    WHERE name = 'Germany'

#### 2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

    SELECT name, population 
    FROM world
    WHERE name IN ('Sweden', 'Norway', 'Denmark')

#### 3.  Show the country and the area for countries with an area between 200,000 and 250,000

    SELECT name, area 
    FROM world
    WHERE area BETWEEN 200000 AND 250000


### SELECT from World

#### 1.  Show the name, continent and population of all countries.

    SELECT name, continent, population 
    FROM world

#### 2. Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

    SELECT name FROM world
    WHERE population >= 200000000

#### 3.  Give the name and the per capita GDP for those countries with a population of at least 200 million.

    SELECT name,
    gdp/population AS per_capita_GDP
    FROM world
    WHERE population >= 200000000

#### 4. Show the name and population in millions for the countries of the continent 'South America'. 

    SELECT name, population/1000000 AS mil
    FROM world
    WHERE continent ="South America"

#### 5. Show the name and population for France, Germany, Italy.

    SELECT name, population
    FROM world
    WHERE name IN ("France","Germany","Italy")

#### 6. Show the countries which have a name that includes the word 'United'.

    SELECT name
    FROM world
    WHERE name LIKE "United%"

#### 7. Show the countries that are big by area or big by population. Show name, population and area.

    SELECT name, population, area
    FROM world
    WHERE area > 3000000
    OR population > 250000000

#### 8. Exclusive OR (XOR). Show the countries that are big by area (more than 3 million) or big by population (more than 250 million) but not both.

    SELECT name, population, area
    FROM world
    WHERE area > 3000000
    XOR population > 250000000

#### 9. Show the name and population in millions and the GDP in billions for the countries of the continent 'South America'. 

    SELECT name, ROUND(population/1000000,2), ROUND(gdp/1000000000.0,2)
    FROM world
    WHERE continent="South America"

#### 10. Show the name and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros).

    SELECT name,ROUND(gdp/population,-3) AS per_capita_GDP
    FROM world
    WHERE gdp >=1000000000000

#### 11. Show the name and capital where the name and the capital have the same number of characters.

    SELECT name, capital
    FROM world
    WHERE LENGTH(name)=LENGTH(capital)

#### 12. Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

    SELECT name,capital
    FROM world
    WHERE LEFT(name,1)=LEFT(capital,1)
    AND SUBSTR(name,2)<>SUBSTR(capital,2)

#### 13. Find the country that has all the vowels and no spaces in its name.

    SELECT name
    FROM world
    WHERE name LIKe "%a%" 
    AND name LIKe "%e%" 
    AND name LIKe "%i%"
    AND name LIKe "%o%"
    AND name LIKe "%u%"
    AND name NOT LIKe "% %"

### SELECT from Nobel

#### 1. Display Nobel prizes for 1950.

    SELECT yr, subject, winner
    FROM nobel
    WHERE yr = 1950

#### 2. Show who won the 1962 prize for literature.

    SELECT winner
    FROM nobel
    WHERE yr = 1962
    AND subject = 'literature'

#### 3. Show the year and subject that won 'Albert Einstein' his prize.

    SELECT yr, subject
    FROM nobel
    WHERE winner = "Albert Einstein"

#### 4. Give the name of the 'peace' winners since the year 2000, including 2000.

    SELECT winner
    FROM nobel
    WHERE yr >= 2000
    AND subject="peace"

#### 5. Show all details (yr, subject, winner) of the literature prize winners for 1980 to 1989 inclusive.

    SELECT yr, subject, winner
    FROM nobel
    WHERE yr BETWEEN 1980 AND 1989
    AND subject="literature"

#### 6. Show all details of the presidential winners:
Theodore Roosevelt
Thomas Woodrow Wilson
Jimmy Carter
Barack Obama

    SELECT * FROM nobel
    WHERE winner in ("Theodore Roosevelt",
    "Thomas Woodrow Wilson",
    "Jimmy Carter",
    "Barack Obama")

#### 7. Show the winners with first name John.

    SELECT winner FROM nobel
    WHERE winner LIKE "John%"

#### 8. Show the year, subject, and name of physics winners for 1980 together with the chemistry winners for 1984.

    SELECT yr,subject,winner
    FROM nobel
    WHERE yr="1980"
    AND subject="physics"
    
    UNION
    
    SELECT yr,subject,winner
    FROM nobel
    WHERE yr="1984"
    AND subject="chemistry"

#### 9. Show the year, subject, and name of winners for 1980 excluding chemistry and medicine.

    SELECT yr, subject, winner
    FROM nobel
    WHERE yr=1980
    AND subject <> "chemistry"
    AND subject <> "medicine"

#### 10. Show year, subject, and name of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004).

    SELECT yr,subject,winner
    FROM nobel
    WHERE yr<1910
    AND subject="Medicine"
    
    UNION
    
    SELECT yr,subject,winner
    FROM nobel
    WHERE yr>=2004
    AND subject="Literature"

#### 11. Find all details of the prize won by PETER GRÜNBERG.

    SELECT *
    FROM nobel
    WHERE winner="PETER GRÜNBERG"

#### 12. Find all details of the prize won by EUGENE O'NEILL

    SELECT *
    FROM nobel
    WHERE winner="EUGENE O'NEILL"

#### 13. List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

    SELECT winner,yr,subject
    FROM nobel
    WHERE winner LIKE "Sir%"
    ORDER BY yr DESC, winner 

#### 14. Show the 1984 winners and subject ordered by subject and winner name; but list chemistry and physics last.

    SELECT winner, subject
    FROM nobel
    WHERE yr=1984
    ORDER BY subject IN ('physics','chemistry'),subject

### SELECT within SELECT

#### 1. List each country name where the population is larger than that of 'Russia'.

    SELECT name 
    FROM world
    WHERE population >(SELECT population FROM world WHERE name='Russia')

#### 2. Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

    SELECT name 
    FROM world
    WHERE gdp/population >
         (SELECT gdp/population FROM world
          WHERE name='United Kingdom')
    AND continent="Europe"

#### 3. List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

    SELECT name,continent
    FROM world 
    WHERE continent ="Oceania" OR continent ="South America"
    ORDER BY name

#### 4. Which country has a population that is more than United Kingdom but less than Germany? Show the name and the population.

    SELECT name, population
    FROM world
    WHERE population > (SELECT population FROM world WHERE name="United KIngdom")
    AND population < (SELECT population FROM world WHERE name="Germany")

#### 5. Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

    SELECT name,CONCAT(ROUND(((population/(SELECT population FROM world WHERE name="Germany"))*100),0),"%") AS percentage
    FROM world
    WHERE continent="Europe"

#### 6.  Show countries that have a GDP greater than every country in Europe.

    SELECT name
    FROM world
    WHERE gdp > (SELECT MAX(gdp)
    FROM world
    WHERE continent="Europe")

#### 7. Find the largest country (by area) in each continent, show the continent, the name and the area.

    SELECT continent, name, area FROM world x
    WHERE area >= ALL (SELECT area FROM world y
            WHERE y.continent=x.continent)

#### 8. List each continent and the name of the country that comes first alphabetically.

    SELECT continent, name FROM world x
      WHERE name <= ALL (SELECT name FROM world y
            WHERE y.continent=x.continent)

#### 9. Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

    SELECT name, continent, population 
    FROM world x
    WHERE 25000000 >= ALL (SELECT population FROM world y WHERE x.continent=y.continent)

#### 10. Some countries have populations more than three times that of all of their neighbours (in the same continent). Give the countries and continents.

    SELECT name, continent
    FROM world x
    WHERE population > ALL (SELECT population*3 FROM world y WHERE x.continent=y.continent AND x.name!=y.name)

### SUM and COUNT

#### 1. Show the total population of the world.

    SELECT SUM(population)
    FROM world

#### 2. List all the continents - just once each.

    SELECT DISTINCT continent
    FROM world

#### 3. Give the total GDP of Africa

    SELECT SUM(gdp)
    FROM world
    WHERE continent="Africa"

#### 4. How many countries have an area of at least 1000000

    SELECT COUNT(name)
    FROM world
    WHERE area >= 1000000

#### 5. What is the total population of ('Estonia', 'Latvia', 'Lithuania')

    SELECT SUM(population)
    FROM world
    WHERE name IN ('Estonia', 'Latvia', 'Lithuania')

#### 6. For each continent show the continent and number of countries.

    SELECT continent, COUNT(continent) number_of_countries
    FROM world
    GROUP BY continent

#### 7. For each continent show the continent and number of countries with populations of at least 10 million.

    SELECT continent, COUNT(continent) number_of_countries
    FROM world
    WHERE population >= 10000000
    GROUP BY continent

#### 8. List the continents that have a total population of at least 100 million.

    SELECT continent
    FROM world
    GROUP BY continent
    HAVING SUM(population) >= 100000000

### JOIN

#### 1. Show the matchid and player name for all goals scored by Germany.

    SELECT matchid, player
    FROM goal JOIN game ON(id=matchid)
    WHERE teamid="GER"

#### 2. Show id, stadium, team1, team2 for just game 1012.

    SELECT DISTINCT id,stadium,team1,team2
    FROM game JOIN goal ON(matchid=id)
    WHERE ID="1012"

#### 3. Show the player, teamid, stadium and mdate for every German goal.

    SELECT player,teamid,stadium,mdate
    FROM game JOIN goal ON (id=matchid)
    Where teamid="GER"

#### 4. Show the team1, team2 and player for every goal scored by a player called Mario.

    SELECT team1,team2,player
    FROM game JOIN goal ON (id=matchid)
    Where player LIKE 'Mario%'

#### 5. Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10.

    SELECT player, teamid, coach, gtime
    FROM goal JOIN eteam on teamid=id
    WHERE gtime<=10

#### 6. List the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

    SELECT mdate, teamname
    FROM game JOIN eteam ON (game.team1=eteam.id) 
    WHERE coach="Fernando Santos"

#### 7. List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.

    SELECT player
    FROM game JOIN goal ON(id=matchid)
    WHERE stadium="National Stadium, Warsaw"

#### 8. Show the name of all players who scored a goal against Germany.

    SELECT DISTINCT player
    FROM game JOIN goal ON matchid = id 
    WHERE ((team1='GER' AND team2!="GER") OR (team1!='GER' AND team2="GER")) AND teamid!="GER"

#### 9. Show teamname and the total number of goals scored.

    SELECT teamname, COUNT(teamname)
    FROM goal JOIN eteam ON (goal.teamid=eteam.id)
    GROUP BY teamname

#### 10. Show the stadium and the number of goals scored in each stadium.

    SELECT stadium, COUNT(1)
    FROM game JOIN goal ON matchid=id
    GROUP BY stadium

#### 11. For every match involving 'POL', show the matchid, date and the number of goals scored.

    SELECT matchid,mdate,COUNT(teamid)
    FROM game JOIN goal ON matchid=id
    WHERE teamid="POL" OR team1="POL" OR team2="POL"
    GROUP BY matchid,mdate

#### 12. For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'.

    SELECT matchid,mdate,COUNT(teamid)
    FROM game JOIN goal ON matchid=id
    WHERE teamid="GER"
    GROUP BY matchid,mdate

#### 13. List every match with the goals scored by each team as shown.

    SELECT 
      mdate,
      team1,
      SUM(CASE WHEN teamid = team1 THEN 1 ELSE 0 END) AS score1,
      team2,
      SUM(CASE WHEN teamid = team2 THEN 1 ELSE 0 END) AS score2
    FROM game
    LEFT JOIN goal ON matchid = id
    GROUP BY mdate, matchid, team1, team2

### More JOIN operations

#### 1. List the films where the yr is 1962.

    SELECT id, title
    FROM movie
    WHERE yr=1962

#### 2. Give year of 'Citizen Kane'.

    SELECT yr
    FROM movie
    WHERE title="Citizen Kane"

#### 3. List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

    SELECT id, title,yr
    FROM movie
    WHERE title LIKE "%Star Trek%"
    ORDER BY yr

#### 4. What id number does the actor 'Glenn Close' have?

    SELECT DISTINCT actor.id
    FROM casting JOIN actor ON casting.actorid=actor.id
    WHERE actor.name="GLenn Close"

#### 5. What is the id of the film 'Casablanca'

    SELECT id
    FROM movie
    WHERE title= 'Casablanca'

#### 6. Obtain the cast list for 'Casablanca'.

    SELECT actor.name
    FROM actor JOIN casting ON actor.id=casting.actorid
    WHERE movieid=11768

#### 7. Obtain the cast list for the film 'Alien'

    SELECT actor.name
    FROM casting JOIN actor ON actor.id=casting.actorid
    JOIN movie ON casting.movieid=movie.id
    WHERE title="Alien"

#### 8. List the films in which 'Harrison Ford' has appeared

    SELECT movie.title
    FROM casting JOIN actor ON casting.actorid=actor.id
    JOIN movie ON casting.movieid=movie.id
    WHERE actor.name='Harrison Ford'

#### 9. List the films where 'Harrison Ford' has appeared - but not in the starring role.

    SELECT movie.title
    FROM casting JOIN actor ON casting.actorid=actor.id
    JOIN movie ON casting.movieid=movie.id
    WHERE actor.name='Harrison Ford' AND casting.ord!=1

#### 10. List the films together with the leading star for all 1962 films.

    SELECT movie.title, actor.name
    FROM casting JOIN actor ON casting.actorid=actor.id
    JOIN movie ON casting.movieid=movie.id
    WHERE movie.yr=1962 AND casting.ord=1

#### 11. Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

    SELECT yr,COUNT(title) FROM
      movie JOIN casting ON movie.id=movieid
            JOIN actor   ON actorid=actor.id
    WHERE name='Rock Hudson'
    GROUP BY yr
    HAVING COUNT(title) > 2

#### 12. List the film title and the leading actor for all of the films 'Julie Andrews' played in.





### Using Null
### Self join

