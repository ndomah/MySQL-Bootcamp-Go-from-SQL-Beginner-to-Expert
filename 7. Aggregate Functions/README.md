# Aggregate Functions
## `COUNT` Basics
- Counts rows
```mysql
SELECT COUNT(*)
FROM books;
```
| COUNT(*) |
|----------|
|    19    |
```mysql
SELECT COUNT(author_lname)
FROM books;
```
| COUNT(author_lname) |
|--------------------|
| 19                 |
```mysql
SELECT COUNT(DISTINCT author_lname)
FROM books;
```
| COUNT(DISTINCT author_lname) |
|-----------------------------|
| 11                          |
```mysql
SELECT COUNT(*)
FROM books
WHERE title LIKE '%the%';
```
| COUNT(*) |
|----------|
| 6        |
## `GROUP BY`
- Summarizes or aggregates idential data into single rows
```mysql
SELECT author_lname,
       COUNT(*) 
FROM books
GROUP BY author_lname;
```
| author_lname    | COUNT(*) |
|----------------|----------|
| Lahiri         | 2        |
| Gaiman         | 3        |
| Eggers         | 3        |
| Chabon         | 1        |
| Smith          | 1        |
| Carver         | 2        |
| DeLillo        | 1        |
| Steinbeck      | 1        |
| Foster Wallace | 2        |
| Harris         | 2        |
| Saunders       | 1        |
```mysql
SELECT author_lname,
       COUNT(*) AS books_written
FROM books
GROUP BY author_lname
ORDER BY books_written DESC;
```
| author_lname    | books_written |
|----------------|---------------|
| Gaiman         | 3             |
| Eggers         | 3             |
| Lahiri         | 2             |
| Carver         | 2             |
| Foster Wallace | 2             |
| Harris         | 2             |
| Chabon         | 1             |
| Smith          | 1             |
| DeLillo        | 1             |
| Steinbeck      | 1             |
| Saunders       | 1             |
## `MIN` and `MAX`
```mysql
SELECT MAX(pages)
FROM books;
```
| MAX(pages) |
|------------|
| 634        |
```mysql
SELECT MIN(author_lname)
FROM books;
```
| MIN(author_lname) |
|------------------|
| Carver           |
## Subqueries
- Let's say we wanted to find the longest book
- We previously learned we can do this:
```mysql
SELECT title, pages
FROM books
ORDER BY pages
LIMIT 1;
```
- We can use subqueries instead
```mysql
SELECT title, pages
FROM books
WHERE pages = (SELECT MAX(pages)
               FROM books);
```
| title                                       | pages |
|---------------------------------------------|-------|
| The Amazing Adventures of Kavalier & Clay   |  634  |
- Find the most recently released book
```mysql
-- Find most recent year
SELECT MIN(released_year)
FROM books;

-- Integrate as subquery
SELECT title, released_year
FROM books 
WHERE released_year = (SELECT MIN(released_year)
                       FROM books);
```
| title        | released_year |
|--------------|---------------|
| Cannery Row  | 1945          |
## Grouping By Multiple Columns
- Count occurences of author names in table
```mysql
SELECT author_fname, author_lname, COUNT(*) 
FROM books 
GROUP BY author_lname, author_fname;
```
| author_fname | author_lname    | COUNT(*) |
|--------------|----------------|----------|
| Jhumpa       | Lahiri          | 2        |
| Neil         | Gaiman          | 3        |
| Dave         | Eggers          | 3        |
| Michael      | Chabon          | 1        |
| Patti        | Smith           | 1        |
| Raymond      | Carver          | 2        |
| Don          | DeLillo         | 1        |
| John         | Steinbeck       | 1        |
| David        | Foster Wallace  | 2        |
| Dan          | Harris          | 1        |
| Freida       | Harris          | 1        |
| George       | Saunders        | 1        |
- Count number of books each author wrote
```mysql
SELECT CONCAT(author_fname, ' ', author_lname) AS author,
       COUNT(*)
FROM books
GROUP BY author;
```
| author                | COUNT(*) |
|-----------------------|----------|
| Jhumpa Lahiri         | 2        |
| Neil Gaiman           | 3        |
| Dave Eggers           | 3        |
| Michael Chabon        | 1        |
| Patti Smith           | 1        |
| Raymond Carver        | 2        |
| Don DeLillo           | 1        |
| John Steinbeck        | 1        |
| David Foster Wallace  | 2        |
| Dan Harris            | 1        |
| Freida Harris         | 1        |
| George Saunders       | 1        |
## `MIN` and `MAX` with `GROUP BY`
- Find the earliest release year for each author
```mysql
SELECT author_lname,
       MIN(released_year)
FROM books
GROUP BY author_lname;
```
| author_lname   |   min_released_year |
|----------------|---------------------|
| Carver         |                1981 |
| Chabon         |                2000 |
| DeLillo        |                1985 |
| Eggers         |                2001 |
| Foster Wallace |                2004 |
| Gaiman         |                2001 |
| Harris         |                2001 |
| Lahiri         |                1996 |
| Saunders       |                2017 |
| Steinbeck      |                1945 |
- Find the earliest and latest release year for each author
```mysql
SELECT author_lname,
       MAX(released_year),
       MIN(released_year)
FROM books
GROUP BY author_lname;
```
| author_lname   |   max_released_year |   min_released_year |
|----------------|---------------------|---------------------|
| Carver         |                1989 |                1981 |
| Chabon         |                2000 |                2000 |
| DeLillo        |                1985 |                1985 |
| Eggers         |                2013 |                2001 |
| Foster Wallace |                2005 |                2004 |
| Gaiman         |                2016 |                2001 |
| Harris         |                2014 |                2001 |
| Lahiri         |                2003 |                1996 |
| Saunders       |                2017 |                2017 |
| Steinbeck      |                1945 |                1945 |
- For each author last name, find the number of books they wrote, the earliest and latest release year, and the page count of thier longest book.
```mysql
SELECT author_lname, 
	COUNT(*) as books_written, 
	MAX(released_year) AS latest_release,
	MIN(released_year)  AS earliest_release,
       MAX(pages) AS longest_page_count
FROM books
GROUP BY author_lname;
```
| author_lname   |   books_written |   latest_release |   earliest_release |   longest_page_count |
|----------------|-----------------|------------------|--------------------|----------------------|
| Carver         |               2 |             1989 |               1981 |                  526 |
| Chabon         |               1 |             2000 |               2000 |                  634 |
| DeLillo        |               1 |             1985 |               1985 |                  320 |
| Eggers         |               3 |             2013 |               2001 |                  504 |
| Foster Wallace |               2 |             2005 |               2004 |                  343 |
| Gaiman         |               3 |             2016 |               2001 |                  465 |
| Harris         |               2 |             2014 |               2001 |                  428 |
| Lahiri         |               2 |             2003 |               1996 |                  291 |
| Saunders       |               1 |             2017 |               2017 |                  367 |
| Steinbeck      |               1 |             1945 |               1945 |                  181 |
- Do the same as before, but account for the fact that some authors have the same last name
```mysql
SELECT author_lname, 
       author_fname,
	COUNT(*) as books_written, 
	MAX(released_year) AS latest_release,
	MIN(released_year)  AS earliest_release
FROM books
GROUP BY author_lname, author_fname;
```
| author_lname   | author_fname   |   books_written |   latest_release |   earliest_release |
|----------------|---------------|-----------------|------------------|--------------------|
| Carver         | Raymond        |               2 |             1989 |               1981 |
| Chabon         | Michael        |               1 |             2000 |               2000 |
| DeLillo        | Don            |               1 |             1985 |               1985 |
| Eggers         | Dave           |               3 |             2013 |               2001 |
| Foster Wallace | David          |               2 |             2005 |               2004 |
| Gaiman         | Neil           |               3 |             2016 |               2001 |
| Harris         | Dan            |               1 |             2014 |               2014 |
| Harris         | Freida         |               1 |             2001 |               2001 |
| Lahiri         | Jhumpa         |               2 |             2003 |               1996 |
| Saunders       | George         |               1 |             2017 |               2017 |
| Steinbeck      | John           |               1 |             1945 |               1945 |
## `SUM`
- Add things together
- Find the total page count for all books
```mysql
SELECT SUM(pages)
FROM books;
```
| SUM(pages) |
|------------|
| 6623       |
- For each author's last name, find how many books they wrote and their total page count
```mysql
SELECT author_lname,
       COUNT(*),
       SUM(pages)
FROM books
GROUP BY author_lname;
```
| author_lname   |   books_written |   total_pages |
|----------------|-----------------|---------------|
| Carver         |               2 |           702 |
| Chabon         |               1 |           634 |
| DeLillo        |               1 |           320 |
| Eggers         |               3 |          1293 |
| Foster Wallace |               2 |           672 |
| Gaiman         |               3 |           977 |
| Harris         |               2 |           684 |
| Lahiri         |               2 |           489 |
| Saunders       |               1 |           367 |
| Steinbeck      |               1 |           181 |
## `AVG`
- Calculate averages
- Find the average number of pages across all books
```mysql
SELECT AVG(pages)
FROM books;
```
| AVG(pages)  |
|-------------|
| 348.58      |
- Find the average publication year
```mysql
SELECT AVG(released_year)
FROM books;
```
- Find the averate stock quantity and number of books published per year
```mysql
SELECT released_year, 
      AVG(stock_quantity), 
      COUNT(*)
FROM books
GROUP BY released_year;
```
|   released_year |   avg_stock_quantity |   book_count |
|----------------|----------------------|--------------|
|            1945 |                95.00 |            1 |
|            1981 |                23.00 |            1 |
|            1985 |                49.00 |            1 |
|            1989 |                12.00 |            1 |
|            1996 |                97.00 |            1 |
|            2000 |                68.00 |            1 |
|            2001 |               134.33 |            3 |
|            2003 |                66.00 |            2 |
|            2004 |               172.00 |            1 |
|            2005 |                92.00 |            1 |
|            2010 |                55.00 |            1 |
|            2012 |               154.00 |            1 |
|            2013 |                26.00 |            1 |
|            2014 |                29.00 |            1 |
|            2016 |                43.00 |            1 |
|            2017 |              1000.00 |            1 |
## More Aggregate Functions
- Refer to the [MySQL Aggregate Functions Docs](https://dev.mysql.com/doc/refman/8.4/en/aggregate-functions.html) for more functions
## Aggregate Functions Exercises
- Print the number of books in the database
```mysql
SELECT COUNT(*)
FROM books;
```
| COUNT(*) |
|----------|
| 19       |
- Print out how many books were released in each year
```mysql
SELECT released_year,
       COUNT(*)
FROM books
GROUP BY released_year;
```
|   released_year |   book_count |
|----------------|--------------|
|            1945 |            1 |
|            1981 |            1 |
|            1985 |            1 |
|            1989 |            1 |
|            1996 |            1 |
|            2000 |            1 |
|            2001 |            3 |
|            2003 |            2 |
|            2004 |            1 |
|            2005 |            1 |
|            2010 |            1 |
|            2012 |            1 |
|            2013 |            1 |
|            2014 |            1 |
|            2016 |            1 |
|            2017 |            1 |
- Print out the total number of books in stock
```mysql
SELECT SUM(stock_quantity)
FROM books;
```
| SUM(stock_quantity) |
|--------------------|
| 2450               |

- Find the average release year for each author
```mysql
SELECT AVG(released_year)
FROM books
GROUP BY author_lname, author_fname;
```
| author_lname   | author_fname   |   avg_released_year |
|----------------|---------------|---------------------|
| Carver         | Raymond        |             1985.00 |
| Chabon         | Michael        |             2000.00 |
| DeLillo        | Don            |             1985.00 |
| Eggers         | Dave           |             2008.67 |
| Foster Wallace | David          |             2004.50 |
| Gaiman         | Neil           |             2006.67 |
| Harris         | Dan            |             2014.00 |
| Harris         | Freida         |             2001.00 |
| Lahiri         | Jhumpa         |             1999.50 |
| Saunders       | George         |             2017.00 |
| Steinbeck      | John           |             1945.00 |

- Find the full name of the author who wrote the longest book
```mysql
SELECT CONCAT(author_fname, ' ', author_lname) AS author,
       pages
FROM books
WHERE pages = (SELECT MAX(pages)
	       FROM books);
```
| author         |   pages |
|----------------|---------|
| Michael Chabon |     634 |
- Create a table with 3 columns
  - year
  - number of books
  - average pages of books per year
```mysql
SELECT released_year AS year,
       COUNT(*) AS '# books',
       AVG(pages) AS 'avg pages'
FROM books
GROUP BY released_year
ORDER BY released_year;
```
|   year |   # books |   avg pages |
|--------|-----------|-------------|
|   1945 |         1 |      181.00  |
|   1981 |         1 |      176.00  |
|   1985 |         1 |      320.00  |
|   1989 |         1 |      526.00  |
|   1996 |         1 |      198.00  |
|   2000 |         1 |      634.00  |
|   2001 |         3 |      443.33  |
|   2003 |         2 |      249.50  |
|   2004 |         1 |      329.00  |
|   2005 |         1 |      343.00  |
|   2010 |         1 |      304.00  |
|   2012 |         1 |      352.00  |
|   2013 |         1 |      504.00  |
|   2014 |         1 |      256.00  |
|   2016 |         1 |      304.00  |
|   2017 |         1 |      367.00  |
