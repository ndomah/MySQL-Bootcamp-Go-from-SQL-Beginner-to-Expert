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
|   book_id | author_fname   | author_lname   |   pages |
|-----------|---------------|---------------|---------|
|        14 | Don           | DeLillo       |     320 |
|        16 | David         | Foster Wallace|     329 |
|        17 | David         | Foster Wallace|     343 |
|         6 | Dave          | Eggers        |     504 |
|         5 | Dave          | Eggers        |     352 |
|         9 | Dave          | Eggers        |     437 |
|        18 | Freida        | Harris        |     428 |
|        19 | Dan           | Harris        |     256 |
|         7 | Michael       | Chabon        |     634 |
|         4 | Jhumpa        | Lahiri        |     198 |
|         1 | Jhumpa        | Lahiri        |     291 |
|         3 | Neil          | Gaiman        |     465 |
|         2 | Neil          | Gaiman        |     304 |
|        10 | Neil          | Gaiman        |     208 |
|        15 | George        | Saunders      |     367 |
|        13 | John          | Steinbeck     |     181 |
|        12 | Raymond       | Carver        |     526 |
|        11 | Raymond       | Carver        |     176 |
- You can use numbers to indicate what column in the `SELECT` statement you want to sort by
```mysql
SELECT book_id, author_fname, author_lname, pages
FROM books
ORDER BY 2 desc;
```
|   book_id | author_fname   | author_lname   |   pages |
|-----------|---------------|---------------|---------|
|         7 | Michael       | Chabon        |     634 |
|        12 | Raymond       | Carver        |     526 |
|        11 | Raymond       | Carver        |     176 |
|         4 | Jhumpa        | Lahiri        |     198 |
|         1 | Jhumpa        | Lahiri        |     291 |
|         3 | Neil          | Gaiman        |     465 |
|         2 | Neil          | Gaiman        |     304 |
|        10 | Neil          | Gaiman        |     208 |
|        18 | Freida        | Harris        |     428 |
|        19 | Dan           | Harris        |     256 |
|        14 | Don           | DeLillo       |     320 |
|        16 | David         | Foster Wallace|     329 |
|        17 | David         | Foster Wallace|     343 |
|         6 | Dave          | Eggers        |     504 |
|         5 | Dave          | Eggers        |     352 |
|         9 | Dave          | Eggers        |     437 |
|        15 | George        | Saunders      |     367 |
|        13 | John          | Steinbeck     |     181 |
## `LIMIT`
- Limit how many rows you want in the output
```mysql
SELECT title, released_year
FROM books 
ORDER BY released_year DESC
LIMIT 5;
```
| title                    |   released_year |
|--------------------------|----------------|
| Lincoln In The Bardo     |            2017 |
| Norse Mythology          |            2016 |
| 10% Happier              |            2014 |
| The Circle               |            2013 |
| A Hologram for the King: A Novel |      2012 |
- You can also use an offset (10) and a row count (1)
  - Skip the first 10 rows, choose the 11th row  
```mysql
SELECT title, released_year
FROM books 
ORDER BY released_year DESC
LIMIT 10,1;
```
| title                              |   released_year |
|------------------------------------|----------------|
| Consider the Lobster               |            2005 |
- You can use an extremely large row count if your table has fewer rows than the row count
  - It will print every row after the offset
