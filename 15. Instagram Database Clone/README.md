# Instagram Database Clone
## Schema
Our instagram clone will follow this schema:

![schema](https://github.com/ndomah/MySQL-Bootcamp-Go-from-SQL-Beginner-to-Expert/blob/main/15.%20Instagram%20Database%20Clone/ig_clone.png)

## Relationships
- One-to-Many (1:n):
  - `users` --> `photos` (one user can have many photos)
  - `users` --> `comments` (one user can make many comments)
  - `photos` --> `comments` (one photo can have many comments) 
- Many-to-Many (m:n):
  - `users` <-> `photos` (through `likes`)
  - `users` <-> `users` (through `follows`)
  - `photos` <-> `tags` (through `photo_tags`)
