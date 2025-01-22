# Refining Selections
- Run the following code to insert more books into our books table:
```mysql
INSERT INTO books (title, author_fname, author_lname, released_year, stock_quantity, pages)
VALUES ('10% Happier', 'Dan', 'Harris', 2014, 29, 256), 
       ('fake_book', 'Freida', 'Harris', 2001, 287, 428),
       ('Lincoln In The Bardo', 'George', 'Saunders', 2017, 1000, 367);
```
## `DISTINCT`
- Find distinct values 
```mysql
SELECT author_lname
FROM books;
```
|author_lname|
|:---|
|Lahiri|
|Gaiman|
|Gaiman|
|Lahiri|
|Eggers|
|Eggers|
|Chabon|
|Smith|
|Eggers|
|Gaiman|
|Carver|
|Carver|
|DeLillo|
|Steinbeck|
|Foster Wallace|
|Foster Wallace|
|Harris|
|Harris|
|Saunders|
```mysql
SELECT DISTINCT author_lname
FROM books;
```
|author_lname|
|:---|
|Lahiri|
|Gaiman|
|Eggers|
|Chabon|
|Smith|
|Carver|
|DeLillo|
|Steinbeck|
|Foster Wallace|
|Harris|
|Saunders|
```mysql
SELECT DISTINCT CONCAT(author_fname,' ', author_lname) AS `distinct full names`
FROM books;
```
|distinct full names|
|:---|
|Jhumpa Lahiri|
|Neil Gaiman|
|Dave Eggers|
|Michael Chabon|
|Patti Smith|
|Raymond Carver|
|Don DeLillo|
|John Steinbeck|
|David Foster Wallace|
|Dan Harris|
|Freida Harris|
|George Saunders|
## `ORDER BY`
- Sorting our results
- Sorting is ascending by default
```mysql
SELECT DISTINCT author_lname
FROM books
ORDER BY author_lname;
```
|author_lname|
|:---|
|Carver|
|DeLillo|
|Eggers|
|Foster Wallace|
|Gaiman|
|Harris|
|Lahiri|
|Saunders|
|Smith|
|Steinbeck|
```mysql
SELECT DISTINCT author_lname
FROM books
ORDER BY author_lname DESC;
```
|author_lname|
|:---|
|Steinbeck|
|Smith|
|Saunders|
|Lahiri|
|Harris|
|Gaiman|
|Foster Wallace|
|Eggers|
|DeLillo|
|Carver|
```mysql
SELECT DISTINCT released_year
FROM books
ORDER BY released_year DESC;
```
|released_year|
|:---|
|2017|
|2016|
|2014|
|2013|
|2012|
|2010|
|2005|
|2004|
|2003|
|2001|
|2000|
|1996|
|1989|
|1985|
|1981|
|1945|
## More on `ORDER BY`
- You can sort by multiple columns
```mysql
SELECT book_id, author_fname, author_lname, pages
FROM books
ORDER BY author_lname, author_fname;
```
















