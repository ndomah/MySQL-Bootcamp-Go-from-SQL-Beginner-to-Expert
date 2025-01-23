# Revisiting Data Types
- [MySQL Data Types Documentation](https://dev.mysql.com/doc/refman/8.0/en/data-types.html)
## `CHAR` vs. `VARCHAR`
- Use `CHAR` and `VARCHAR` for storing text
- `CHAR` has a *fixed length*
  - `CHAR(3)` --> Only 3 characters "allowed"
  - Length can be any value from 0 to 255
  - `CHAR` is faster for fixed length text
    - State abbreviations: CA, NY
    - Yes/No flags: Y/N
    - Zip codes: 59715, 94924
- If your use case requires more, use `VARCHAR`

|Value|`CHAR(4)`|Storage|`VARCHAR(4)`|Storage|
|:---|:---|:---|:---|:---|
|''|'  '|4 bytes|''|1 byte|
|'ab'|'ab '|4 bytes|'ab'|3 bytes|
|'abcd'|'abcd'|4 bytes|'abcd'|5 bytes|
## `INT`, `TINYINT`, `BIGINT`, etc.
- `INT`: whole numbers

| Type      | Storage (Bytes) | Minimum Value Signed | Minimum Value Unsigned | Maximum Value Signed | Maximum Value Unsigned |
|-----------|----------------|----------------------|-----------------------|----------------------|-----------------------|
| TINYINT   | 1              | -128                  | 0                      | 127                   | 255                    |
| SMALLINT  | 2              | -32768                | 0                      | 32767                 | 65535                   |
| MEDIUMINT | 3              | -8388608              | 0                      | 8388607               | 16777215                |
| INT       | 4              | -2147483648           | 0                      | 2147483647            | 4294967295              |
| BIGINT    | 8              | -2^63                  | 0                      | 2^63 - 1              | 2^64 - 1               |
## `DECIMAL`
- `DECIMAL(total number of digits, digits after decimal)`
  -  `DECIMAL(5,2)` --> 999.99
## `FLOAT` & `DOUBLE`
- Use `FLOAT` or `DOUBLE` to store larger numbers using less space BUT it comes at the cost of precision

|Data Type|Memory Needed|Precision Issues|
|:---|:---|:---|
|`FLOAT`|4 Bytes|~7 digits|
|`DOUBLE`|8 Bytes|~15 digits|
## Dates & Times
- `DATE`: values with a date but no time
  - YYYY-MM-DD format
- `TIME`: values with a time but no date
  - HH:MM:SS format
- `DATETIME`: values with a date AND time
  - 'YYYY-MM-DD HH:MM:SS' format
## Working with Dates
- Create the following table and insert samples:
```mysql
CREATE TABLE people (
	name VARCHAR(100),
    birthdate DATE,
    birthtime TIME,
    birthdt DATETIME
);
 
INSERT INTO people (name, birthdate, birthtime, birthdt)
VALUES ('Elton', '2000-12-25', '11:00:00', '2000-12-25 11:00:00');
 
INSERT INTO people (name, birthdate, birthtime, birthdt)
VALUES ('Lulu', '1985-04-11', '9:45:10', '1985-04-11 9:45:10');
 
INSERT INTO people (name, birthdate, birthtime, birthdt)
VALUES ('Juan', '2020-08-15', '23:59:00', '2020-08-15 23:59:00');
```
## `CURDATE`, `CURTIME`, & `NOW`
- `CURDATE()`: returns the current date in YYYY-MM-DD format
- `CURTIME()` (also `CURRENT_TIME()`): returns the current time in HH:MM:SS format
- `NOW()` (also `CURRENT_TIMESTAMP()`): returns the current datetime in YYYY-MM-DD HH:MM:SS format
- Add the following person to the people table:
```mysql
INSERT INTO people (name, birthdate, birthtime, birthdt)
VALUES ('Hazel', CURDATE(), CURTIME(), NOW());
```
## Date Functions
- `DAY`, `DAYOFWEEK`, and `DAYOFYEAR`
```mysql
SELECT birthdate,
       DAY(birthdate),
       DAYOFWEEK(birthdate),
       DAYOFYEAR(birthdate)
FROM people;
```
|birthdate|DAY(birthdate|DAYOFWEEK(birthdate)|DAYOFYEAR(birthdate)|
|---|---|---|---|
|2000-12-25|25|2|360|
|1985-04-11|11|5|101|
|2020-08-15|15|7|228|
|2022-10-05|5|4|278|
- `MONTHNAME` and `YEAR`
```mysql
SELECT birthdate,
       MONTHNAME(birthdate),
       YEAR(birthdate)
FROM people;
```
|birthdate|MONTHNAME(birthdate)|YEAR(birthdate)|
|---|---|---|
|2000-12-25|December|2000|
|1985-04-11|November|1985|
|2020-08-15|August|2020|
|2022-10-05|October|2022|
## Time Functions
```mysql
SELECT birthtime,
       HOUR(birthtime),
       MINUTE(birthtime)
FROM people;
```
|birthdate|HOUR(birthtime)|MINUTE(birthtime)|
|---|---|---|
|11:00:00|11|0|
|09:45:10|9|45|
|23:59:00|23|59|
|08:13:50|8|13|
```mysql
SELECT birthdt,
       MONTH(birthdt),
       DAY(birthdt),
       HOUR(birthdt),
       MINUTE(birthdt)
FROM people;
```
|birthdt|MONTH(birthdt)|DAY(birthdt)|HOUR(birthdt)|MINUTE(birthdt)|
|---|---|---|---|---|
|2000-12-25 11:00:00|12|25|11|0|
|1985-04-11 09:45:10|4|11|9|45|
|2020-08-15 23:59:00|8|15|23|59|
|2022-10-05 08:13:50|1|23|8|13|
## Formatting Dates
```mysql
SELECT birthdate,
       DATE_FORMAT(birthdate, '%a %b %D')
FROM people;
```
|birthdate|DATE_FORMAT(birthdate, '%a %b %D')|
|---|---|
|2000-12-25|Mon Dec 25th|
|1985-04-11|Thu Apr 11th|
|2020-08-15|Sat Aug 15th|
|2022-10-05|Thu Jan 23rd|
```mysql
SELECT birthdt,
       DATE_FORMAT(birthdt, '%H:%i')
FROM people;
```
|birthdt|DATE_FORMAT(birthdt, '%H:%i')|
|---|---|
|2000-12-25 11:00:00|11:00|
|1985-04-11 09:45:10|09:45|
|2020-08-15 23:59:00|23:59|
|2022-10-05 08:13:50|08:13|
```mysql
SELECT birthdt,
       DATE_FORMAT(birthdt, 'BORN ON: %r')
FROM people;
```
|birthdt|DATE_FORMAT(birthdt, 'BORN ON: %r')|
|---|---|
|2000-12-25 11:00:00|BORN ON: 11:00 AM|
|1985-04-11 09:45:10|BORN ON: 09:45 AM|
|2020-08-15 23:59:00|BORN ON: 23:59 PM|
|2022-10-05 08:13:50|BORN ON: 08:13 AM|
## Date Math
```mysql
SELECT birthdate,
       DATEDIFF(CURDATE(), birthdate)
FROM people;
```
|birthdate|DATEDIFF(CURDATE(), birthdate)|
|---|---|
|2000-12-25|7954|
|1985-04-11|13691|
|2020-08-15|781|
|2022-10-05|0|
```mysql
SELECT DATE_ADD(CURDATE(), INTERVAL 12 YEAR);
```
|DATE_ADD(CURDATE(), INTERVAL 12 YEAR)|
|---|
|2034-10-05|
```mysql
SELECT TIMEDIFF(CURTIME(), '07:00:00');
```
|TIMEDIFF(CURTIME(), '07:00:00')|
|---|
|10:32:13|
```mysql
SELECT NOW() - INTERVAL 18 YEAR;
```
|NOW() - INTERVAL 18 YEAR|
|---|
|2004-10-05 17:36:10|
```mysql
SELECT name,
       birthdate,
       YEAR(birthdate + INTERVAL 21 YEAR) AS will_be_21
FROM people;
```
|name|birthdate|will_be_21|
|---|---|---|
|Elton|2000-12-25|2021|
|Lulu|1985-04-11|2006|
|Juan|2020-08-15|2041|
|Hazel|2022-10-05|2043|
## `DEFAULT` & `ON UPDATE TIMESTAMPS`
```mysql
CREATE TABLE captions (
  text VARCHAR(150),
  created_at TIMESTAMP default CURRENT_TIMESTAMP
);

INSERT INTO captions (text)
VALUES ('just me and the girls chillin');

INSERT INTO captions (text)
VALUES ('beautiful sunset');

SELECT *
FROM captions;
```
|text|created_at|
|---|---|
|just me and the girls chillin|2022-10-05 18:04:01|
|beautiful sunset|2022-10-05 18:04:09|
```mysql
CREATE TABLE captions2 (
  text VARCHAR(150),
  created_at TIMESTAMP default CURRENT_TIMESTAMP,
  updated_at TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
);

INSERT INTO captions2 (text)
VALUES ('i love life!');

SELECT *
FROM captions2;
```
|text|created_at|update_at|
|---|---|---|
|i love life!|2022-10-05 18:06:055|NULL|
```mysql
UPDATE captions2
SET text='i love life!!!';

SELECT *
FROM captions2;
```
|text|created_at|update_at|
|---|---|---|
|i love life!!!|2022-10-05 18:06:055|2022-10-05 18:08:12|
## Data Types Exercise
- What's a good use case for `CHAR`? (just make one up)
  - Used for text that we know has a fixed length
    - state/country abbreviations, yes/no flags, etc. 
- Fill in the blanks: (price is always < 1,000,000)
```mysql
CREATE TABLE inventory (
  item_name ________,
  price ______,
  quantity ______
);
```
```mysql
CREATE TABLE inventory (
  item_name VARCHAR(100),
  price DECIMAL(8,2),
  quantity INT
);
```
- What's the difference between `DATETIME` and `TIMESTAMP`?
  - They both store datetime information, but there's a difference in the range
    - `TIMESTAMP` has a smaller range, and takes up less space
    - `TIMESTAMP` is used for things like meta-data about when something is created or updated 
- Print out the current time
```mysql
SELECT CURTIME();
```
- Print out the current date (but not time)
```mysql
SELECT CURDATE();
```
- Print out the current date of the week (the number)
```mysql
SELECT DAYOFWEEK(CURDATE());
SELECT DAYOFWEEK(NOW());
SELECT DATE_FORMAT(NOW(), '%w') + 1;
```
- Print out the current date of the week (the day name)
```mysql
SELECT DAYNAME(NOW());
SELECT DATE_FORMAT(NOW(), '%W');
```
- Print out the current day and time using this format: MM/DD/YYYY
```mysql
SELECT DATE_FORMAT(CURDATE(), '%m/%d/%Y');
```
- Print out the current day and time using this format: January 2nd at 3:15
```mysql
SELECT DATE_FORMAT(NOW(), '%M %D at %k:%i');
```
- Create a tweets table that stores:
  - the tweet content
  - a username
  - time it was created
 ```mysql
CREATE TABLE tweets (
  content VARCHAR(140),
  username VARCHAR(20),
  created_at TIMESTAMP DEFAULT NOW()
);

INSERT INTO tweets (content, username)
VALUES ('this is my first tweet', 'coltscat');

INSERT INTO tweets (content, username)
VALUES ('this is my second tweet', 'coltscat');
```
