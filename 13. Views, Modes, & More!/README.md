# Views, Modes, & More!
## Views
- Instead of writing this query all the time:
```mysql
SELECT title, released_year, genre, rating, first_name, last_name
FROM reviews r1
JOIN series s
  ON s.id = r.series_id
JOIN reviewers r2
  ON r2.id = r1.reviewer_id;
```
- We can create a `VIEW`:
```mysql
CREATE VIEW full_reviews AS
  SELECT title, released_year, genre, rating, first_name, last_name
  FROM reviews r1
  JOIN series s
    ON s.id = r1.series_id
  JOIN reviewers r2
    ON r2.id = r1.reviewer_id;
```
- Now we can treat that `VIEW` as a virtual table 
  - At least when it comes to `SELECT`ing
```mysql
SELECT * FROM full_reviews;
```
| Title                | Released Year | Genre      | Rating | First Name | Last Name   |
|---------------------|---------------|------------|--------|------------|-------------|
| Archer              | 2009          | Animation  | 8.0    | Thomas     | Stoneman    |
| Archer              | 2009          | Animation  | 7.5    | Wyatt      | Skaggs      |
| Archer              | 2009          | Animation  | 8.5    | Kimbra     | Masters     |
| Archer              | 2009          | Animation  | 7.7    | Domingo    | Cortes      |
| Archer              | 2009          | Animation  | 8.9    | Colt       | Steele      |
| Arrested Development| 2003          | Comedy     | 8.1    | Thomas     | Stoneman    |
| Arrested Development| 2003          | Comedy     | 6.0    | Domingo    | Cortes      |
| Arrested Development| 2003          | Comedy     | 8.0    | Kimbra     | Masters     |
| Arrested Development| 2003          | Comedy     | 8.4    | Pinkie     | Petit       |
| Arrested Development| 2003          | Comedy     | 9.9    | Colt       | Steele      |
| Bob's Burgers       | 2011          | Animation  | 7.0    | Thomas     | Stoneman    |
| Bob's Burgers       | 2011          | Animation  | 7.5    | Pinkie     | Petit       |
| Bob's Burgers       | 2011          | Animation  | 8.0    | Domingo    | Cortes      |
| Bob's Burgers       | 2011          | Animation  | 7.1    | Kimbra     | Masters     |
| Bob's Burgers       | 2011          | Animation  | 8.0    | Colt       | Steele      |
| Bojack Horseman     | 2014          | Animation  | 7.5    | Thomas     | Stoneman    |
| Bojack Horseman     | 2014          | Animation  | 7.8    | Kimbra     | Masters     |
| Bojack Horseman     | 2014          | Animation  | 8.3    | Domingo    | Cortes      |
| Bojack Horseman     | 2014          | Animation  | 7.6    | Wyatt      | Skaggs      |
| Bojack Horseman     | 2014          | Animation  | 8.5    | Colt       | Steele      |
| Breaking Bad        | 2008          | Drama      | 9.5    | Thomas     | Stoneman    |
| Breaking Bad        | 2008          | Drama      | 9.0    | Kimbra     | Masters     |
| Breaking Bad        | 2008          | Drama      | 9.1    | Domingo    | Cortes      |
| Breaking Bad        | 2008          | Drama      | 9.3    | Wyatt      | Skaggs      |
| Breaking Bad        | 2008          | Drama      | 9.9    | Colt       | Steele      |
| Curb Your Enthusiasm| 2000          | Comedy     | 6.5    | Wyatt      | Skaggs      |
| Curb Your Enthusiasm| 2000          | Comedy     | 7.8    | Kimbra     | Masters     |
| Curb Your Enthusiasm| 2000          | Comedy     | 8.8    | Domingo    | Cortes      |
| Curb Your Enthusiasm| 2000          | Comedy     | 8.4    | Wyatt      | Skaggs      |
| Curb Your Enthusiasm| 2000          | Comedy     | 9.1    | Colt       | Steele      |
| Fargo              | 2014          | Drama      | 9.1    | Wyatt      | Skaggs      |
| Fargo              | 2014          | Drama      | 9.7    | Colt       | Steele      |
| Freaks and Geeks   | 1999          | Comedy     | 8.5    | Domingo    | Cortes      |
| Freaks and Geeks   | 1999          | Comedy     | 7.8    | Wyatt      | Skaggs      |
| Freaks and Geeks   | 1999          | Comedy     | 8.8    | Pinkie     | Petit       |
| Freaks and Geeks   | 1999          | Comedy     | 9.3    | Colt       | Steele      |
| General Hospital   | 1963          | Drama      | 5.5    | Wyatt      | Skaggs      |
| General Hospital   | 1963          | Drama      | 6.8    | Kimbra     | Masters     |
| General Hospital   | 1963          | Drama      | 5.8    | Domingo    | Cortes      |
| General Hospital   | 1963          | Drama      | 4.3    | Pinkie     | Petit       |
| General Hospital   | 1963          | Drama      | 4.5    | Colt       | Steele      |
| Halt and Catch Fire| 2014          | Drama      | 9.9    | Colt       | Steele      |
| Seinfeld           | 1989          | Comedy     | 8.0    | Kimbra     | Masters     |
| Seinfeld           | 1989          | Comedy     | 7.2    | Domingo    | Cortes      |
| Stranger Things    | 2016          | Drama      | 8.5    | Wyatt      | Skaggs      |
| Stranger Things    | 2016          | Drama      | 8.9    | Kimbra     | Masters     |
| Stranger Things    | 2016          | Drama      | 8.9    | Domingo    | Cortes      |

