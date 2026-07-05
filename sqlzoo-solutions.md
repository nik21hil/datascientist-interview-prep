<h1 align="center">🗄️ SQLZoo Problem Solutions</h1> 

---

### 0 SELECT basics 

#### 1. Show the population of Germany

```sql
SELECT population
FROM world
WHERE name = 'Germany';
```

#### 2. Show the name and the population for 'Sweden', 'Norway' and 'Denmark'.

```sql
SELECT name, population
FROM world
WHERE name IN ('Sweden', 'Norway', 'Denmark');
```

#### 3. show the country and the area for countries with an area between 200,000 and 250,000. 

```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000;
```

---

### 1 SELECT name 

#### 1. Find the country that start with Y. 

```sql
SELECT name 
FROM world
WHERE UPPER(name) LIKE 'Y%';
```

#### 2. Find the countries that end with y.

```sql
SELECT name 
FROM world
WHERE UPPER(name) LIKE '%Y';
```

#### 3. Find the countries that contain the letter x.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '%X%';
```

#### 4. Find the countries that end with land.

```sql
SELECT name 
FROM world
WHERE UPPER(name) LIKE '%LAND';
```

#### 5. Find the countries that start with C and end with ia.

```sql
SELECT name 
FROM world
WHERE UPPER(name) LIKE 'C%IA'
ORDER BY 1; 
```

#### 6. Find the country that has oo in the name.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '%OO%';
```

#### 7. Find the countries that have three or more a in the name.

```sql
SELECT name 
FROM world
WHERE UPPER(name) LIKE '%A%A%A%';
```

#### 8. Find the countries that have "t" as the second character.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '_T%'
ORDER BY name;
```

#### 9. Find the countries that have two "o" characters separated by two others.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '%O__O%';
```

#### 10. Find the countries that have exactly four characters.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '____';
```

#### 11. Find the country where the name is the capital city.

```sql
SELECT name
FROM world
WHERE name = capital;
```

#### 12. Find the country where the capital is the country plus "City".

```sql
SELECT name
FROM world
WHERE UPPER(capital) = Concat(UPPER(name), ' CITY');
```

#### 13. Find the capital and the name where the capital includes the name of the country.

```sql
SELECT capital, name 
FROM world 
WHERE UPPER(capital) LIKE UPPER(CONCAT('%', name, '%'));
```

#### 14. Find the capital and the name where the capital is an extension of name of the country.

```sql
SELECT capital, name 
FROM world 
WHERE UPPER(capital) LIKE UPPER(CONCAT(name, '_%'));
```

#### 15. Show the name and the extension where the capital is a proper (non-empty) extension of name of the country.

```sql
SELECT name, REPLACE(capital, name, '') AS extension
FROM world 
WHERE UPPER(capital) LIKE UPPER(CONCAT(name, '_%'));
```

---

### 2 SELECT from World  

#### 1. Observe the result of running this SQL command to show the name, continent and population of all countries.

```sql
SELECT name, continent, population
FROM world;
```

#### 2. Show the name for the countries that have a population of at least 200 million.

```sql
SELECT name 
FROM world
WHERE population > 200000000;
```

#### 3. Give the name and the per capita GDP for countries with a population of at least 200 million.

```sql
SELECT name, (gdp/population) AS gdp_per_capita
FROM world
WHERE population > 200000000;
```

#### 4. Show the name and population in millions for the countries of South America.

```sql
SELECT name, population/1000000 AS population_in_millions
FROM world
WHERE continent = 'South America';
```

#### 5. Show the name and population for France, Germany, and Italy.

```sql
SELECT name, population
FROM world
WHERE name IN ('France', 'Germany', 'Italy');
```

#### 6. Show the countries which have a name that includes the word `United`.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '%UNITED%';
```

#### 7. Show the countries that are big by area or population.

```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 
OR population > 250000000; 
```

#### 8. Show the countries that are big by area or population, but not both.

```sql
SELECT name, population, area
FROM world
WHERE 
area > 3000000 AND population < 250000000
OR
area < 3000000 AND population > 250000000
; 
```

#### 9. Show the name, population, and GDP for South American countries, rounded appropriately.

```sql
SELECT name, 
ROUND(population/1000000,2) AS population_in_millions,
ROUND(gdp/1000000000,2) AS gdp_in_billions
FROM world
WHERE continent = 'South America';
```

#### 10. Show per-capita GDP for trillion dollar countries, rounded to the nearest 1000.

```sql
SELECT name, 
ROUND(gdp/population,-3) AS gdp_per_capita_in_thousands
FROM world
WHERE gdp > 1000000000000;
```

