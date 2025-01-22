# String Functions
- Refer to the [MySQL Documentation](https://dev.mysql.com/doc/refman/8.0/en/string-functions.html) for all string functions
- Run the [book_data.sql](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/5.%20String%20Functions/book_data.sql) file to load in the books data
## `CONCAT`
- Combine data for cleaner output
```mysql
SELECT CONCAT('h', 'e', 'l');
```
|CONCAT('h', 'e', 'l')|
|:---|
|hel|
- Combine author first names with their respective last names
```mysql
SELECT CONCAT(author_fname, ' ', author_lname)
FROM books;
```
|CONCAT(author_fname, ' ', author_lname)|
|:------------------------------------------|
| Jhumpa Lahiri                            |
| Neil Gaiman                              |
| Neil Gaiman                              |
| Jhumpa Lahiri                            |
| Dave Eggers                              |
| Dave Eggers                              |
| Michael Chabon                           |
| Patti Smith                              |
| Dave Eggers                              |
| Neil Gaiman                              |
| Raymond Carver                           |
| Raymond Carver                           |
| Don DeLillo                              |
| John Steinbeck                           |
| David Foster Wallace                     |
| David Foster Wallace                     |
- Use an alias for better column output readability
```mysql
SELECT CONCAT(author_fname, ' ', author_lname) AS author_name
FROM books;
```
|author_name|
|:------------------------------------------|
| Jhumpa Lahiri                            |
| Neil Gaiman                              |
| Neil Gaiman                              |
| Jhumpa Lahiri                            |
| Dave Eggers                              |
| Dave Eggers                              |
| Michael Chabon                           |
| Patti Smith                              |
| Dave Eggers                              |
| Neil Gaiman                              |
| Raymond Carver                           |
| Raymond Carver                           |
| Don DeLillo                              |
| John Steinbeck                           |
| David Foster Wallace                     |
| David Foster Wallace                     |
## `SUBSTRING`
- Work with parts of string
```mysql
SELECT SUBSTRING('Hello World', 1, 4);
```
|SUBSTRING('Hello World', 1, 4)|
|:---|
|Hell|
- *NOTE:* MySQL is not 0 based indexed like Python
```mysql
SELECT SUBSTRING('Hello World', 7);
```
|SUBSTRING('Hello World', 7)|
|:---|
|World|
```mysql
SELECT SUBSTRING('Hello World', -3);
```
|SUBSTRING('Hello World', -3)|
|:---|
|rld|
```mysql
SELECT SUBSTRING(title, 1, 10) AS 'short title' FROM books;

-- Can also be written as:
SELECT SUBSTR(title, 1, 10) AS 'short title' FROM books;
```
|short title |
|:--------------|
| The Namesa   |
| Norse Myth   |
| American G   |
| Interprete   |
| A Hologram   |
| The Circle   |
| The Amazin   |
| Just Kids    |
| A Heartbre   |
| Coraline     |
| What We Ta   |
| Where I'm   |
| White Nois   |
| Cannery Ro   |
| Oblivion:   |
| Consider t   |
## Combining String Functions
```mysql
SELECT CONCAT
    (
        SUBSTRING(title, 1, 10),
        '...'
    ) AS 'short title'
FROM books;
```
|short title|
|:--------------|
| The Namesa...   |
| Norse Myth...    |
| American G...    |
| Interprete...    |
| A Hologram...    |
| The Circle...    |
| The Amazin...    |
| Just Kids...     |
| A Heartbre...    |
| Coraline...      |
| What We Ta...    |
| Where I'm...    |
| White Nois...    |
| Cannery Ro...    |
| Oblivion: ...    |
| Consider t...    |
## *Sidenote:* SQL Formatting
- You can use a [SQL Formatter](https://codebeautify.org/sqlformatter) to improve readabilty and 'beautify' your code
```mysql
-- Before:
SELECT CONCAT
    (
        SUBSTRING(title, 1, 10),
        '...'
    ) AS 'short title'
FROM books;

-- After:
SELECT 
  CONCAT (
    SUBSTRING(title, 1, 10), 
    '...'
  ) AS 'short title' 
FROM 
  books;
```
## `REPLACE`
- Replace parts of strings
```mysql
SELECT REPLACE('Hello World', 'Hell', '%$#@');
```
|REPLACE('Hello World', 'Hell', '%$#@')|
|:---|
|%$#@o World|
```mysql
SELECT REPLACE('Hello World', 'l', '7');
```
|REPLACE('Hello World', 'l', '7')|
|:---|
|He77o Wor7d|
```mysql
SELECT REPLACE('cheese bread coffee milk', ' ', ' and ');
```
|REPLACE('cheese bread coffee milk', ' ', ' and ')|
|:---|
|cheese and bread and coffee and milk|
```mysql
SELECT REPLACE(title, 'e ', '3')
FROM books;
```
|REPLACE(title, 'e ', '3')|
|:-------------------------------------------------------------------|
| Th3Namesake                                                       |
| Nors3Mythology                                                    |
| American Gods                                                     |
| Interpreter of Maladies                                           |
| A Hologram for th3King: A Novel                                   |
| Th3Circle                                                         |
| Th3Amazing Adventures of Kavalier & Clay                          |
| Just Kids                                                         |
| A Heartbreaking Work of Staggering Genius                         |
| Coraline                                                          |
| What W3Talk About When W3Talk About Love: Stories                 |
| Wher3I'm Calling From: Selected Stories                           |
| Whit3Noise                                                        |
| Cannery Row                                                       |
| Oblivion: Stories                                                 |
| Consider th3Lobster                                               |
```mysql
SELECT REPLACE(title, ' ', '-') AS new_title
FROM books;
```
|new_title|
|:-----------------------------------------------------------|
| The-Namesake                                              |
| Norse-Mythology                                           |
| American-Gods                                             |
| Interpreter-of-Maladies                                   |
| A-Hologram-for-the-King:-A-Novel                          |
| The-Circle                                                |
| The-Amazing-Adventures-of-Kavalier-&-Clay                 |
| Just-Kids                                                 |
| A-Heartbreaking-Work-of-Staggering-Genius                 |
| Coraline                                                  |
| What-We-Talk-About-When-We-Talk-About-Love:-Stories       |
| Where-I'm-Calling-From:-Selected-Stories                  |
| White-Noise                                               |
| Cannery-Row                                               |
| Oblivion:-Stories                                         |
| Consider-the-Lobster                                      |
## `REVERSE`
- Reverse strings
```mysql
SELECT REVERSE('Hello World');
```
|REVERSE('Hello World')|
|:---|
|dlroW olleH|
```mysql
SELECT REVERSE(author_fname)
FROM books;
```
|REVERSE(author_fname)|
|:-----------------------|
| apmuhJ               |
| lieN                 |
| lieN                 |
| apmuhJ               |
| evaD                 |
| evaD                 |
| leahciM              |
| ittaP                |
| evaD                 |
| lieN                 |
| dnomyaR              |
| dnomyaR              |
| noD                  |
| nhoJ                 |
| divaD                |
| divaD                |
```mysql
SELECT CONCAT(author_fname, REVERSE(author_fname))
FROM books;
```
|CONCAT(author_fname, REVERSE(author_fname))|
|:--------------------------------------------|
| JhumpaapmuhJ                               |
| NeillieN                                   |
| NeillieN                                   |
| JhumpaapmuhJ                               |
| DaveevaD                                   |
| DaveevaD                                   |
| MichaelleahciM                             |
| PattiittaP                                 |
| DaveevaD                                   |
| NeillieN                                   |
| RaymonddnomyaR                             |
| RaymonddnomyaR                             |
| DonnoD                                     |
| JohnnhoJ                                   |
| DaviddivaD                                 |
| DaviddivaD                                 |
## `CHAR_LENGTH`
- Counts characters in strings
```mysql
SELECT CHAR_LENGTH('Hello World');
```
|CHAR_LENGTH('Hello World')|
|:---|
|11|
```mysql
SELECT CHAR_LENGTH(title) as length, title
FROM books;
```
|length|title|
|:--------|:-----------------------------------------------------------|
| 12     | The Namesake                                              |
| 15     | Norse Mythology                                           |
| 13     | American Gods                                             |
| 23     | Interpreter of Maladies                                   |
| 32     | A Hologram for the King: A Novel                          |
| 10     | The Circle                                                |
| 41     | The Amazing Adventures of Kavalier & Clay                 |
| 9      | Just Kids                                                 |
| 41     | A Heartbreaking Work of Staggering Genius                 |
| 8      | Coraline                                                  |
| 51     | What We Talk About When We Talk About Love: Stories       |
| 40     | Where I'm Calling From: Selected Stories                  |
| 11     | White Noise                                               |
| 11     | Cannery Row                                               |
| 17     | Oblivion: Stories                                         |
| 20     | Consider the Lobster                                      |
```mysql
SELECT author_lname,
       CHAR_LENGTH(author_lname) AS 'length'
FROM books;
```
|author_lname|length|
|:---|:---|
| Lahiri         | 6      |
| Gaiman         | 6      |
| Gaiman         | 6      |
| Lahiri         | 6      |
| Eggers         | 6      |
| Eggers         | 6      |
| Chabon         | 6      |
| Smith          | 5      |
| Eggers         | 6      |
| Gaiman         | 6      |
| Carver         | 6      |
| Carver         | 6      |
| DeLillo        | 7      |
| Steinbeck      | 9      |
| Foster Wallace | 14     |
| Foster Wallace | 14     |
```mysql
SELECT CONCAT(author_lname, ' is ', CHAR_LENGTH(author_lname), ' characters long')
FROM books;
```
|CONCAT(author_lname,' is ',CHAR_LENGTH(author_lname),' characters long')|
|:------------------------------------------------------------------------|
|Lahiri is 6 characters long                                             |
|Gaiman is 6 characters long                                             |
|Gaiman is 6 characters long                                             |
|Lahiri is 6 characters long                                             |
|Eggers is 6 characters long                                             |
|Eggers is 6 characters long                                             |
|Chabon is 6 characters long                                             |
|Smith is 5 characters long                                              |
|Eggers is 6 characters long                                             |
|Gaiman is 6 characters long                                             |
|Carver is 6 characters long                                             |
|Carver is 6 characters long                                             |
|DeLillo is 7 characters long                                            |
|Steinbeck is 9 characters long                                          |
|Foster Wallace is 14 characters long                                    |
|Foster Wallace is 14 characters long                                    |
## `UPPER()` & `LOWER()`
- Change a string's case
```mysql
SELECT UPPER('Hello World');
```
|UPPER('Hello World')|
|:---|
|HELLO WORLD|
```mysql
SELECT LOWER('Hello World');
```
|LOWER('Hello World')|
|:---|
|hello world|
```mysql
SELECT CONCAT('My favorite book is ', UPPER(title)) AS fav_book
FROM books;
```
|fav_book                                                           |
|:-------------------------------------------------------------------|
|My favorite book is THE NAMESAKE                                   |
|My favorite book is NORSE MYTHOLOGY                                |
|My favorite book is AMERICAN GODS                                  |
|My favorite book is INTERPRETER OF MALADIES                        |
|My favorite book is A HOLOGRAM FOR THE KING: A NOVEL               |
|My favorite book is THE CIRCLE                                     |
|My favorite book is THE AMAZING ADVENTURES OF KAVALIER & CLAY      |
|My favorite book is JUST KIDS                                      |
|My favorite book is A HEARTBREAKING WORK OF STAGGERING GENIUS      |
|My favorite book is CORALINE                                       |
|My favorite book is WHAT WE TALK ABOUT WHEN WE TALK ABOUT LOVE: STORIES|
|My favorite book is WHERE I'M CALLING FROM: SELECTED STORIES       |
|My favorite book is WHITE NOISE                                    |
|My favorite book is CANNERY ROW                                    |
|My favorite book is OBLIVION: STORIES                              |
|My favorite book is CONSIDER THE LOBSTER                           |
## Other String Functions
### `INSERT`
```mysql
SELECT INSERT('Hello Bobby', 6, 0, 'There');
```
|INSERT('Hello Bobby', 6, 0, 'There')|
|:---|
|HelloThere Bobby|
### `LEFT`
```mysql
SELECT LEFT('omghahalol!', 3);
```
|LEFT('omghahalol!', 3)|
|:---|
|omg|
### `RIGHT`
```mysql
SELECT RIGHT('omghahalol!', 4);
```
|RIGHT('omghahalol!', 4)|
|:---|
|lol!|
### `REPEAT`
```mysql
SELECT REPEAT('ha', 4);
```
|REPEAT('ha', 4)|
|:---|
|hahahaha|
### `TRIM`
```mysql
SELECT TRIM('  pickle  ');
```
|TRIM('  pickle  ')|
|:---|
|pickle|
## String Functions Exercise
- Reverse and uppercase the following sentence: "Why does my cat look at me with such hatred?"
```mysql
SELECT UPPER(REVERSE("Why does my cat look at me with such hatred?"));
```
|UPPER(REVERSE("Why does my cat look at me with such hatred?"))|
|:--------------------------------------------------------------|
|?DERTAH SUHC HTIW EM TA KOOL TAC YM SEOD YHW                  |

- What does the following code print out? (Describe before running)
```mysql
SELECT
  REPLACE
  (
  CONCAT('I', ' ', 'like', ' ', 'cats'),
  ' ',
  '_'
  );
```
  - It first concats the words with a space: I like cats
  - Then it replaces ths trings with a hyphen: I-like-cats

|REPLACE(CONCAT('I',' ','like',' ','cats'),' ','_')|
|:--------------------------------------------------|
|I_like_cats                                       |
- Replace spaces in titles with '->'
```mysql
SELECT REPLACE(title, ' ', '->') AS title
FROM books;
```
|title                                                                |
|:---------------------------------------------------------------------|
|The->Namesake                                                        |
|Norse->Mythology                                                     |
|American->Gods                                                       |
|Interpreter->of->Maladies                                            |
|A->Hologram->for->the->King:->A->Novel                               |
|The->Circle                                                          |
|The->Amazing->Adventures->of->Kavalier->&->Clay                      |
|Just->Kids                                                           |
|A->Heartbreaking->Work->of->Staggering->Genius                       |
|Coraline                                                             |
|What->We->Talk->About->When->We->Talk->About->Love:->Stories        |
|Where->I'm->Calling->From:->Selected->Stories                        |
|White->Noise                                                         |
|Cannery->Row                                                         |
|Oblivion:->Stories                                                  |
|Consider->the->Lobster                                              |
- In one column, print the authors' first name normally as `forwards`
- In another column, print the authors' first name backwards as `backwards`
```mysql
SELECT author_fname AS forwards,
       REVERSE(author_fname) AS backwards
FROM books;
```
|forwards|backwards|
|--------|---------|
|Jhumpa  |apmuhJ   |
|Neil    |lieN     |
|Neil    |lieN     |
|Jhumpa  |apmuhJ   |
|Dave    |evaD     |
|Dave    |evaD     |
|Michael |leahciM  |
|Patti   |ittaP    |
|Dave    |evaD     |
|Neil    |lieN     |
|Raymond |dnomyaR  |
|Raymond |dnomyaR  |
|Don     |noD      |
|John    |nhoJ     |
|David   |divaD    |
|David   |divaD    |
- Generate a table that combines the authors' first and last names in uppercase as `full name in caps`
```mysql
SELECT UPPER(CONCAT(author_fname, ' ', author_lname)) AS 'full name in caps'
FROM books;
```
|full name in caps|
|-----------------|
|JHUMPA LAHIRI    |
|NEIL GAIMAN      |
|NEIL GAIMAN      |
|JHUMPA LAHIRI    |
|DAVE EGGERS      |
|DAVE EGGERS      |
|MICHAEL CHABON   |
|PATTI SMITH      |
|DAVE EGGERS      |
|NEIL GAIMAN      |
|RAYMOND CARVER   |
|RAYMOND CARVER   |
|DON DELILLO      |
|JOHN STEINBECK   |
|DAVID FOSTER WALLACE|
|DAVID FOSTER WALLACE|
- Generate a table that tells you when a book was released as `blurb`
```mysql
SELECT CONCAT(title, ' was released in ', released_year) AS blurb
FROM books;
```
|blurb                                                             |
|------------------------------------------------------------------|
|The Namesake was released in 2003                                 |
|Norse Mythology was released in 2016                              |
|American Gods was released in 2001                                |
|Interpreter of Maladies was released in 1996                      |
|A Hologram for the King: A Novel was released in 2012             |
|The Circle was released in 2013                                   |
|The Amazing Adventures of Kavalier & Clay was released in 2000    |
|Just Kids was released in 2010                                    |
|A Heartbreaking Work of Staggering Genius was released in 2001    |
|Coraline was released in 2003                                     |
|What We Talk About When We Talk About Love: Stories was released in 1981 |
|Where I'm Calling From: Selected Stories was released in 1989     |
|White Noise was released in 1985                                  |
|Cannery Row was released in 1945                                  |
|Oblivion: Stories was released in 2004                            |
|Consider the Lobster was released in 2005                         |
- Print the book titles and the length of each title
```mysql
SELECT title,
       CHAR_LENGTH(title) AS `character count`
FROM books;
```
|title                                                        |character count|
|-------------------------------------------------------------|---------------|
|The Namesake                                                 |12             |
|Norse Mythology                                              |15             |
|American Gods                                               |13             |
|Interpreter of Maladies                                     |23             |
|A Hologram for the King: A Novel                            |32             |
|The Circle                                                  |10             |
|The Amazing Adventures of Kavalier & Clay                   |41             |
|Just Kids                                                   |9              |
|A Heartbreaking Work of Staggering Genius                   |41             |
|Coraline                                                    |8              |
|What We Talk About When We Talk About Love: Stories         |51             |
|Where I'm Calling From: Selected Stories                    |40             |
|White Noise                                                 |11             |
|Cannery Row                                                 |11             |
|Oblivion: Stories                                           |17             |
|Consider the Lobster                                        |20             |
- Generate the following table:

|short title|author|quantity|
|:---|:---|:---|
|American G...|Gaiman, Neil|12 in stock|
|A Heartbre...|Eggers, Dave|104 in stock|
```mysql
SELECT CONCAT(SUBSTRING(title, 1, 10), '...') AS 'short title',
       CONCAT(author_lname, ', ', author_fname) AS author,
       CONCAT(stock_quantity, ' in stock') AS quantity
FROM books
WHERE title = 'American Gods' OR title = 'A Heartbreaking Work of Staggering Genius';
```
