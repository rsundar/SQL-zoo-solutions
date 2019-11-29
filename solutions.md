# SOLUTIONS TO SQL ZOO PROBLEMS

This repo contains all of the solutions for the SQL Solo curriculum.

Link: [sqlzoo](https://www.sqlzoo.net)
Author: Rohan Sundar
Github: [rsundar](https://www.github.com/rsundar)

## SELECT Basics Solutions
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

## SELECT from WORLD Solutions
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

## SELECT from Nobel Solutions
[https://sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial](https://sqlzoo.net/wiki/SELECT_from_Nobel_Tutorial)

#### 1. Winners from 1950
Change the query shown so that it displays Nobel prizes for 1950.

``` sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950;
```

#### 2. 1962 Literature
Show who won the 1962 prize for Literature.

``` sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'Literature';
```

#### 3. Albert Einstein
Show the year and subject that won 'Albert Einstein' his prize.

``` sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

#### 4. Recent Peace Prizes
Give the name of the 'Peace' winners since the year 2000, including 2000.

``` sql
SELECT winner
FROM nobel
WHERE subject = 'Peace'
  AND yr >= 2000;
```

#### 5. Literature in the 1980's
Show all details (yr, subject, winner) of the Literature prize winners for 1980 to 1989 inclusive.

``` sql
SELECT *
FROM nobel
WHERE subject = 'Literature'
  AND yr >= 1980
  AND yr <= 1989;
```

#### 6. Only Presidents
Show all details of the presidential winners:
- Theodore Roosevelt
- Woodrow Wilson
- Jimmy Carter
- Barack Obama

``` sql
SELECT *
FROM nobel
WHERE winner IN ('Theodore Roosevelt', 'Woodrow Wilson', 'Jimmy Carter', 'Barack Obama');
```

#### 7. John
Show the winners with first name John.

``` sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```

#### 8. Chemistry and Physics from different years
Show the year, subject, and name of Physics winners for 1980 together with the Chemistry winners for 1984.

``` sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Physics' AND yr = 1980
OR subject = 'Chemistry' AND yr = 1984;
```

#### 9. Exclude Chemists and Medics
Show the year, subject, and name of winners for 1980 excluding Chemistry and Medicine.

``` sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
AND subject NOT IN ('Chemistry', 'Medicine');
```

#### 10. Early Medicine, Late Literature
Show `year`, `subject`, and `name` of people who won a 'Medicine' prize in an early year (before 1910, not including 1910) together with winners of a 'Literature' prize in a later year (after 2004, including 2004).

``` sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Medicine'
 AND yr < 1910
OR
subject = 'Literature'
 AND yr >= 2004;
```

### Harder Questions

#### 11. Umlaut
Find all details of the prize won by PETER GRÜNBERG.

``` sql
SELECT *
FROM nobel
WHERE winner = 'PETER GRÜNBERG'
```

#### 12. Apostrophe
Find all details of the prize won by EUGENE O'NEILL.

``` sql
SELECT *
FROM nobel
WHERE winner = 'EUGENE O\'NEILL'
```

#### 13. Knights of the realm
Knights in order

List the winners, year and subject where the winner starts with Sir. Show the the most recent first, then by name order.

``` sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC
```

#### 13. Chemistry and Physics last
The expression subject IN ('Chemistry','Physics') can be used as a value - it will be 0 or 1.

Show the 1984 winners and subject ordered by subject and winner name; but list Chemistry and Physics last.

``` sql
SELECT winner, subject
FROM nobel
WHERE yr = 1984
ORDER BY
CASE WHEN subject IN ('Physics', 'Chemistry') THEN 1 ELSE 0 END, subject, winner;
```

## SELECT within SELECT Solutions
[https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial](https://sqlzoo.net/wiki/SELECT_within_SELECT_Tutorial)

Table Structure: `world(name, continent, area, population, gdp)`

#### 1. Bigger than Russia
List each country name where the population is larger than that of 'Russia'.

``` sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia');
```

#### 2. Richer than UK
Show the countries in Europe with a per capita GDP greater than 'United Kingdom'.

``` sql
SELECT name
FROM world
WHERE continent = 'Europe'
  AND gdp/population > (SELECT gdp/population
    FROM world
    WHERE name = 'United Kingdom');
```

#### 3. Neighbors of Argentina and Australia
List the name and continent of countries in the continents containing either Argentina or Australia. Order by name of the country.

``` sql
SELECT name, continent
FROM world
WHERE continent IN (
  SELECT continent
  FROM world
  WHERE name IN ('Argentina', 'Australia')
)
ORDER BY name;
```

#### 4. Between Canada and Poland
Which country has a population that is more than Canada but less than Poland? Show the name and the population.

``` sql
SELECT name, population
FROM world
WHERE population > (SELECT population FROM world WHERE name = 'Canada')
  AND population < (SELECT population FROM world WHERE name = 'Poland');
```

#### 5. Percentages of Germany
Germany (population 80 million) has the largest population of the countries in Europe. Austria (population 8.5 million) has 11% of the population of Germany.

Show the name and the population of each country in Europe. Show the population as a percentage of the population of Germany.

``` sql
SELECT name, CONCAT(ROUND(population/(SELECT population FROM world WHERE name = 'Germany') * 100, 0), '%') AS '% of German Population'
FROM world
WHERE continent = 'Europe';
```

#### 6. Bigger than every country in Europe
Which countries have a GDP greater than every country in Europe? Give the name only. (Some countries may have NULL GDP values).

``` sql
SELECT name
FROM world
WHERE gdp > ALL(
  SELECT gdp
  FROM world
  WHERE continent = 'Europe'
    AND gdp > 0);
```

#### 7. Largest in each continent
Find the largest country (by area) in each continent, show the continent, the name and the area.

``` sql
SELECT continent, name, area FROM world x
  WHERE area >= ALL
    (SELECT area FROM world y
        WHERE y.continent=x.continent)
```

#### 8. First country of each continent (alphabetically)
List each continent and the name of the country that comes first alphabetically.

``` sql
SELECT continent, name
FROM world x
  WHERE name <= ALL
    (SELECT name
     FROM world y
     WHERE y.continent=x.continent);
```

### Difficult Questions That Utilize Techniques Not Covered In Prior Sections

#### 9.
Find the continents where all countries have a population <= 25000000. Then find the names of the countries associated with these continents. Show name, continent and population.

``` sql
SELECT name, continent, population
FROM world x
WHERE 25000000 > ALL(
  SELECT population
  FROM world y
  WHERE x.continent = y.continent
    AND population > 0
);
```

#### 10.
Some countries have populations more than three times that of any of their neighbours (in the same continent). Give the countries and continents.

``` sql
SELECT name, continent
FROM world x
WHERE population > ALL(
  SELECT population*3
  FROM world y
  WHERE x.continent = y.continent
  AND population > 0
  AND y.name != x.name
);
```