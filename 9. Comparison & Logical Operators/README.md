# Comparison & Logical Operators
## Not Equal
```mysql
SELECT *
FROM books
WHERE released_year != 2017;
```
| book_id | title                                         | author_fname | author_lname    | released_year | stock_quantity | pages |
|---------|-----------------------------------------------|--------------|----------------|---------------|----------------|-------|
| 1       | The Namesake                                  | Jhumpa       | Lahiri         | 2003          | 32             | 291   |
| 2       | Norse Mythology                               | Neil         | Gaiman         | 2016          | 43             | 304   |
| 3       | American Gods                                 | Neil         | Gaiman         | 2001          | 12             | 465   |
| 4       | Interpreter of Maladies                      | Jhumpa       | Lahiri         | 1996          | 97             | 198   |
| 5       | A Hologram for the King: A Novel             | Dave         | Eggers         | 2012          | 154            | 352   |
| 6       | The Circle                                    | Dave         | Eggers         | 2013          | 26             | 504   |
| 7       | The Amazing Adventures of Kavalier & Clay    | Michael      | Chabon         | 2000          | 68             | 634   |
| 8       | Just Kids                                     | Patti        | Smith          | 2010          | 55             | 304   |
| 9       | A Heartbreaking Work of Staggering Genius    | Dave         | Eggers         | 2001          | 104            | 437   |
| 10      | Coraline                                      | Neil         | Gaiman         | 2003          | 100            | 208   |
| 11      | What We Talk About When We Talk About Love   | Raymond      | Carver         | 1981          | 23             | 176   |
| 12      | Where I'm Calling From: Selected Stories     | Raymond      | Carver         | 1989          | 12             | 526   |
| 13      | White Noise                                   | Don          | DeLillo        | 1985          | 49             | 320   |
| 14      | Cannery Row                                   | John         | Steinbeck      | 1945          | 95             | 181   |
| 15      | Oblivion: Stories                             | David        | Foster Wallace | 2004          | 172            | 329   |
| 16      | Consider the Lobster                         | David        | Foster Wallace | 2005          | 92             | 343   |
| 17      | 10% Happier                                   | Dan          | Harris         | 2014          | 29             | 256   |
| 18      | fake_book                                     | Freida       | Harris         | 2001          | 287            | 428   |
## `NOT LIKE`
```mysql
SELECT *
FROM books
WHERE title NOT LIKE '%e%';
```
| book_id | title      | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|-----------|--------------|--------------|---------------|----------------|-------|
| 8       | Just Kids | Patti        | Smith        | 2010          | 55             | 304   |
## Greater Than
```mysql
SELECT *
FROM books
WHERE released_year > 2005;
```
| book_id | title                            | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|----------------------------------|--------------|--------------|---------------|----------------|-------|
| 2       | Norse Mythology                   | Neil         | Gaiman       | 2016          | 43             | 304   |
| 5       | A Hologram for the King: A Novel  | Dave         | Eggers       | 2012          | 154            | 352   |
| 6       | The Circle                        | Dave         | Eggers       | 2013          | 26             | 504   |
| 8       | Just Kids                         | Patti        | Smith        | 2010          | 55             | 304   |
| 17      | 10% Happier                        | Dan          | Harris       | 2014          | 29             | 256   |
| 19      | Lincoln In The Bardo              | George       | Saunders     | 2017          | 1000           | 367   |
```mysql
SELECT *
FROM books
WHERE pages > 500;
```
| book_id | title                                      | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|--------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 6       | The Circle                                 | Dave         | Eggers       | 2013          | 26             | 504   |
| 7       | The Amazing Adventures of Kavalier & Clay  | Michael      | Chabon       | 2000          | 68             | 634   |
| 12      | Where I'm Calling From: Selected Stories  | Raymond      | Carver       | 1989          | 12             | 526   |
## Less Than or Equal To
```mysql
SELECT *
FROM books
WHERE pages < 200;
```
| book_id | title                                      | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|--------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 4       | Interpreter of Maladies                   | Jhumpa       | Lahiri       | 1996          | 97             | 198   |
| 11      | What We Talk About When We Talk About Love: Stories | Raymond  | Carver       | 1981          | 23             | 176   |
| 14      | Cannery Row                                | John         | Steinbeck    | 1945          | 95             | 181   |
```mysql
SELECT *
FROM books
WHERE released_year <= 1985;
```
| book_id | title                                      | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|--------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 11      | What We Talk About When We Talk About Love: Stories | Raymond  | Carver       | 1981          | 23             | 176   |
| 13      | White Noise                                | Don          | DeLillo      | 1985          | 49             | 320   |
| 14      | Cannery Row                                | John         | Steinbeck    | 1945          | 95             | 181   |
## Logical `AND`
```mysql
SELECT title, author_lname, released_year
FROM books
WHERE released_year > 2010
  AND author_lname = 'Eggers'
  AND title LIKE '%novel%';
```
| title                                 | author_lname | released_year |
|---------------------------------------|--------------|---------------|
| A Hologram for the King: A Novel      | Eggers       | 2012          |
## Logical `OR`
```mysql
SELECT title, author_lname, released_year
FROM books
WHERE author_lname='Eggers'
  OR released_year > 2010;
```
| title                                      | author_lname | released_year |
|--------------------------------------------|--------------|---------------|
| Norse Mythology                             | Gaiman       | 2016          |
| A Hologram for the King: A Novel            | Eggers       | 2012          |
| The Circle                                  | Eggers       | 2013          |
| A Heartbreaking Work of Staggering Genius   | Eggers       | 2001          |
| 10% Happier                                 | Harris       | 2014          |
| Lincoln In The Bardo                        | Saunders     | 2017          |
## `BETWEEN`
```mysql
SELECT title, released_year
FROM books
WHERE released_year BETWEEN 2004 AND 2014;
```
| title                                 | released_year |
|---------------------------------------|---------------|
| A Hologram for the King: A Novel      | 2012          |
| The Circle                            | 2013          |
| Just Kids                             | 2010          |
| Oblivion: Stories                      | 2004          |
| Consider the Lobster                   | 2005          |
| 10% Happier                            | 2014          |
## Comparing Dates
```mysql
SELECT * FROM people
WHERE birthtime BETWEEN CAST('09:00:00' AS TIME) AND CAST('18:00:00' AS TIME);

-- can also be written as
SELECT *
FROM people
WHERE HOUR(birthtime) BETWEEN 12 AND 16;
```
| name  | birthdate  | birthtime | birthdt             |
|-------|------------|-----------|---------------------|
| Elton | 2000-12-25  | 11:00:00   | 2000-12-25 11:00:00 |
| Lulu  | 1985-04-11  | 09:45:10   | 1985-04-11 09:45:10 |
## The `IN` Operator
```mysql
SELECT title, author_lname
FROM books
WHERE author_lname IN ('Carver', 'Lahiri', 'Smith');
```
| title                                             | author_lname |
|--------------------------------------------------|--------------|
| The Namesake                                     | Lahiri       |
| Interpreter of Maladies                          | Lahiri       |
| Just Kids                                        | Smith        |
| What We Talk About When We Talk About Love: Stories | Carver    |
| Where I'm Calling From: Selected Stories         | Carver       |
```mysql
SELECT title, author_lname
FROM books
WHERE author_lname NOT IN ('Carver', 'Lahiri', 'Smith');
```
| title                                      | author_lname    |
|--------------------------------------------|-----------------|
| Norse Mythology                             | Gaiman          |
| American Gods                               | Gaiman          |
| A Hologram for the King: A Novel            | Eggers          |
| The Circle                                  | Eggers          |
| The Amazing Adventures of Kavalier & Clay   | Chabon          |
| A Heartbreaking Work of Staggering Genius   | Eggers          |
| Coraline                                    | Gaiman          |
| White Noise                                 | DeLillo         |
| Cannery Row                                 | Steinbeck       |
| Oblivion: Stories                           | Foster Wallace  |
| Consider the Lobster                        | Foster Wallace  |
| 10% Happier                                 | Harris          |
| fake_book                                   | Harris          |
| Lincoln In The Bardo                        | Saunders        |
## `CASE`
```mysql
SELECT title,
       stock_quantity,
       CASE
          WHEN stock_quantity <= 40 THEN '*'
          WHEN stock_quantity <= 70 THEN '**'
          WHEN stock_quantity <= 100 THEN '***'
          WHEN stock_quantity <= 140 THEN '****'
          ELSE '*****'
       END AS stock
FROM books;
```
| title                                      | stock_quantity | stock  |
|--------------------------------------------|----------------|--------|
| The Namesake                               | 32             | *      |
| Norse Mythology                            | 43             | **     |
| American Gods                              | 12             | *      |
| Interpreter of Maladies                    | 97             | ***    |
| A Hologram for the King: A Novel            | 154            | *****  |
| The Circle                                 | 26             | *      |
| The Amazing Adventures of Kavalier & Clay  | 68             | **     |
| Just Kids                                  | 55             | **     |
| A Heartbreaking Work of Staggering Genius  | 104            | ****   |
| Coraline                                   | 100            | ***    |
| What We Talk About When We Talk About Love: Stories | 23     | *      |
| Where I'm Calling From: Selected Stories   | 12             | *      |
| White Noise                                | 49             | **     |
| Cannery Row                                | 95             | ***    |
| Oblivion: Stories                          | 172            | *****  |
| Consider the Lobster                       | 92             | ***    |
| 10% Happier                                | 29             | *      |
| fake_book                                  | 287            | *****  |
| Lincoln In The Bardo                       | 1000           | *****  |
## `IS NULL`
```mysql
/*
- finds NULL values in author last name column
- nothing will return because our table doesn't have null values
*/
SELECT *
FROM books
WHERE author_lname IS NULL;
```
## Exercise
- Evaluate the following:
```mysql
SELECT 10 != 10;
-- 0

SELECT 15 > 14 AND 99 - 5 <= 94;
-- 1

SELECT 1 IN (5,3) OR 9 BETWEEN 8 AND 10;
-- 1
```
- Select all books written before 1980 (non-inclusive)
```mysql
SELECT *
FROM books
WHERE released_year < 1980;
```
| book_id | title       | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|------------|--------------|--------------|---------------|----------------|-------|
| 14      | Cannery Row | John         | Steinbeck    | 1945          | 95             | 181   |
- Seelct all books written by Eggers or Chabon
```mysql
SELECT *
FROM books
WHERE author_lname IN ('Eggers', 'Chabon');
```
| book_id | title                                      | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|--------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 5       | A Hologram for the King: A Novel           | Dave         | Eggers       | 2012          | 154            | 352   |
| 6       | The Circle                                 | Dave         | Eggers       | 2013          | 26             | 504   |
| 7       | The Amazing Adventures of Kavalier & Clay  | Michael      | Chabon       | 2000          | 68             | 634   |
| 9       | A Heartbreaking Work of Staggering Genius  | Dave         | Eggers       | 2001          | 104            | 437   |
- Select all books written by Lahiri, published after 2000
```mysql
SELECT *
FROM books
WHERE author_lname = 'Lahiri' AND released_year > 2000;
```
| book_id | title        | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|-------------|--------------|--------------|---------------|----------------|-------|
| 1       | The Namesake | Jhumpa       | Lahiri       | 2003          | 32             | 291   |
- Select all books with page counts between 100 and 200
```mysql
SELECT *
FROM books
WHERE pages BETWEEN 100 and 200;
```
| book_id | title                                             | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|-------------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 4       | Interpreter of Maladies                          | Jhumpa       | Lahiri       | 1996          | 97             | 198   |
| 11      | What We Talk About When We Talk About Love: Stories | Raymond  | Carver       | 1981          | 23             | 176   |
| 14      | Cannery Row                                      | John         | Steinbeck    | 1945          | 95             | 181   |
- Select all books where author_lname starts with a 'C' or an 'S'
```mysql
SELECT *
FROM books
WHERE author_lname LIKE 'C%'
   OR author_lname LIKE 'S%'; 
```
| book_id | title                                             | author_fname | author_lname | released_year | stock_quantity | pages |
|---------|-------------------------------------------------|--------------|--------------|---------------|----------------|-------|
| 7       | The Amazing Adventures of Kavalier & Clay        | Michael      | Chabon       | 2000          | 68             | 634   |
| 8       | Just Kids                                        | Patti        | Smith        | 2010          | 55             | 304   |
| 11      | What We Talk About When We Talk About Love: Stories | Raymond  | Carver       | 1981          | 23             | 176   |
| 12      | Where I'm Calling From: Selected Stories         | Raymond      | Carver       | 1989          | 12             | 526   |
| 14      | Cannery Row                                      | John         | Steinbeck    | 1945          | 95             | 181   |
| 19      | Lincoln In The Bardo                             | George       | Saunders     | 2017          | 1000           | 367   |
- Output the following table
  - If title contains 'stories' label as Short Stories
  - The books *Just Kids* and *A Heartbreaking Work of Staggering Genius* should be labeled as Memoirs
  - Everything else should be a Novel
 ```mysql
SELECT title, author_lname,
  CASE
    WHEN title LIKE '%stories%' THEN 'Short Stories'
    WHEN title = 'Just Kids' THEN 'Memoir'
    WHEN title = 'A Heartbreaking Work of Staggering Genius' THEN 'Memoir'
    ELSE 'Novel'
  END AS type
FROM books;
```
| title                                         | author_lname    | type          |
|-----------------------------------------------|-----------------|---------------|
| The Namesake                                  | Lahiri          | Novel         |
| Norse Mythology                               | Gaiman          | Novel         |
| American Gods                                 | Gaiman          | Novel         |
| Interpreter of Maladies                       | Lahiri          | Novel         |
| A Hologram for the King: A Novel              | Eggers          | Novel         |
| The Circle                                    | Eggers          | Novel         |
| The Amazing Adventures of Kavalier & Clay     | Chabon          | Novel         |
| Just Kids                                     | Smith           | Memoir        |
| A Heartbreaking Work of Staggering Genius     | Eggers          | Memoir         |
| Coraline                                      | Gaiman          | Novel         |
| What We Talk About When We Talk About Love    | Carver          | Short Stories |
| Where I'm Calling From: Selected Stories      | Carver          | Short Stories |
| White Noise                                   | DeLillo         | Novel         |
| Cannery Row                                   | Steinbeck       | Novel         |
| Oblivion: Stories                             | Foster Wallace  | Short Stories |
| Consider the Lobster                          | Foster Wallace  | Novel         |
| 10% Happier                                   | Harris          | Novel         |
| fake_book                                     | Harris          | Novel         |
| Lincoln In The Bardo                          | Saunders        | Novel         |
- Output a table that includes the author's last name, first name, and how many books they wrote
```mysql
SELECT author_fname, author_lname,
  CASE
    WHEN COUNT(*) = 1 THEN '1 book'
    ELSE CONCAT(COUNT(*), ' books')
  END AS count
FROM books
GROUP BY author_fname, author_lname;
```
| author_fname | author_lname    | count   |
|--------------|----------------|---------|
| Jhumpa       | Lahiri          | 2 books |
| Neil         | Gaiman          | 3 books |
| Dave         | Eggers          | 3 books |
| Michael      | Chabon          | 1 book  |
| Patti        | Smith           | 1 book  |
| Raymond      | Carver          | 2 books |
| Don          | DeLillo         | 1 book  |
| John         | Steinbeck       | 1 book  |
| David        | Foster Wallace  | 2 books |
| Dan          | Harris          | 1 book  |
| Freida       | Harris          | 1 book  |
| George       | Saunders        | 1 book  |
