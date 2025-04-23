
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

#### 1️.  Show the population of Germany.

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

#### 1️.  Show the name, continent and population of all countries.

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



