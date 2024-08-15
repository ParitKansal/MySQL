# MySQL

## Database Creation and Usage

### CREATE DATABASE
```sql
CREATE DATABASE temp;
USE temp;
```

### CREATE TABLE
```sql
CREATE TABLE student (
    id INT PRIMARY KEY,
    name VARCHAR(255)
);
```

## Inserting Data

### INSERT INTO
```sql
INSERT INTO student (id, name)
VALUES (1, 'Parit'),
       (2, 'Shruti');

INSERT INTO table_name (col1, col2, col3) 
VALUES (v1, v2, v3),
       (val1, val2, val3);
```

## Data Types

- **CHAR**: Fixed-length data size  
- **VARCHAR**: Variable-length data size  
- **TEXT**: Large text data  
- **INT, SMALLINT, MEDIUMINT, BIGINT**: Integer types  
- **FLOAT, DOUBLE**: Floating-point numbers  
- **DATE, DATETIME, TIME**: Date and time  
- **BOOLEAN**: True/False values  
- **ENUM**: One of the preset values  
- **SET**: One or many of the preset values

## Signed and Unsigned Integers
```sql
CREATE TABLE student (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    marks INT UNSIGNED
);
```

## Deleting Databases and Tables

### DROP
```sql
DROP DATABASE db_name;
DROP TABLE table_name;
DROP VIEW view_name;
```

## Displaying Databases and Tables

### SHOW
```sql
SHOW DATABASES;
SHOW TABLES;
```

## Conditional Operations

### IF EXISTS / IF NOT EXISTS
```sql
DROP DATABASE IF EXISTS db_name;
DROP VIEW IF EXISTS view_name;
CREATE DATABASE IF NOT EXISTS db_name;
```

## Keys and Constraints

### PRIMARY KEY and AUTO_INCREMENT
```sql
CREATE TABLE student (
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255),
    marks INT UNSIGNED
);
```

### PRIMARY KEY and FOREIGN KEY
```sql
CREATE TABLE student (
    id INT PRIMARY KEY,
    name VARCHAR(255),
    marks INT UNSIGNED,
    course_id INT,
    FOREIGN KEY (course_id) REFERENCES course_table(id)
);
```

### UNIQUE
```sql
CREATE TABLE customer (
    email VARCHAR(1024) UNIQUE
);
```

### CHECK
```sql
CREATE TABLE customer (
    age INT,
    CONSTRAINT age_check CHECK (age > 12)
);
```

### DEFAULT
```sql
CREATE TABLE account (
    saving_rate DOUBLE NOT NULL DEFAULT 4.25
);
```

## Modifying Tables

### ALTER

#### Add Column
```sql
ALTER TABLE table_name
ADD new_col_name datatype,
ADD new_col_name_2 datatype;
```

#### Modify Column
```sql
ALTER TABLE table_name
MODIFY col_name col_datatype;
```

#### Change Column
```sql
ALTER TABLE table_name
CHANGE COLUMN old_col_name new_col_name new_col_datatype;
```

#### Drop Column
```sql
ALTER TABLE table_name
DROP COLUMN col_name;
```

#### Rename Table
```sql
ALTER TABLE table_name
RENAME TO new_table_name;
```

## Querying Data

### SELECT
```sql
SELECT * FROM table_name;
```

### WHERE
```sql
SELECT * FROM customer WHERE age > 18;
```

### BETWEEN
```sql
SELECT * FROM customer WHERE age BETWEEN 0 AND 100;
```

### IN
```sql
SELECT * FROM officers WHERE officer_name IN ('Lakshay', 'Maharana Pratap');
```

### AND/OR/NOT
```sql
SELECT * FROM table_name WHERE cond1 AND cond2;
SELECT * FROM table_name WHERE cond1 OR cond2;
SELECT * FROM table_name WHERE col_name NOT IN (1, 2, 3, 4);
```

### IS NULL
```sql
SELECT * FROM customer WHERE prime_status IS NULL;
```

### Pattern Searching / Wildcards ('%', '_')
```sql
SELECT * FROM customer WHERE name LIKE '%p_';
```

### ORDER BY
```sql
SELECT * FROM customer ORDER BY first_name DESC, second_name ASC;
```

### DISTINCT
```sql
SELECT DISTINCT department FROM worker;
```

### LIMIT
```sql
SELECT * FROM table_name ORDER BY AGE DESC LIMIT 5;
SELECT * FROM table_name ORDER BY AGE DESC LIMIT 2, 1;
```

## Updating Data

### UPDATE
```sql
UPDATE table_name SET col1 = 1, col2 = 'abc' WHERE id = 1;
```

### Update Multiple Rows
```sql
UPDATE student SET standard = standard + 1;
```

