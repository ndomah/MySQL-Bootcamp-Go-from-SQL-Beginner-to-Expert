# Many to Many
## Basics
- A **many-to-many (M:N)** relationship in a relational database occurs when multiple records in one table are related to multiple records in another table
- This type of relationship cannot be directly implemented with only two tables; instead, an **intermediate (junction) table** is required to establish the relationship.

![m:n](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/12.%20Many%20to%20Many/image.png)
## Creating our Many to Many Tables
```mysql
CREATE TABLE reviewers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL
);
 
CREATE TABLE series (
    id INT PRIMARY KEY AUTO_INCREMENT,
    title VARCHAR(100),
    released_year YEAR,
    genre VARCHAR(100)
);
 
CREATE TABLE reviews (
    id INT PRIMARY KEY AUTO_INCREMENT,
    rating DECIMAL(2 , 1 ),
    series_id INT,
    reviewer_id INT,
    FOREIGN KEY (series_id)
        REFERENCES series (id),
    FOREIGN KEY (reviewer_id)
        REFERENCES reviewers (id)
);
 
INSERT INTO series (title, released_year, genre) VALUES
    ('Archer', 2009, 'Animation'),
    ('Arrested Development', 2003, 'Comedy'),
    ('Bob\'s Burgers', 2011, 'Animation'),
    ('Bojack Horseman', 2014, 'Animation'),
    ('Breaking Bad', 2008, 'Drama'),
    ('Curb Your Enthusiasm', 2000, 'Comedy'),
    ('Fargo', 2014, 'Drama'),
    ('Freaks and Geeks', 1999, 'Comedy'),
    ('General Hospital', 1963, 'Drama'),
    ('Halt and Catch Fire', 2014, 'Drama'),
    ('Malcolm In The Middle', 2000, 'Comedy'),
    ('Pushing Daisies', 2007, 'Comedy'),
    ('Seinfeld', 1989, 'Comedy'),
    ('Stranger Things', 2016, 'Drama');
  
INSERT INTO reviewers (first_name, last_name) VALUES
    ('Thomas', 'Stoneman'),
    ('Wyatt', 'Skaggs'),
    ('Kimbra', 'Masters'),
    ('Domingo', 'Cortes'),
    ('Colt', 'Steele'),
    ('Pinkie', 'Petit'),
    ('Marlon', 'Crafford');
    
INSERT INTO reviews(series_id, reviewer_id, rating) VALUES
    (1,1,8.0),(1,2,7.5),(1,3,8.5),(1,4,7.7),(1,5,8.9),
    (2,1,8.1),(2,4,6.0),(2,3,8.0),(2,6,8.4),(2,5,9.9),
    (3,1,7.0),(3,6,7.5),(3,4,8.0),(3,3,7.1),(3,5,8.0),
    (4,1,7.5),(4,3,7.8),(4,4,8.3),(4,2,7.6),(4,5,8.5),
    (5,1,9.5),(5,3,9.0),(5,4,9.1),(5,2,9.3),(5,5,9.9),
    (6,2,6.5),(6,3,7.8),(6,4,8.8),(6,2,8.4),(6,5,9.1),
    (7,2,9.1),(7,5,9.7),
    (8,4,8.5),(8,2,7.8),(8,6,8.8),(8,5,9.3),
    (9,2,5.5),(9,3,6.8),(9,4,5.8),(9,6,4.3),(9,5,4.5),
    (10,5,9.9),
    (13,3,8.0),(13,4,7.2),
    (14,2,8.5),(14,3,8.9),(14,4,8.9);
```
## TV Series Challenge 1
- Print this:

| title               | rating |
|-------------------- |--------|
| Archer              | 8.0    |
| Archer              | 7.5    |
| Archer              | 8.5    |
| Archer              | 7.7    |
| Archer              | 8.9    |
| Arrested Development| 8.1    |
| Arrested Development| 6.0    |
| Arrested Development| 8.0    |
| Arrested Development| 8.4    |
| Arrested Development| 9.9    |
| Bob's Burgers       | 7.0    |
| Bob's Burgers       | 7.5    |
| Bob's Burgers       | 8.0    |
| Bob's Burgers       | 7.1    |
| Bob's Burgers       | 8.0    |
```mysql
SELECT title, rating
FROM series s
JOIN reviews r
  ON s.id = r.series_id;
```
## TV Series Challenge 2
- Print this:

| title                  | avg_rating |
|------------------------|------------|
| General Hospital       | 5.38000     |
| Bob's Burgers          | 7.52000     |
| Seinfeld               | 7.60000     |
| Bojack Horseman        | 7.94000     |
| Arrested Development   | 8.08000     |
| Curb Your Enthusiasm   | 8.12000     |
| Archer                 | 8.12000     |
| Freaks and Geeks       | 8.60000     |
| Stranger Things        | 8.76667     |
| Breaking Bad           | 9.36000     |
| Fargo                  | 9.40000     |
| Halt and Catch Fire    | 9.90000     |
```mysql
SELECT title,
       ROUND(AVG(rating), 2) AS avg_rating
FROM series s
JOIN reviews r
  ON s.id = r.series_id
GROUP BY title
ORDER BY avg_rating;
```
## TV Series Challenge 3
- Print this:

