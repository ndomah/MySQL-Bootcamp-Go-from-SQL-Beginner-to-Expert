# Working with Lots of IG Data
- Run [ig_clone_data.sql](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/16.%20Working%20with%20Lots%20of%20IG%20Data/ig_clone_data.sql) to setup database and tables

## Challenge 1
- We want to reward our users who have been around the longest
- Find the 5 oldest users
```mysql
SELECT *
  FROM users
 ORDER BY created_at
 LIMIT 5;
```
| id  | username            | created_at          |
|-----|--------------------|---------------------|
|  80 | Darby_Herzog        | 2016-05-06 00:14:21  |
|  67 | Emilio_Bernier52    | 2016-05-06 13:04:30  |
|  63 | Elenor88            | 2016-05-08 01:30:41  |
|  95 | Nicole71            | 2016-05-09 17:30:22  |
|  38 | Jordyn.Jacobson2    | 2016-05-14 07:56:26  |

## Challenge 2
- We need to figure out when to schedule an ad campaign
- What day of the week do most users register on?
```mysql
SELECT DAYNAME(created_at) AS day,
       COUNT(*) AS total
  FROM users
 GROUP BY day
 ORDER BY total DESC
 LIMIT 2;
```
| day      | total |
|----------|-------|
| Thursday | 16    |
| Sunday   | 16    |
## Challenge 3
- We want to target our inactive users with an email campaign
- Find the users who have never posted a photo
```mysql
SELECT username
  FROM users u
  LEFT JOIN photos p
    ON u.id = p.user_id
 WHERE p.id IS NULL;
```
| username              |
|-----------------------|
| Aniya_Hackett         |
| Bartholome.Bernhard   |
| Bethany20             |
| Darby_Herzog          |
| David.Osinski47       |
| Duane60               |
| Esmeralda.Mraz57      |
| Esther.Zulauf61       |
| Franco_Keebler64      |
| Hulda.Macejkovic      |
| Jaclyn81              |
| Janelle.Nikolaus81    |
| Jessyca_West          |
| Julien_Schmidt        |
| Kasandra_Homenick     |
| Leslie67              |
| Linnea59              |
| Maxwell.Halvorson     |
| Mckenna17             |
| Mike.Auer39           |
| Morgan.Kassulke       |
| Nia_Haag              |
| Ollie_Ledner37        |
| Pearl7                |
| Rocio33               |
| Tierra.Trantow        |

## Challenge 4
- We're running a new contest to see who can get the most likes on a single photo.
- Who won?
```mysql
SELECT username,
       p.id,
       p.image_url,
       COUNT(*) AS total
  FROM photos p
 INNER JOIN likes l
    ON l.photo_id = p.id
 INNER JOIN users u
    ON p.user_id = u.id
 GROUP BY p.id
 ORDER BY total DESC
 LIMIT 1;
```
| username       | id  | image_url           | total |
|----------------|-----|--------------------|-------|
| Zack_Kemmer93  | 145 | https://jarret.name | 48    |

## Challenge 5
- Our investors want to know...
- How many times does the average user post?
```mysql
SELECT (SELECT COUNT(*)
          FROM photos) / (SELECT COUNT(*)
                            FROM users) AS avg;
```
|avg|
|---|
|2.5700|

## Challenge 6
- A brand wants to know which hashtags to use in a post
- What are the top 5 most commonly used hashtags?
```mysql
SELECT t.tag_name,
       COUNT(*) AS total
  FROM photo_tags pt
  JOIN tags t
    ON pt.tag_id = t.id
 GROUP BY t.id
 ORDER BY total DESC
 LIMIT 5;
```
| tag_name | total |
|----------|-------|
| smile    | 59    |
| beach    | 42    |
| party    | 39    |
| fun      | 38    |
| concert  | 24    |

## Challenge 7
- We have a small problem with bots on our site
- Find users who have liked every single photo on the site
```mysql
SELECT username,
       COUNT(*) AS num_likes
  FROM users u
 INNER JOIN likes l
    ON u.id = l.user_id
 GROUP BY l.user_id
HAVING num_likes = (SELECT COUNT(*)
                      FROM photos);
```
| username           | num_likes |
|------------------- |-----------|
| Aniya_Hackett      | 257       |
| Bethany20          | 257       |
| Duane60            | 257       |
| Jaclyn81           | 257       |
| Janelle.Nikolaus81 | 257       |
| Julien_Schmidt     | 257       |
| Leslie67           | 257       |
| Maxwell.Halvorson  | 257       |
| Mckenna17          | 257       |
| Mike.Auer39        | 257       |
| Nia_Haag           | 257       |
| Ollie_Ledner37     | 257       |
| Rocio33            | 257       |