## Updateable Views
```mysql
CREATE VIEW ordered_series AS
  SELECT *
  FROM series
  ORDER BY released_year;

SELECT *
FROM ordered_series; 
```
| id  | title                  | released_year | genre     |
|-----|------------------------|---------------|-----------|
| 9   | General Hospital       | 1963          | Drama     |
| 13  | Seinfeld               | 1989          | Comedy    |
| 8   | Freaks and Geeks        | 1999          | Comedy    |
| 6   | Curb Your Enthusiasm    | 2000          | Comedy    |
| 11  | Malcolm In The Middle   | 2000          | Comedy    |
| 2   | Arrested Development    | 2003          | Comedy    |
| 12  | Pushing Daisies         | 2007          | Comedy    |
| 5   | Breaking Bad            | 2008          | Drama     |
| 1   | Archer                  | 2009          | Animation |
| 3   | Bob's Burgers           | 2011          | Animation |
| 4   | Bojack Horseman         | 2014          | Animation |
| 7   | Fargo                   | 2014          | Drama     |
| 10  | Halt and Catch Fire     | 2014          | Drama     |
| 14  | Stranger Things         | 2016          | Drama     |
```mysql
INSERT INTO ordered_series (title, released_year, genre)
VALUES ('The Great', 2020, 'Comedy');

SELECT *
FROM ordered_series;
```
| id  | title                  | released_year | genre     |
|-----|------------------------|---------------|-----------|
| 9   | General Hospital       | 1963          | Drama     |
| 13  | Seinfeld               | 1989          | Comedy    |
| 8   | Freaks and Geeks        | 1999          | Comedy    |
| 6   | Curb Your Enthusiasm    | 2000          | Comedy    |
| 11  | Malcolm In The Middle   | 2000          | Comedy    |
| 2   | Arrested Development    | 2003          | Comedy    |
| 12  | Pushing Daisies         | 2007          | Comedy    |
| 5   | Breaking Bad            | 2008          | Drama     |
| 1   | Archer                  | 2009          | Animation |
| 3   | Bob's Burgers           | 2011          | Animation |
| 4   | Bojack Horseman         | 2014          | Animation |
| 7   | Fargo                   | 2014          | Drama     |
| 10  | Halt and Catch Fire     | 2014          | Drama     |
| 14  | Stranger Things         | 2016          | Drama     |
| 15  | The Great               | 2020          | Comedy    |

## Replacing Views
```mysql
-- If view exists already, replace it
CREATE OR REPLACE VIEW ordered_series AS
  SELECT *
  FROM series
  -- Added descending order
  ORDER BY released_year DESC;

SELECT *
FROM ordered_series;
```
| id  | title                  | released_year | genre     |
|-----|------------------------|---------------|-----------|
| 15  | The Great               | 2020          | Comedy    |
| 14  | Stranger Things         | 2016          | Drama     |
| 4   | Bojack Horseman         | 2014          | Animation |
| 7   | Fargo                   | 2014          | Drama     |
| 10  | Halt and Catch Fire     | 2014          | Drama     |
| 3   | Bob's Burgers           | 2011          | Animation |
| 1   | Archer                  | 2009          | Animation |
| 5   | Breaking Bad            | 2008          | Drama     |
| 12  | Pushing Daisies         | 2007          | Comedy    |
| 2   | Arrested Development    | 2003          | Comedy    |
| 6   | Curb Your Enthusiasm    | 2000          | Comedy    |
| 11  | Malcolm In The Middle   | 2000          | Comedy    |
| 8   | Freaks and Geeks        | 1999          | Comedy    |
| 13  | Seinfeld                | 1989          | Comedy    |
| 9   | General Hospital        | 1963          | Drama     |

