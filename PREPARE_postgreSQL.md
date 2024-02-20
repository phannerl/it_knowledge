**PREPARE** — prepare a statement for execution
=> PREPARE name [ ( data_type [, ...] ) ] AS statement

Description: 
  - PREPARE creates a prepared statement
  - A **prepared statement** is a server-side object that can be used to optimize performance
  - When the PREPARE statement is executed, the specified statement is parsed, analyzed, and rewritten. When an EXECUTE command is subsequently issued, the prepared statement is planned and executed
  - Prepared statements only last for the duration of the current database session. When the session ends, the prepared statement is forgotten, so it must be recreated before being used again.
  - Prepared statements can be manually cleaned up using the DEALLOCATE command.
Exmaples:
  ```
    PREPARE fooplan (int, text, bool, numeric) AS
      INSERT INTO foo VALUES($1, $2, $3, $4);
    EXECUTE fooplan(1, 'Hunter Valley', 't', 200.00);
  ```
  ```
    PREPARE usrrptplan (int) AS
      SELECT * FROM users u, logs l WHERE u.usrid=$1 AND u.usrid=l.usrid
      AND l.date = $2;
    EXECUTE usrrptplan(1, current_date);
  ```