| first_name | last_name | rating |
|------------|-----------|--------|
| Thomas     | Stoneman  | 8.0    |
| Thomas     | Stoneman  | 8.1    |
| Thomas     | Stoneman  | 7.0    |
| Thomas     | Stoneman  | 7.5    |
| Thomas     | Stoneman  | 9.5    |
| Wyatt      | Skaggs    | 7.5    |
| Wyatt      | Skaggs    | 7.6    |
| Wyatt      | Skaggs    | 9.3    |
| Wyatt      | Skaggs    | 6.5    |
| Wyatt      | Skaggs    | 8.4    |
| Wyatt      | Skaggs    | 9.1    |
| Wyatt      | Skaggs    | 7.8    |
| Wyatt      | Skaggs    | 5.5    |
| Wyatt      | Skaggs    | 8.5    |
| Kimbra     | Masters   | 8.5    |
| Kimbra     | Masters   | 8.0    |
| Kimbra     | Masters   | 7.1    |
| Kimbra     | Masters   | 7.8    |
| Kimbra     | Masters   | 9.0    |
| Kimbra     | Masters   | 7.8    |
```mysql
SELECT first_name, last_name, rating
FROM reviewers r1
JOIN reviews r2
  ON r2.reviewer_id = r1.id;
```
## TV Series Challenge 4
- Print this:

| unreviewed_series       |
|-------------------------|
| Malcolm In The Middle   |
| Pushing Daisies         |
```mysql
-- Left Join
SELECT title AS unreviewed_series
FROM series s
LEFT JOIN reviews r
  ON s.id = r.series_id
WHERE rating IS NULL;

-- Right Join
SELECT title AS unreviewed_series
FROM reviews r
RIGHT JOIN series s
  ON s.id = r.series_id
WHERE rating IS NULL;
```
## TV Series Challenge 5
- Print this:

| genre      | avg_rating |
|------------|------------|
| Animation  | 7.86000    |
| Comedy     | 8.16250    |
| Drama      | 8.04375    |
```mysql
SELECT genre,
       ROUND(AVG(rating), 2) AS avg_rating
FROM series s
JOIN reviews r
  ON s.id = r.series_id
GROUP BY genre;
```
## TV Series Challenge 6
- Print this:

| first_name | last_name | COUNT | MIN  | MAX  | AVG     | STATUS   |
|------------|-----------|-------|------|------|---------|----------|
| Thomas     | Stoneman  | 5     | 7.0  | 9.5  | 8.02000  | ACTIVE   |
| Wyatt      | Skaggs    | 9     | 5.5  | 9.3  | 7.80000  | ACTIVE   |
| Kimbra     | Masters   | 9     | 6.8  | 9.0  | 7.98889  | ACTIVE   |
| Domingo    | Cortes    | 10    | 5.8  | 9.1  | 7.83000  | ACTIVE   |
| Colt       | Steele    | 10    | 4.5  | 9.9  | 8.77000  | ACTIVE   |
| Pinkie     | Petit     | 4     | 4.3  | 8.8  | 7.25000  | ACTIVE   |
| Marlon     | Crafford  | 0     | 0.0  | 0.0  | 0.00000  | INACTIVE |
```mysql
-- Using CASE
SELECT first_name,
       last_name,
       COUNT(rating) AS count,
       IFNULL(MIN(rating), 0) AS min,
       IFNULL(MAX(rating), 0) AS max,
       ROUND(IFNULL(AVG(rating), 0), 2) AS average,
       CASE
          WHEN COUNT(rating) >= 10 THEN 'POWERUSER'
          WHEN COUNT(rating) > 0 THEN 'ACTIVE'
          ELSE 'INACTIVE'
       END AS status
FROM reviewers r1
LEFT JOIN reviews r2
  ON r1.id = r2.reviewer_id
GROUP BY first_name , last_name;

-- Using IF
SELECT first_name,
       last_name,
       COUNT(rating) AS count,
       IFNULL(MIN(rating), 0) AS min,
       IFNULL(MAX(rating), 0) AS max,
       ROUND(IFNULL(AVG(rating), 0), 2) AS average,
       IF(COUNT(rating) > 0, 'ACTIVE', 'INACTIVE') AS status
FROM reviewers r1
LEFT JOIN reviews r2
  ON r1.id = r2.reviewer_id
GROUP BY first_name , last_name;
```
## TV Series Challenge 7
- Print this:

| title               | rating | reviewer          |
|--------------------|--------|------------------|
| Archer             | 8.0    | Thomas Stoneman   |
| Archer             | 7.7    | Domingo Cortes    |
| Archer             | 8.5    | Kimbra Masters    |
| Archer             | 7.5    | Wyatt Skaggs      |
| Archer             | 8.9    | Colt Steele       |
| Arrested Development | 8.4  | Pinkie Petit      |
| Arrested Development | 9.9  | Colt Steele       |
| Arrested Development | 8.1  | Thomas Stoneman   |
| Arrested Development | 6.0  | Domingo Cortes    |
| Arrested Development | 8.0  | Kimbra Masters    |
| Bob's Burgers      | 7.0    | Thomas Stoneman   |
| Bob's Burgers      | 8.0    | Domingo Cortes    |
| Bob's Burgers      | 7.1    | Kimbra Masters    |
| Bob's Burgers      | 7.5    | Pinkie Petit      |
| Bob's Burgers      | 8.0    | Colt Steele       |
```mysql
SELECT title,
       rating,
       CONCAT(first_name, ' ', last_name) AS reviewer
FROM reviews r1
INNER JOIN series s
  ON r1.series_id = s.id
INNER JOIN reviewers r2
  ON r1.reviewer_id = r2.id;
```