#### 11. Show the name and capital where the name and capital have the same number of characters.

```sql
SELECT name, capital
FROM world
WHERE LENGTH(name) = LENGTH(capital);
```

#### 12. Show the name and capital where the first letters match but the name and capital are different.

```sql
SELECT name, capital
FROM world
WHERE name <> capital 
AND LEFT(name, 1) = LEFT(capital, 1);
```

#### 13. Find countries that contain all vowels and no spaces in their name.

```sql
SELECT name
FROM world
WHERE UPPER(name) LIKE '%A%'
AND UPPER(name) LIKE '%E%'
AND UPPER(name) LIKE '%I%'
AND UPPER(name) LIKE '%O%'
AND UPPER(name) LIKE '%U%'
AND UPPER(name) NOT LIKE '% %';
```

---

### 3 SELECT from Nobel 

#### 1. Show Nobel prizes for 1950.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1950;
```

#### 2. Show the winner of the 1962 Literature prize.

```sql
SELECT winner
FROM nobel
WHERE yr = 1962
AND UPPER(subject) = 'LITERATURE';
```

#### 3. Show the year and subject for Albert Einstein.

```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein';
```

#### 4. Show Peace prize winners since 2000.

```sql
SELECT winner
FROM nobel
WHERE UPPER(subject) = 'PEACE' 
AND yr >= 2000;
```

#### 5. Show Literature prize winners from 1980 to 1989.

```sql
SELECT yr, subject,winner
FROM nobel
WHERE UPPER(subject) = 'LITERATURE' 
AND yr BETWEEN 1980 AND 1989;
```

#### 6. Show prize details for selected US presidents.

```sql
SELECT * 
FROM nobel
WHERE winner IN 
(
'Theodore Roosevelt',
'Thomas Woodrow Wilson',
'Jimmy Carter',
'Barack Obama'
);
```

#### 7. Show winners with first name `John`.

```sql
SELECT winner
FROM nobel
WHERE UPPER(winner) LIKE ('JOHN%');
```

#### 8. Show Physics winners from 1980 plus CHemistry winners from 1984.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE 
(UPPER(subject) = 'PHYSICS' AND yr = 1980)
OR
(UPPER(subject) = 'CHEMISTRY' AND yr = 1984);
```

#### 9. Show winners from 1980 excluding Chemistry and Medicine.

```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980
AND subject NOT IN ('Chemistry','Medicine');
```

#### 10. Show early Medicine winners and recent Literature winners.

```sql

```

#### 11. Find the winner with special characters in the name.

```sql

```

#### 12. Find the winner with an apostrophe in the name.

```sql

```

#### 13. Show winners whose name starts with `Sir`.

```sql

```

#### 14. Show 1984 winners ordered by subject and winner.

```sql

```

---

### 4 SELECT within SELECT 

#### 1. List countries with population greater than Russia.

```sql

```

#### 2. Show countries in Europe with per-capita GDP greater than the United Kingdom.

```sql

```

#### 3. List countries in the same continents as Argentina or Australia.

```sql

```

#### 4. Show countries with population greater than Canada but less than Poland.

```sql

```

#### 5. Show European countries with population as a percentage of Germany.

```sql

```

#### 6. Show countries with GDP greater than every country in Europe.

```sql

```

#### 7. Find the largest country by area in each continent.

```sql

```

#### 8. List the first country alphabetically in each continent.

```sql

```

#### 9. Find continents where every country has population less than or equal to 25 million.

```sql

```

#### 10. Find countries from continents where all countries have population less than or equal to 25 million.

```sql

```

#### 11. Find countries with population more than three times that of any other country in the same continent.

```sql

```

---

### 5 SUM and COUNT 

#### 1. Show the total population of the world.

```sql

```

#### 2. List all continents only once.

```sql

```

#### 3. Show the total GDP of Africa.

```sql

```

#### 4. Count the countries with area of at least 1,000,000.

```sql

```

#### 5. Show the total population of Estonia, Latvia, and Lithuania.

```sql

```

#### 6. For each continent, show the continent and number of countries.

```sql

```

#### 7. For each continent, show the continent and number of countries with population of at least 10 million.

```sql

```

#### 8. Show continents with total population of at least 100 million.

```sql

```

---

### 6 JOIN

#### 1. Show match id and player name for goals scored by Germany.

```sql

```

#### 2. Show id, stadium, team1, and team2 for a given game.

```sql

```

#### 3. Show player, team id, stadium, and date for German goals.