## Altering Views
```mysql
-- Change back to ascending order
ALTER VIEW ordered_series AS
  SELECT *
  FROM series
  ORDER BY released_year;

SELECT *
FROM ordered_series;
```
| id  | title                  | released_year | genre     |
|-----|------------------------|---------------|-----------|
| 9   | General Hospital        | 1963          | Drama     |
| 13  | Seinfeld                | 1989          | Comedy    |
| 8   | Freaks and Geeks        | 1999          | Comedy    |
| 6   | Curb Your Enthusiasm    | 2000          | Comedy    |
| 11  | Malcolm In The Middle   | 2000          | Comedy    |
| 2   | Arrested Development    | 2003          | Comedy    |
| 12  | Pushing Daisies         | 2007          | Comedy    |
| 5   | Breaking Bad            | 2008          | Drama     |
| 1   | Archer                  | 2009          | Animation |
| 3   | Bob's Burgers           | 2011          | Animation |
| 4   | Bojack Horseman         | 2014          | Animation |
| 7   | Fargo                   | 2014          | Drama     |
| 10  | Halt and Catch Fire     | 2014          | Drama     |
| 14  | Stranger Things         | 2016          | Drama     |
| 15  | The Great               | 2020          | Comedy    |

## Drop View
```mysql
DROP VIEW ordered_series;

SELECT *
FROM ordered_series;
```
```
> Table 'people.ordered_series' doesn't exist
```
## `HAVING`
- `HAVING` is used to filter records after aggregation has been performed using `GROUP BY`
- Similar to the `WHERE` clause, but the key difference is:
  - `WHERE` filters rows before aggregation
  - `HAVING` filters groups after aggregation
```mysql
SELECT title, 
       AVG(rating),
       COUNT(rating) AS review_count
FROM full_reviews 
GROUP BY title
HAVING COUNT(rating) > 1;
```
| title                 | AVG(rating) | review_count |
|-----------------------|------------|--------------|
| Archer                | 8.12000     | 5            |
| Arrested Development  | 8.08000     | 5            |
| Bob's Burgers         | 7.52000     | 5            |
| Bojack Horseman       | 7.94000     | 5            |
| Breaking Bad          | 9.36000     | 5            |
| Curb Your Enthusiasm  | 8.12000     | 5            |
| Fargo                 | 9.40000     | 2            |
| Freaks and Geeks      | 8.60000     | 4            |
| General Hospital      | 5.38000     | 5            |
| Seinfeld              | 7.60000     | 2            |
| Stranger Things       | 8.76667     | 3            |
## `WITH ROLLUP`
- `WITH ROLLUP` is used to generate subtotals and grand totals when performing aggregation with the `GROUP BY` clause
- Allows hierarchical grouping and provides cumulative totals for each grouping level
```mysql
SELECT  title, AVG(rating)
FROM full_reviews
GROUP BY title WITH ROLLUP;
```
| title                 | AVG(rating) |
|-----------------------|-------------|
| Archer                | 8.12000     |
| Arrested Development  | 8.08000     |
| Bob's Burgers         | 7.52000     |
| Bojack Horseman       | 7.94000     |
| Breaking Bad          | 9.36000     |
| Curb Your Enthusiasm  | 8.12000     |
| Fargo                 | 9.40000     |
| Freaks and Geeks      | 8.60000     |
| General Hospital      | 5.38000     |
| Halt and Catch Fire   | 9.90000     |
| Seinfeld              | 7.60000     |
| Stranger Things       | 8.76667     |
| (NULL)                | 8.02553     |

