# SOLUTIONS TO SQL ZOO PROBLEMS

This repo contains all of the solutions for the SQL Solo curriculum.

Link: [sqlzoo](https://www.sqlzoo.net)
Author: Rohan Sundar
Github: [rsundar](https://www.github.com/rsundar)

## SELECT Basics
[sqlzoo.net/wiki/SELECT_basics](sqlzoo.net/wiki/SELECT_basics)

#### 1. Introducing the world table of countries
The example uses a WHERE clause to show the population of 'France'. Note that strings (pieces of text that are data) should be in 'single quotes';

Modify it to show the population of Germany

``` sql
SELECT population FROM world
  WHERE name = 'Germany'
```

#### 2. Scandinavia
Checking a list The word IN allows us to check if an item is in a list. The example shows the name and population for the countries 'Brazil', 'Russia', 'India' and 'China'.

Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

``` sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

#### 3. Just the right size
Which countries are not too small and not too big? BETWEEN allows range checking (range specified is inclusive of boundary values). The example below shows countries with an area of 250,000-300,000 sq. km.

Modify it to show the country and the area for countries with an area between 200,000 and 250,000.

``` sql
SELECT name, area FROM world
  WHERE area BETWEEN 200000 AND 250000
```

## SELECT from WORLD Tutorial
[https://sqlzoo.net/wiki/SELECT_from_WORLD_Tutorial](https://sqlzoo.net/wiki/SELECT_from_WORLD_Tutorial)

#### Example Data

| name | continent | area | population | gdp |
|------|-----------|------|------------|-----|
| Afghanistan | Asia | 652230 | 25500100 | 20343000000 |
| Albania | Europe |28748 | 2831741 | 12960000000 |
| Algeria | Africa |2381741 | 37100000 | 188681000000 |
| Andorra | Europe |468 |	78115 | 3712000000 |
| Angola | Africa | 1246700 | 20609294 | 100990000000 |

#### 1. Introduction
Observe the result of running this SQL command to show the name, continent and population of all countries.

``` sql
SELECT name, continent, population
FROM world;
```

#### 2. Large countries
Show the name for the countries that have a population of at least 200 million. 200 million is 200000000, there are eight zeros.

``` sql
SELECT name FROM world
WHERE population > 200000000;
```

#### 3. Per-capita GDP
Give the name and the per capita GDP for those countries with a population of at least 200 million.

``` sql
SELECT name, gdp/population AS 'per capita GDP'
FROM world
WHERE population > 200000000;
```

#### 4. South America In millions
Show the `name` and `population` in millions for the countries of the `continent` 'South America'. Divide the population by 1000000 to get population in millions.

``` sql
SELECT name, population/1000000 AS 'population (millions)'
FROM world
WHERE continent = 'South America';
```

#### 5. France, Germany, Italy
Show the `name` and `population` for France, Germany and Italy.

``` sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

#### 6. United
Show the countries which have a `name` that includes the word 'United'.

``` sql
SELECT name
FROM world
WHERE name LIKE '%United%';
```

#### 7. Two ways to be big
Two ways to be big: A country is **big** if it has an area of more than 3 million sq km or it has a population of more than 250 million.

Show the countries that are big by area or big by population. Show name, population and area.

``` sql
SELECT name, population, area
FROM world
WHERE area > 3000000
  OR population > 250000000;
```

#### 8. One or the other (but not both)
Exclusive OR (XOR). Show the countries that are big by area or big by population but not both. Show name, population and area.

- Australia has a big area but a small population, it should be included.
- Indonesia has a big population but a small area, it should be included.
- China has a big population and big area, it should be excluded.
- United Kingdom has a small population and a small area, it should be excluded.

``` sql
SELECT name, population, area
FROM world
WHERE area > 3000000
  XOR population > 250000000;
```

#### 9. Rounding
Show the `name` and `population` in millions and the GDP in billions for the countries of the `continent` 'South America'. Use the ROUND function to show the values to two decimal places.

For South America show population in millions and GDP in billions both to 2 decimal places.

``` sql
SELECT name, ROUND(population/1000000, 2) AS 'Population (millions)', ROUND(gdp/1000000000, 2) AS 'GDP (billions)'
FROM world
WHERE continent = 'South America';
```

#### 10. Trillion dollar economies
Show the `name` and per-capita GDP for those countries with a GDP of at least one trillion (1000000000000; that is 12 zeros). Round this value to the nearest 1000.

Show per-capita GDP for the trillion dollar countries to the nearest $1000.

``` sql
SELECT name, ROUND(gdp/population, -3) AS 'per-capita GDP'
FROM world
WHERE gdp > 1000000000000;
```

#### 11. Name and capital have the same length
Greece has capital Athens.

Each of the strings 'Greece', and 'Athens' has 6 characters.

Show the name and capital where the name and the capital have the same number of characters.

``` sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

#### 12. Matching name and capital
The capital of Sweden is Stockholm. Both words start with the letter 'S'.

Show the name and the capital where the first letters of each match. Don't include countries where the name and the capital are the same word.

- You can use the function LEFT to isolate the first character.
- You can use <> as the NOT EQUALS operator.

``` sql
SELECT name, capital
FROM world
WHERE LEFT(name, 1) = LEFT(capital, 1)
  AND name <> capital;
```

#### 13. All the vowels
Equatorial Guinea and Dominican Republic have all of the vowels (a e i o u) in the name. They don't count because they have more than one word in the name.

Find the country that has all the vowels and no spaces in its name.

- You can use the phrase name NOT LIKE '%a%' to exclude characters from your results.
- The query shown misses countries like Bahamas and Belarus because they contain at least one 'a'.

``` sql
SELECT name
FROM world
WHERE name NOT LIKE '% %'
AND name LIKE '%a%'
AND name LIKE '%e%'
AND name LIKE '%i%'
AND name LIKE '%o%'
AND name LIKE '%u%'
```


