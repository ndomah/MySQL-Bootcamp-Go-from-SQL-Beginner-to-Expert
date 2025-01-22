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