```mysql
SELECT title, COUNT(rating)
FROM full_reviews
GROUP BY title WITH ROLLUP;
```
| title                | COUNT(rating) |
|----------------------|---------------|
| Archer               | 5             |
| Arrested Development | 5             |
| Bob's Burgers        | 5             |
| Bojack Horseman      | 5             |
| Breaking Bad         | 5             |
| Curb Your Enthusiasm | 5             |
| Fargo                | 2             |
| Freaks and Geeks     | 4             |
| General Hospital     | 5             |
| Halt and Catch Fire  | 1             |
| Seinfeld             | 2             |
| Stranger Things      | 3             |
| (NULL)               | 47            |
```mysql
SELECT first_name, released_year, genre, AVG(rating)
FROM full_reviews
GROUP BY released_year , genre , first_name WITH ROLLUP;
```
| first_name | released_year | genre | AVG(rating) |
|-------------|---------------|-------|-------------|
| Colt        | 1963          | Drama | 4.50000     |
| Domingo     | 1963          | Drama | 5.80000     |
| Kimbra      | 1963          | Drama | 6.80000     |
| Pinkie      | 1963          | Drama | 4.30000     |
| Wyatt       | 1963          | Drama | 5.50000     |
| NULL        | 1963          | Drama | 5.38000     |
| NULL        | 1963          | NULL  | 5.38000     |
| Domingo     | 1989          | Comedy| 7.20000     |
| Kimbra      | 1989          | Comedy| 8.00000     |
| NULL        | 1989          | Comedy| 7.60000     |
| NULL        | 1989          | NULL  | 7.60000     |
| Colt        | 1999          | Comedy| 9.30000     |
| Domingo     | 1999          | Comedy| 8.50000     |
| Pinkie      | 1999          | Comedy| 8.80000     |
| Wyatt       | 1999          | Comedy| 7.80000     |
| NULL        | 1999          | Comedy| 8.60000     |
| NULL        | 1999          | NULL  | 8.60000     |
| Colt        | 2000          | Comedy| 9.10000     |
| Domingo     | 2000          | Comedy| 8.80000     |
| Kimbra      | 2000          | Comedy| 7.80000     |
| Wyatt       | 2000          | Comedy| 7.45000     |
| NULL        | 2000          | Comedy| 8.12000     |
| NULL        | 2000          | NULL  | 8.12000     |
| Colt        | 2003          | Comedy| 9.90000     |
| Domingo     | 2003          | Comedy| 6.00000     |
| Kimbra      | 2003          | Comedy| 8.00000     |
| Pinkie      | 2003          | Comedy| 8.40000     |
| Thomas      | 2003          | Comedy| 8.10000     |
| NULL        | 2003          | Comedy| 8.08000     |
| NULL        | 2003          | NULL  | 8.08000     |
| Colt        | 2008          | Drama | 9.90000     |
| Domingo     | 2008          | Drama | 9.10000     |
| Kimbra      | 2008          | Drama | 9.00000     |
| Thomas      | 2008          | Drama | 9.50000     |
| Wyatt       | 2008          | Drama | 9.30000     |
| NULL        | 2008          | Drama | 9.36000     |
| NULL        | 2008          | NULL  | 9.36000     |
| Colt        | 2009          | Animation | 8.90000 |
| Domingo     | 2009          | Animation | 7.70000 |
| Kimbra      | 2009          | Animation | 8.50000 |
| Thomas      | 2009          | Animation | 8.00000 |
| Wyatt       | 2009          | Animation | 7.50000 |
| NULL        | 2009          | Animation | 8.12000 |
| NULL        | 2009          | NULL  | 8.12000     |
| Colt        | 2011          | Animation | 8.00000 |
| Domingo     | 2011          | Animation | 8.00000 |
| Kimbra      | 2011          | Animation | 7.10000 |
| Pinkie      | 2011          | Animation | 7.50000 |
| Thomas      | 2011          | Animation | 7.00000 |
| NULL        | 2011          | Animation | 7.52000 |
| NULL        | 2011          | NULL  | 7.52000     |
| Colt        | 2014          | Animation | 8.50000 |
| Domingo     | 2014          | Animation | 8.30000 |
| Kimbra      | 2014          | Animation | 7.80000 |
| Thomas      | 2014          | Animation | 7.50000 |
| Wyatt       | 2014          | Animation | 7.60000 |
| NULL        | 2014          | Animation | 7.94000 |
| Colt        | 2014          | Drama | 9.80000     |
| Wyatt       | 2014          | Drama | 9.10000     |
| NULL        | 2014          | Drama | 9.56667     |
| NULL        | 2014          | NULL  | 8.55000     |
| Domingo     | 2016          | Drama | 8.90000     |
| Kimbra      | 2016          | Drama | 8.90000     |
| Wyatt       | 2016          | Drama | 8.50000     |
| NULL        | 2016          | Drama | 8.76667     |
| NULL        | 2016          | NULL  | 8.76667     |
| NULL        | NULL          | NULL  | 8.02553     |
## SQL Modes Basics
- Configurations that affect the SQL syntax and data handling behavior of the database
- Help control how MySQL handles certain operations such as invalid values, missing data, strictness of constraints, and compatibility with SQL standards
```mysql
-- To View Modes:
SELECT @@GLOBAL.sql_mode; -- apply globally to all db connections
SELECT @@SESSION.sql_mode; -- apply to current session specific to db connection
 
-- To Set Them:
SET GLOBAL sql_mode = 'modes'; -- changes for all new connections (not current active)
SET SESSION sql_mode = 'modes'; -- changes for only current session
```
## `STRICT_TRANS_TABLES`
- Enforces strict handling of invalid or missing values in transactional tables, while allowing non-transactional tables to use default values when invalid data is provided
```mysql
-- Check current SQL mode
SELECT @@sql_mode;

-- Enable for current session
SET SESSION sql_mode = 'STRICT_TRANS_TABLES';

-- Enable for global configuration
SET GLOBAL sql_mode = 'STRICT_TRANS_TABLES';
```
