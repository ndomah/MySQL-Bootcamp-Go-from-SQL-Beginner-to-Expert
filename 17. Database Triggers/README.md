# Database Triggers
## Introduction
- A **trigger** is a set of instructions that are automatically executed (or "triggered") when a specific event occurs on a table, such as `INSERT`, `UPDATE`, or `DELETE`
- Help enforce business rules, validate data, and maintain database integrity.

**Syntax**
```mysql
CREATE TRIGGER trigger_name
    trigger_time trigger_event ON table_name FOR EACH ROW
    BEGIN
        ...
    END;
```
- `trigger_time`: `BEFORE`, `AFTER`
- `trigger_event`: `INSERT`, `UPDATE`, `DELETE`

## Example 1
### A Simple Validation
```mysql
DELIMITER $$

CREATE TRIGGER must_be_adult
     BEFORE INSERT ON users FOR EACH ROW
     BEGIN
          IF NEW.age < 18
          THEN
              SIGNAL SQLSTATE '45000'
                    SET MESSAGE_TEXT = 'Must be an adult!';
          END IF;
     END;
$$

DELIMITER ;
```
### Explanation
- `DELIMITER $$` / `DELIMITER ;`
  - `DELIMITER` changes the command delimiter temporarily to `$$`. This is necessary because the trigger definition contains multiple SQL statements inside the `BEGIN...END` block, and using `;` would prematurely end the trigger creation
  - After the trigger definition, the delimiter is reset back to the default `;`

- `CREATE TRIGGER must_be_adult`
  - Defines a new trigger named `must_be_adult`.

- `BEFORE INSERT ON users`
  - Specifies that the trigger should fire **before** an `INSERT` operation on the `users` table.
  - This means the trigger checks the condition before inserting data, and can prevent the insertion if conditions are not met.

- `FOR EACH ROW`
  - Ensures the trigger runs **for each row** being inserted into the table, not once per `INSERT` statement.

- `BEGIN ... END`
  - This block contains the trigger logic and allows the execution of multiple SQL statements inside.

- `IF NEW.age < 18 THEN`
  - Checks if the value of the `age` column in the new row (`NEW.age`) being inserted is less than 18.

- `SIGNAL SQLSTATE '45000'`
  - Generates a custom SQL error to prevent the insertion when the age condition is not met.
  - `SQLSTATE 45000` is a generic error code used for custom-defined exceptions.

- `SET MESSAGE_TEXT = 'Must be an adult!';`
  - Sets the error message that will be returned to the user, explaining why the insertion was blocked.
### Example Usage
**Attempt to Insert an Underage User:**
```mysql
INSERT INTO users (username, age) VALUES ('young_user', 16);
```
**Expected Output:**
```mysql
ERROR 1644 (45000): Must be an adult!
```
## Example 2
### Preventing Self-Follows
```mysql
DELIMITER $$

CREATE TRIGGER example_cannot_follow_self
     BEFORE INSERT ON follows FOR EACH ROW
     BEGIN
          IF NEW.follower_id = NEW.following_id
          THEN
               SIGNAL SQLSTATE '45000'
                    SET MESSAGE_TEXT = 'Cannot follow yourself, silly';
          END IF;
     END;
$$

DELIMITER ;
```
- Ensures that a user cannot follow themselves in the `follows` table by checking if the `follower_id` is the same as the `following_id`
- If the condition is met, an error message is triggered to prevent the insertion
### Example Usage
#### Valid Case (User follows another user):
```mysql
INSERT INTO follows (follower_id, following_id) VALUES (1, 2);
```
Result: The row is successfully inserted
#### Invalid Case (User tries to follow themselves):
```mysql
INSERT INTO follows (follower_id, following_id) VALUES (1, 1);
```
**Expected Output:**
```mysql
ERROR 1644 (45000): Cannot follow yourself, silly
```
- The insertion is blocked, and the custom error message is shown
## Example 3
### Logging Unfollows
```mysql
DELIMITER $$

CREATE TRIGGER create_unfollow
    AFTER DELETE ON follows FOR EACH ROW 
BEGIN
    INSERT INTO unfollows
    SET follower_id = OLD.follower_id,
        followee_id = OLD.followee_id;
END$$

DELIMITER ;
```
- Trigger named `create_unfollow` automatically logs an **"unfollow"** action into the `unfollows` table **after** a row is deleted from the `follows` table
- This ensures a historical record is maintained when users unfollow others
### Example Usage
**Initial state of `follows` table:**
```mysql
SELECT *
FROM follows;
```
|follower_id|followee_id|
|---|---|
|1|2|
|3|4|

**Deleting a follow relationship:**
```mysql
DELETE FROM follows WHERE follower_id = 1 AND followee_id = 2;
```
- The deleted row `(1, 2)` is automatically inserted into the `unfollows` table
**Contents of the `unfollows` table after ther trigger execution:**
```mysql
SELECT *
FROM unfollows;
```
|follower_id|followee_id|
|---|---|
|1|2|
## Managing Triggers
### Listing Triggers
```mysql
SHOW TRIGGERS;
```
### Removing Triggers
```mysql
DROP TRIGGER trigger_name;
```

*WARNING: Triggers can make debugging hard!*
