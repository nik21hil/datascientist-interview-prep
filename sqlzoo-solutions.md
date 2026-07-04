<h1 align="center">🗄️ SQLZoo Problem Solutions</h1> 

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

## 1 SELECT name 

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


## 2 SELECT from World  










## 3 SELECT from Nobel 

## 4 SELECT within SELECT 

## 5 SUM and COUNT 

## 6 JOIN

## 7 More JOIN operations

## 8 Using Null

## 8+ Numeric Examples

## 9- Window function

## 9+ COVID 19

## 9 Self join


### Solution

```sql
SELECT product_id
FROM Products
WHERE low_fats = 'Y'
  AND recyclable = 'Y';
```


