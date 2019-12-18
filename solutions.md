# SOLUTIONS TO SQL ZOO PROBLEMS

This repo contains all of the solutions for the SQL Solo curriculum.

**Link**: [sqlzoo](https://www.sqlzoo.net)

**Author**: Rohan Sundar

**Github**: [rsundar](https://www.github.com/rsundar)

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

## SUM and COUNT
[https://sqlzoo.net/wiki/SUM_and_COUNT](https://sqlzoo.net/wiki/SUM_and_COUNT)

Data: `world(name, continent, area, population, gdp)`

#### 1. Total world population
Show the total population of the world.

``` sql
SELECT SUM(population)
FROM world;
```

#### 2. List of continents
List all the continents - just once each.

``` sql
SELECT DISTINCT(continent)
FROM world;
```

#### 3. GDP of Africa
Give the total GDP of Africa.

``` sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```

#### 4. Count the big countries
How many countries have an area of at least 1000000.

``` sql
SELECT COUNT(name)
FROM world
WHERE area > 1000000
```

#### 5. Baltic states population
What is the total population of ('Estonia', 'Latvia', 'Lithuania').

``` sql
SELECT SUM(population)
FROM world
WHERE name IN ('Estonia', 'Latvia', 'Lithuania');
```

### Using GROUP BY and HAVING

#### 6. Counting the countries of each continent
For each continent show the continent and number of countries.

``` sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```

#### 7.
For each continent show the continent and number of countries with populations of at least 10 million.

``` sql
SELECT continent, COUNT(name) as 'Countires with population > 1m'
FROM world
WHERE population >= 10000000
GROUP BY continent
```

#### 8. Counting big continents
List the continents that have a total population of at least 100 million.

``` sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population) > 100000000;
```

## The JOIN operation
[https://sqlzoo.net/wiki/The_JOIN_operation](https://sqlzoo.net/wiki/The_JOIN_operation)

#### JOIN and UEFA EURO 2012

This tutorial introduces JOIN which allows you to use data from two or more tables. The tables contain all matches and goals from UEFA EURO 2012 Football Championship in Poland and Ukraine.

#### 1.
The first example shows the goal scored by a player with the last name 'Bender'. The * says to list all the columns in the table - a shorter way of saying matchid, teamid, player, gtime

Modify it to show the matchid and player name for all goals scored by Germany. To identify German players, check for: teamid = 'GER'

``` sql
SELECT matchid, player
FROM goal
WHERE teamid LIKE 'GER';
```

#### 2.
From the previous query you can see that Lars Bender's scored a goal in game 1012. Now we want to know what teams were playing in that match.

Notice in that the column matchid in the goal table corresponds to the id column in the game table. We can look up information about game 1012 by finding that row in the game table.

Show id, stadium, team1, team2 for just game 1012

``` sql
SELECT id, stadium, team1, team2
FROM game
WHERE id = '1012';
```

#### 3.
You can combine the two steps into a single query with a JOIN.

```sql
SELECT * FROM game JOIN goal ON (id=matchid)
```

The FROM clause says to merge data from the goal table with that from the game table. The ON says how to figure out which rows in game go with which rows in goal - the matchid from goal must match id from game. (If we wanted to be more clear/specific we could say
ON (game.id=goal.matchid)

The code below shows the player (from the goal) and stadium name (from the game table) for every goal scored.

Modify it to show the player, teamid, stadium and mdate for every German goal.

``` sql
SELECT player, teamid, stadium, mdate
FROM game
JOIN goal ON (game.id = goal.matchid)
WHERE teamid = 'GER';
```

#### 4.
Use the same `JOIN` as in the previous question.

Show the team1, team2 and player for every goal scored by a player called Mario `player LIKE 'Mario%'`

``` sql
SELECT team1, team2, player
FROM game
JOIN goal ON (game.id = goal.matchid)
WHERE player LIKE 'Mario%';
```

#### 5.
The table eteam gives details of every national team including the coach. You can JOIN goal to eteam using the phrase goal JOIN eteam on teamid=id.

Show player, teamid, coach, gtime for all goals scored in the first 10 minutes gtime<=10.

``` sql
SELECT player, teamid, coach, gtime
FROM goal
JOIN eteam ON (goal.teamid = eteam.id)
WHERE gtime <= 10;
```

#### 6.
To JOIN game with eteam you could use either
game JOIN eteam ON (team1=eteam.id) or game JOIN eteam ON (team2=eteam.id).

Notice that because id is a column name in both game and eteam you must specify eteam.id instead of just id.

List the the dates of the matches and the name of the team in which 'Fernando Santos' was the team1 coach.

``` sql
SELECT mdate, teamname
FROM game
JOIN eteam ON (eteam.id = game.team1)
WHERE eteam.coach = 'Fernando Santos'
```

#### 7.
List the player for every goal scored in a game where the stadium was 'National Stadium, Warsaw'.

``` sql
SELECT player
FROM goal
JOIN game ON (goal.matchid = game.id)
WHERE game.stadium = 'National Stadium, Warsaw';
```

### More difficult questions

#### 8.
The example query shows all goals scored in the Germany-Greece quarterfinal.

Instead show the name of all players who scored a goal against Germany.

``` sql
SELECT DISTINCT(player)
FROM game
JOIN goal ON (goal.matchid = game.id)
WHERE 'GER' IN (game.team1, game.team2)
  AND teamid != 'GER';
```

#### 9.
Show teamname and the total number of goals scored.

``` sql
SELECT teamname, COUNT(teamname) AS 'Goals Scored'
FROM eteam
JOIN goal ON (eteam.id = goal.teamid)
GROUP BY teamname;
```

#### 10.
Show the stadium and the number of goals scored in each stadium.

``` sql
SELECT stadium, COUNT(stadium) AS 'Goals'
FROM game
JOIN goal ON (game.id = goal.matchid)
GROUP BY stadium;
```

#### 11.
For every match involving 'POL', show the matchid, date and the number of goals scored.

``` sql
SELECT matchid, mdate, COUNT(matchid)
FROM game
JOIN goal ON (goal.matchid = game.id)
WHERE 'POL' IN (game.team1, game.team2)
GROUP BY mdate, matchid;
```

#### 12.
For every match where 'GER' scored, show matchid, match date and the number of goals scored by 'GER'

``` sql
SELECT matchid, mdate, COUNT(matchid) AS 'Goals by GER'
FROM game
JOIN goal ON (goal.matchid = game.id)
WHERE goal.teamid = 'GER'
GROUP BY mdate, matchid;
```

#### 13.
List every match with the goals scored by each team as shown. This will use "CASE WHEN" which has not been explained in any previous exercises.

``` sql
SELECT mdate,
  team1, SUM(CASE WHEN (goal.teamid = game.team1) THEN 1 ELSE 0 END) AS score1,
  team2, SUM(CASE WHEN (goal.teamid = game.team2) THEN 1 ELSE 0 END) AS score2
FROM game
LEFT JOIN goal ON (game.id = goal.matchid)
GROUP BY mdate, team1, team2
ORDER BY mdate, matchid, team1, team2;
```

### More JOIN operation

[https://sqlzoo.net/wiki/More_JOIN_operations](https://sqlzoo.net/wiki/More_JOIN_operations)

This tutorial introduces the notion of a join. The database consists of three tables `movie` , `actor` and `casting`.

#### 1. 1962 movies
List the films where the yr is 1962 [Show id, title]

``` sql
SELECT id, title
FROM movie
WHERE yr = 1962;
```

#### 2. When was Citizen Kane released?
Give year of 'Citizen Kane'.

``` sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane';
```

#### 3. Star Trek movies
List all of the Star Trek movies, include the id, title and yr (all of these movies include the words Star Trek in the title). Order results by year.

``` sql
SELECT id, title, yr
FROM movie
WHERE title LIKE 'Star Trek%';
```

#### 4. id for actor Glenn Close
What id number does the actor 'Glenn Close' have?

``` sql
SELECT id
FROM actor
WHERE name = 'Glenn Close';
```

#### 5. id for Casablanca
What is the id of the film 'Casablanca'?

``` sql
SELECT id
FROM movie
WHERE title = 'Casablanca';
```

#### 6. Cast list for Casablanca
Obtain the cast list for 'Casablanca'.

Use movieid=11768, (or whatever value you got from the previous question).

``` sql
SELECT actor.name
FROM actor
JOIN casting ON (actor.id = casting.actorid)
WHERE casting.movieid = 11768;
```

#### 7. Alien cast list
Obtain the cast list for the film 'Alien'

``` sql
SELECT actor.name
FROM actor
JOIN casting ON (casting.actorid = actor.id)
JOIN movie ON (movie.id = casting.movieid)
WHERE movie.title = 'Alien';
```

#### 8. Harrison Ford movies
List the films in which 'Harrison Ford' has appeared.

``` sql
SELECT movie.title
FROM movie
JOIN casting ON (casting.movieid = movie.id)
JOIN actor ON (actor.id = casting.actorid)
WHERE actor.name = 'Harrison Ford';
```

#### 9. Harrison Ford as a supporting actor
List the films where 'Harrison Ford' has appeared - but not in the starring role.

``` sql
SELECT movie.title
FROM movie
JOIN casting ON (casting.movieid = movie.id)
JOIN actor ON (actor.id = casting.actorid)
WHERE actor.name = 'Harrison Ford'
  AND casting.ord != 1;
```

#### 10. Lead actors in 1962 movies
List the films together with the leading star for all 1962 films.

``` sql
SELECT movie.title, actor.name
FROM movie
JOIN casting ON (movie.id = casting.movieid)
JOIN actor ON (actor.id = casting.actorid)
WHERE movie.yr = 1962
  AND casting.ord = 1;
```

#### 11. Busy years for Rock Hudson
Which were the busiest years for 'Rock Hudson', show the year and the number of movies he made each year for any year in which he made more than 2 movies.

``` sql
SELECT yr, COUNT(movie.title) AS 'Movies'
FROM movie
JOIN casting ON (movie.id = casting.movieid)
JOIN actor ON (casting.actorid = actor.id)
WHERE actor.name = 'Rock Hudson'
GROUP BY movie.yr
HAVING COUNT(movie.title) > 2;
```

#### 12. Lead actor in Julie Andrews movies
List the film title and the leading actor for all of the films 'Julie Andrews' played in.

``` sql
SELECT movie.title, actor.name
FROM movie
JOIN casting ON (movie.id = casting.movieid AND ord = 1)
JOIN actor ON (casting.actorid = actor.id)
WHERE movie.id IN (
  SELECT casting.movieid
  FROM casting
  WHERE casting.actorid IN (
    SELECT actor.id
    FROM actor
    WHERE actor.name = 'Julie Andrews'))
```

#### 13. Actors with 30 leading roles
Obtain a list, in alphabetical order, of actors who've had at least 30 starring roles.

``` sql
SELECT actor.name
FROM actor
JOIN casting ON (actor.id = casting.actorid AND ord = 1)
GROUP BY actor.name
HAVING COUNT(actor.name) >= 30
ORDER BY actor.name;
```

#### 14.
List the films released in the year 1978 ordered by the number of actors in the cast, then by title.

``` sql
SELECT title, COUNT(actorid) as cast
FROM movie
JOIN casting ON (movie.id = casting.movieid)
WHERE yr = 1978
GROUP BY title
ORDER BY cast DESC, title;
```

#### 15.
List all the people who have worked with 'Art Garfunkel'.

``` sql
SELECT DISTINCT(name)
FROM actor
JOIN casting ON (actor.id = casting.actorid)
WHERE movieid IN (
  SELECT movieid
  FROM casting
  JOIN actor ON (casting.actorid = actor.id AND actor.name='Art Garfunkel')
)
AND actor.name != 'Art Garfunkel'
GROUP BY name;
```

### Using Null
[https://sqlzoo.net/wiki/Using_Null](https://sqlzoo.net/wiki/Using_Null)

#### Teachers and Departments

The school includes many departments. Most teachers work exclusively for a single department. Some teachers have no department.

#### NULL, INNER JOIN, LEFT JOIN, RIGHT JOIN

#### 1.
List the teachers who have NULL for their department.

``` sql
SELECT name
FROM teacher
WHERE dept IS NULL;
```

#### 2.
Note the INNER JOIN misses the teachers with no department and the departments with no teacher.

``` sql
SELECT teacher.name, dept.name
FROM teacher
INNER JOIN dept ON (teacher.dept = dept.id);
```

#### 3.
Use a different JOIN so that all teachers are listed.

``` sql
SELECT teacher.name, dept.name
FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id);
```

#### 4.
Use a different JOIN so that all departments are listed.

``` sql
SELECT teacher.name, dept.name
FROM teacher
RIGHT JOIN dept ON (teacher.dept = dept.id)
```

#### 5.
Use COALESCE to print the mobile number. Use the number '07986 444 2266' if there is no number given. Show teacher name and mobile number or '07986 444 2266'.

``` sql
SELECT name, COALESCE(mobile, '07986 444 2266') AS mobile
FROM teacher;
```

#### 6.
Use the COALESCE function and a LEFT JOIN to print the teacher name and department name. Use the string 'None' where there is no department.

``` sql
SELECT teacher.name, COALESCE(dept.name, 'None') as dept
FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id);
```

#### 7.
Use COUNT to show the number of teachers and the number of mobile phones.

``` sql
SELECT COUNT(name) AS teachers, COUNT(mobile) as mobiles
FROM teacher;
```

#### 8.
Use COUNT and GROUP BY dept.name to show each department and the number of staff. Use a RIGHT JOIN to ensure that the Engineering department is listed.

``` sql
SELECT dept.name, COUNT(teacher.name) AS staff
FROM teacher
RIGHT JOIN dept ON (teacher.dept = dept.id)
GROUP BY dept.name;
```

#### 9.
Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2 and 'Art' otherwise.

``` sql
SELECT teacher.name,
CASE WHEN dept.id IN (1, 2) THEN 'Sci' ELSE 'Art' END
FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id);
```

#### 10.
Use CASE to show the name of each teacher followed by 'Sci' if the teacher is in dept 1 or 2, show 'Art' if the teacher's dept is 3 and 'None' otherwise.

``` sql
SELECT teacher.name,
CASE
WHEN dept.id IN (1, 2) THEN 'Sci'
WHEN dept.id = 3 THEN 'Art'
ELSE 'None' END
FROM teacher
LEFT JOIN dept ON (teacher.dept = dept.id);
```

### Self Join
[https://sqlzoo.net/wiki/Self_join](https://sqlzoo.net/wiki/Self_join)

#### Edinburgh Buses

#### 1.
How many stops are in the database.

``` sql
SELECT COUNT(id) AS stops
FROM stops;
```

#### 2.
Find the id value for the stop 'Craiglockhart'.

``` sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart';
```

#### 3.
Give the id and the name for the stops on the '4' 'LRT' service.

``` sql
SELECT id, name
FROM stops
JOIN route ON (stops.id = route.stop)
WHERE route.num = 4
  AND route.company = 'LRT';
```

#### 4.
The query shown gives the number of routes that visit either London Road (149) or Craiglockhart (53). Run the query and notice the two services that link these stops have a count of 2. Add a HAVING clause to restrict the output to these two routes.

``` sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) = 2;
```

#### 5.
Execute the self join shown and observe that b.stop gives all the places you can get to from Craiglockhart, without changing routes. Change the query so that it shows the services from Craiglockhart to London Road.

``` sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
WHERE a.stop = 53
  AND b.stop = 149;
```

#### 6.
The query shown is similar to the previous one, however by joining two copies of the stops table we can refer to stops by name rather than by number. Change the query so that the services between 'Craiglockhart' and 'London Road' are shown. If you are tired of these places try 'Fairmilehead' against 'Tollcross'.

``` sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a
JOIN route b ON(a.company = b.company AND a.num = b.num)
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart' AND stopb.name = 'London Road';
```

#### 7.
Give a list of all the services which connect stops 115 and 137 ('Haymarket' and 'Leith').

``` sql
SELECT DISTINCT a.company, a.num
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name = 'Haymarket' AND stopb.name = 'Leith';
```

#### 8.
Give a list of the services which connect the stops 'Craiglockhart' and 'Tollcross'.

``` sql
SELECT DISTINCT a.company, a.num
FROM route a
JOIN route b ON (a.num = b.num AND a.company = b.company)
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopa.name = 'Craiglockhart'
  AND stopb.name = 'Tollcross';
```

#### 9.
Give a distinct list of the stops which may be reached from 'Craiglockhart' by taking one bus, including 'Craiglockhart' itself, offered by the LRT company. Include the company and bus no. of the relevant services.

``` sql
SELECT stopa.name, a.company, a.num
FROM route a
JOIN route b ON (a.num = b.num AND a.company = b.company)
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
WHERE stopb.name = 'Craiglockhart';
```

#### 10.
Find the routes involving two buses that can go from Craiglockhart to Lochend.
Show the bus no. and company for the first bus, the name of the stop for the transfer, and the bus no. and company for the second bus.

``` sql
SELECT DISTINCT a.num, a.company, stopb.name, c.num, c.company
FROM route a
JOIN route b ON (a.company = b.company AND a.num = b.num)
JOIN ( route c JOIN route d ON (c.company = d.company AND c.num= d.num))
JOIN stops stopa ON (a.stop = stopa.id)
JOIN stops stopb ON (b.stop = stopb.id)
JOIN stops stopc ON (c.stop = stopc.id)
JOIN stops stopd ON (d.stop = stopd.id)
WHERE stopa.name = 'Craiglockhart' AND stopd.name = 'Sighthill'
  AND  stopb.name = stopc.name
ORDER BY LENGTH(a.num), b.num, stopb.id, LENGTH(c.num), d.num;
```