```mysql
SELECT title
FROM books
LIMIT 5, 123219476457;
```
| title                               |
|-------------------------------------|
| The Circle                          |
| The Amazing Adventures of Kavalier & Clay |
| Just Kids                           |
| A Heartbreaking Work of Staggering Genius |
| Coraline                            |
| What We Talk About When We Talk About Love: Stories |
| Where I'm Calling From: Selected Stories |
| White Noise                         |
| Cannery Row                          |
| Oblivion: Stories                    |
| Consider the Lobster                 |
## `LIKE`
- Used for comparitive searching
- `%` are wildcards that indicate 0 or more characters
```mysql
SELECT title, author_fname, author_lname, pages 
FROM books
WHERE author_fname LIKE '%da%';
```
| title                | author_fname   | author_lname     |   pages |
|----------------------|----------------|------------------|---------|
| 10% Happier          | Dan            | Harris           |     256 |
| fake_book            | Freida         | Harris           |     428 |
| Consider the Lobster | David          | Foster Wallace   |     343 |
| Oblivion: Stories    | David          | Foster Wallace   |     329 |
```mysql
SELECT title, author_fname, author_lname, pages 
FROM books
WHERE title LIKE '%:%';
```
| title                                               | author_fname   | author_lname     |   pages |
|-----------------------------------------------------|----------------|------------------|---------|
| A Hologram for the King: A Novel                    | Dave           | Eggers           |     352 |
| Oblivion: Stories                                   | David          | Foster Wallace   |     329 |
| What We Talk About When We Talk About Love: Stories | Raymond        | Carver           |     176 |
- `_` are wildcards that indicate 1 character
- They can be stacked
```mysql
SELECT *
FROM books
WHERE author_fname LIKE '____';
```
|   book_id | title                  | author_fname | author_lname  |   released_year |   stock_quantity |   pages |
|-----------|------------------------|--------------|---------------|----------------|------------------|---------|
|        14 | White Noise             | Don          | DeLillo       |           1985 |               49 |     320 |
|        19 | 10% Happier              | Dan          | Harris        |           2014 |               29 |     256 |
|         5 | A Hologram for the King: A Novel | Dave         | Eggers        |           2012 |              154 |     352 |
```mysql
SELECT *
FROM books
WHERE author_fname LIKE '_a_';
```
|   book_id | title       | author_fname | author_lname |   released_year |   stock_quantity |   pages |
|-----------|-------------|--------------|--------------|----------------|------------------|---------|
|        19 | 10% Happier | Dan          | Harris       |           2014 |               29 |     256 |
## Escaping Wildcards
- What if you are searching for a book with a '%' or a '_' in it?
- Use a backslash `\`
```mysql
SELECT *
FROM books
WHERE title LIKE '%\%%';
```
|   book_id | title         | author_fname | author_lname |   released_year |   stock_quantity |   pages |
|-----------|--------------|--------------|--------------|----------------|------------------|---------|
|        19 | 10% Happier   | Dan          | Harris       |           2014 |               29 |     256 |
```mysql
SELECT *
FROM books
WHERE title LIKE '%\_%';
```
|   book_id | title                                       | author_fname | author_lname |   released_year |   stock_quantity |   pages |
|-----------|---------------------------------------------|--------------|--------------|----------------|------------------|---------|
|         7 | The Amazing Adventures of Kavalier & Clay   | Michael      | Chabon       |           2000 |               68 |     634 |
|        18 | fake_book                                   | Freida       | Harris       |           2001 |              287 |     428 |
## Refining Selections Exercises
- Select all titles that contain 'stories'
```mysql
SELECT title
FROM books
WHERE title LIKE '%stories%';
```
| title                                               |
|-----------------------------------------------------|
| Where I'm Calling From: Selected Stories            |
| What We Talk About When We Talk About Love: Stories |
| Oblivion: Stories                                   |
- Find the longest book, print out the title and page count
```mysql
SELECT title, pages
FROM books
ORDER BY pages DESC
LIMIT 1;
```
| title                                       |   pages |
|---------------------------------------------|---------|
| The Amazing Adventures of Kavalier & Clay   |     634 |
- Print a summary containing the title and year, for the 3 most recent books
```mysql
SELECT CONCAT(title, ' - ', released_year) AS summary
FROM books
ORDER BY released_year DESC
LIMIT 3;
```
| summary                     |
|-----------------------------|
| Lincoln In The Bardo - 2017 |
| Norse Mythology - 2016      |
| 10% Happier - 2014          |
- Find all books where the author's last name contains a space
```mysql
SELECT title, author_lname
FROM books
WHERE author_lname LIKE '% %';
```
| title                | author_lname   |
|----------------------|----------------|
| Oblivion: Stories    | Foster Wallace |
| Consider the Lobster | Foster Wallace |
- Find the 3 books with the lowest stock (select title, year, and stock)
```mysql
SELECT title, released_year, stock_quantity
FROM books
ORDER BY stock_quantity
LIMIT 3;
```
| title                                               |   released_year |   stock_quantity |
|-----------------------------------------------------|-----------------|------------------|
| American Gods                                       |            2001 |               12 |
| Where I'm Calling From: Selected Stories            |            1989 |               12 |
| What We Talk About When We Talk About Love: Stories |            1981 |               23 |
- Print the title and author's last name, sorted first by author's last name and then by title
```mysql
SELECT title, author_lname
FROM books
ORDER BY 2, 1;
```
| title                                               | author_lname     |
|-----------------------------------------------------|------------------|
| What We Talk About When We Talk About Love: Stories | Carver           |
| Where I'm Calling From: Selected Stories            | Carver           |
| White Noise                                         | DeLillo           |
| Consider the Lobster                                | Foster Wallace   |
| Oblivion: Stories                                   | Foster Wallace   |
| The Amazing Adventures of Kavalier & Clay           | Chabon           |
| The Circle                                          | Eggers           |
| A Hologram for the King: A Novel                    | Eggers           |
| A Heartbreaking Work of Staggering Genius           | Eggers           |
| 10% Happier                                         | Harris           |
| fake_book                                           | Harris           |
| Coraline                                            | Gaiman           |
| American Gods                                       | Gaiman           |
| Norse Mythology                                     | Gaiman           |
| Interpreter of Maladies                             | Lahiri           |
| The Namesake                                        | Lahiri           |
| Lincoln In The Bardo                                | Saunders         |
| Cannery Row                                         | Steinbeck        |
- Generate a table that contains an uppercase statement in the following format: "MY FAVORITE AUTHOR IS <AUTHOR'S NAME>!
- Sort it alphabetically by last name
```mysql
SELECT UPPER(CONCAT('My favorite author is ', author_fname, ' ', author_lname, '!')) AS yell
FROM books
ORDER BY author_lname;
```
| yell                                        |
|---------------------------------------------|
| MY FAVORITE AUTHOR IS RAYMOND CARVER!       |
| MY FAVORITE AUTHOR IS RAYMOND CARVER!       |
| MY FAVORITE AUTHOR IS MICHAEL CHABON!       |
| MY FAVORITE AUTHOR IS DON DELILLO!          |
| MY FAVORITE AUTHOR IS DAVE EGGERS!          |
| MY FAVORITE AUTHOR IS DAVE EGGERS!          |
| MY FAVORITE AUTHOR IS DAVE EGGERS!          |
| MY FAVORITE AUTHOR IS NEIL GAIMAN!          |
| MY FAVORITE AUTHOR IS NEIL GAIMAN!          |
| MY FAVORITE AUTHOR IS NEIL GAIMAN!          |
| MY FAVORITE AUTHOR IS JHUMPA LAHIRI!        |
| MY FAVORITE AUTHOR IS JHUMPA LAHIRI!        |
| MY FAVORITE AUTHOR IS DAN HARRIS!           |
| MY FAVORITE AUTHOR IS FREIDA HARRIS!        |
| MY FAVORITE AUTHOR IS GEORGE SAUNDERS!      |
| MY FAVORITE AUTHOR IS JOHN STEINBECK!       |
| MY FAVORITE AUTHOR IS PATRICIA SMITH!       |
| MY FAVORITE AUTHOR IS DAVID FOSTER WALLACE! |
| MY FAVORITE AUTHOR IS DAVID FOSTER WALLACE! |