### Handling SQL_SAFE_UPDATES
```sql
SET SQL_SAFE_UPDATES = 0;
```

## Deleting Data

### DELETE
```sql
DELETE FROM table_name WHERE id = 1;
```

### DELETE with Constraints

#### DELETE CASCADE
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    delivery_date DATE,
    cust_id INT,
    FOREIGN KEY (cust_id) REFERENCES customer(id) ON DELETE CASCADE
);
```

#### DELETE SET NULL
```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    delivery_date DATE,
    cust_id INT,
    FOREIGN KEY (cust_id) REFERENCES customer(id) ON DELETE SET NULL
);
```

## Replacing Data

### REPLACE INTO
```sql
REPLACE INTO student (id, class) VALUES (4, 3);
REPLACE INTO table_name SET id = 4, class = 3;
```

## Joins

### INNER JOIN
```sql
SELECT column_list FROM table1 
INNER JOIN table2 ON condition1
INNER JOIN table3 ON condition2;
```

### LEFT OUTER JOIN
```sql
SELECT columns FROM table1 
LEFT JOIN table2 ON join_condition;
```

### RIGHT OUTER JOIN
```sql
SELECT columns FROM table1 
RIGHT JOIN table2 ON join_condition;
```

### FULL OUTER JOIN
```sql
SELECT columns FROM table1 AS t1 
LEFT JOIN table2 AS t2 ON t1.id = t2.id
UNION
SELECT columns FROM table1 AS t1 
RIGHT JOIN table2 AS t2 ON t1.id = t2.id;
```

### CROSS JOIN
```sql
SELECT column_list FROM table1 
CROSS JOIN table2;
```

### Joins Without Using Join Keywords
```sql
SELECT artist_name, album_name, year_recorded
FROM artist, album
WHERE artist.id = album.artist_id;
```

## Set Operations

### UNION
```sql
SELECT * FROM table1
UNION
SELECT * FROM table2;
```

### INTERSECT
```sql
SELECT DISTINCT column_list 
FROM table1 
INNER JOIN table2 
ON table1.column = table2.column;
```

### MINUS
```sql
SELECT * 
FROM table1
LEFT JOIN table2 
USING (column)
WHERE table2.column IS NULL;
```

## Subqueries

### Subquery Examples
```sql
SELECT * FROM table1 WHERE col1 IN (SELECT col1 FROM table2);
SELECT * FROM table1 WHERE col1 > ANY (SELECT col1 FROM table2);
SELECT * FROM table1 WHERE EXISTS (SubQuery);
SELECT MAX(rating) FROM (SELECT * FROM movie WHERE country = 'India') AS temp;
```

## Co-related Subqueries

### Third Largest Age
```sql
SELECT * 
FROM employee e1
WHERE 3 = (
    SELECT COUNT(e2.age)
    FROM employee e2
    WHERE e2.age >= e1.age
);
```

### Third Smallest Age
```sql
SELECT * 
FROM employee e1
WHERE 3 = (
    SELECT COUNT(e2.age)
    FROM employee e2
    WHERE e2.age <= e1.age
);
```

## Views

### CREATE VIEW
```sql
CREATE VIEW view_name AS 
SELECT sr_no, first_name FROM student;
SELECT * FROM view_name;
```

## Utility Functions

### String Functions

- **UPPER('parit')**: Converts all characters in the string to uppercase.
  - Example: `UPPER('parit')` returns `'PARIT'`.

- **LOWER('PARIT')**: Converts all characters in the string to lowercase.
  - Example: `LOWER('PARIT')` returns `'parit'`.

- **SUBSTRING(str, start, length)**: Extracts a substring from a string starting at a specific position for a certain length.
  - Example: `SUBSTRING('Parit', 2, 3)` returns `'ari'`.

- **INSTR(str1, str2)**: Returns the position of the first occurrence of `str2` in `str1`.
  - Example: `INSTR('Parit', 'it')` returns `4`.

- **LTRIM(str)**: Removes leading spaces from a string.
  - Example: `LTRIM('  Parit')` returns `'Parit'`.

- **RTRIM(str)**: Removes trailing spaces from a string.
  - Example: `RTRIM('Parit  ')` returns `'Parit'`.

- **LENGTH(str)**: Returns the length of a string.
  - Example: `LENGTH('Parit')` returns `5`.

- **REPLACE(str1, str2, str3)**: Replaces all occurrences of `str2` in `str1` with `str3`.
  - Example: `REPLACE('Parit', 'a', 'o')` returns `'Porit'`.

- **CONCAT(str1, str2, str3, ...)**: Concatenates multiple strings into one.
  - Example: `CONCAT('Pa', 'rit')` returns `'Parit'`.

---

This guide provides a comprehensive reference for SQL commands and functions.
