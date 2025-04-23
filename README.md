
# SQLZOO solutions

I’ve just completed the sixth course in the Google Data Analytics program and wanted to sharpen my SQL skills before moving on to R.
This repository contains my solutions and notes from working through the SQLZOO challenges.

## Table of Contents

- [0 SELECT basics](#select-basics)
- [1 SELECT name](#select-name)
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


### SELECT name

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

### SELECT from World