```sql

```

#### 4. Show team1, team2, and player for goals by a specific player.

```sql

```

#### 5. Show player, team id, coach, and goal time for goals scored in the first 10 minutes.

```sql

```

#### 6. Show match dates and team names where a specific coach was involved.

```sql

```

#### 7. Show players who scored in a specific stadium.

```sql

```

#### 8. Show players who scored against Germany.

```sql

```

#### 9. Show team name and total goals scored by each team.

```sql

```

#### 10. Show stadium and number of goals scored in each stadium.

```sql

```

#### 11. Show match id, date, and number of goals for matches involving a specific team.

```sql

```

#### 12. Show match id, date, and number of goals scored by Germany.

```sql

```

#### 13. Show every match with team names and score.

```sql

```

---

### 7 More JOIN operations

#### 1. List the films released in 1962.

```sql

```

#### 2. Show the year when `Citizen Kane` was released.

```sql

```

#### 3. List all `Star Trek` movies, including id, title, and year.

```sql

```

#### 4. Find the id number for actor Glenn Close.

```sql

```

#### 5. Find the id number for the film `Casablanca`.

```sql

```

#### 6. Show the cast list for `Casablanca`.

```sql

```

#### 7. Show the cast list for `Alien`.

```sql

```

#### 8. List the films in which Harrison Ford appeared.

```sql

```

#### 9. List films where Harrison Ford appeared but was not the starring actor.

```sql

```

#### 10. List films with Art Garfunkel.

```sql

```

#### 11. List lead actors in Julie Andrews films released after 1978.

```sql

```

#### 12. Find actors with at least 15 starring roles.

```sql

```

#### 13. List films released in 1978 ordered by cast size.

```sql

```

#### 14. List people who worked with Art Garfunkel.

```sql

```

---

### 8 Using Null

#### 1. List teachers who have NULL for their department.

```sql

```

#### 2. Use INNER JOIN to show teacher and department details.

```sql

```

#### 3. Use LEFT JOIN to show all teachers and their departments.

```sql

```

#### 4. Use COALESCE to show mobile number or default value.

```sql

```

#### 5. Use COALESCE to show department name or default value.

```sql

```

#### 6. Count the number of teachers.

```sql

```

#### 7. Count the number of teachers by department.

```sql

```

#### 8. Use CASE to classify teachers by department.

```sql

```

#### 9. Use CASE to classify teachers into custom groups.

```sql

```

---

### 8+ Numeric Examples

#### 1. Numeric example question 1.

```sql

```

#### 2. Numeric example question 2.

```sql

```

#### 3. Numeric example question 3.

```sql

```

#### 4. Numeric example question 4.

```sql

```

#### 5. Numeric example question 5.

```sql

```

#### 6. Numeric example question 6.

```sql

```

#### 7. Numeric example question 7.

```sql

```

#### 8. Numeric example question 8.

```sql

```

---

### 9- Window function

#### 1. Show basic election results for a selected constituency and year.

```sql

```

#### 2. Show party and votes for a selected constituency.

```sql

```

#### 3. Use RANK to rank candidates within a constituency.

```sql

```

#### 4. Show ranking results for a selected constituency.

```sql

```

#### 5. Show winning candidates for selected constituencies.

```sql

```

#### 6. Count seats won by each party.

```sql

```

---

### 9+ COVID 19

#### 1. Show COVID data for a selected country.

```sql

```

#### 2. Show confirmed cases for a selected country and date range.

```sql

```

#### 3. Show daily new cases using window functions.

```sql

```

#### 4. Show weekly changes using window functions.

```sql

```

#### 5. Show percentage increases in confirmed cases.

```sql

```

#### 6. Find peak daily increases by country.

```sql

```

#### 7. Compare countries using confirmed cases and deaths.

```sql

```

#### 8. Rank countries by selected COVID metric.

```sql

```

---

### 9 Self join

#### 1. Find the stop id for `Craiglockhart`.

```sql

```

#### 2. Find the stops used by selected services.

```sql

```

#### 3. Show routes involving selected stops.

```sql

```

#### 4. Find services connecting two selected stops.

```sql

```

#### 5. Show services from one stop to another.

```sql

```

#### 6. Find routes from `Craiglockhart` to `London Road`.

```sql

```

#### 7. Show routes involving two named stops.

```sql

```

#### 8. Find two-bus routes from one stop to another.

```sql

```

#### 9. Show transfer points for two-bus journeys.

```sql

```

#### 10. Show complete two-bus journey details.

```sql

```



