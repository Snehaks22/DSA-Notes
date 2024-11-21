# SQL
- SQL stands for Standard Query Language
- It is launched by IBM
- Standard way to query/add/delete/modify etc.
- Domain specific language
     - a computer language that's designed for a specific application domain, or problem space
- Declarative programming language
     - a style of programming that focuses on the desired outcome of a program, rather than the steps required to achieve it
- Online Tutorial
    - https://sqlzoo.net/wiki/SQL_Tutorial
- SQL keywords are NOT case sensitive
   - select is the same as SELECT
- Semicolon is the standard way to separate each SQL statement in database systems that allow more than one SQL statement to be executed in the same call to the server.
- The PRIMARY KEY constraint uniquely identifies each record in a table.
Primary keys must contain UNIQUE values, and cannot contain NULL values.
A table can have only ONE primary key; and in the table, this primary key can consist of single or multiple columns (fields)
#### SELECT
- The SELECT statement is used to select data from a database.
- SELECT * select all columns from the table
- FROM is a keyword used to specify which table to select or delete data from.
  - eg: SELECT * FROM world; #gives all the columns from the table world
#### LIMIT,OFFSET
view information like a page by page fashion
        - e.g. flipkart view gadgets by price/review

    - SELECT name, rankscore FROM movies LIMIT 20;
    - SELECT name, rankscore FROM movies LIMIT 20 OFFSET 40;

#### ORDER BY
- default sorting order in ascending
   
      - SELECT name, year FROM movies ORDER BY year DESC LIMIT 10;

#### DISTINCT
- Can be used to find distinct values with in a columns

      - SELECT DISTINCT genre FROM movie_genres;

##### Comparison Operator =,<> or !=, <,<=,>,>=
##### NULL: does not exist/unknown/missing
- "=" does not work with NULL, will give you an empty set
##### LOGICAL OPERATORS
- AND, OR, NOT, ALL, ANY, BETWEEN, EXIST, IN, LIKE, SOME 
##### AGGREGATE FUNCTIONS 
- COUNT, MAX, MIN, AVG, SUM
#### GROUP BY
- often used with COUNT, MIN, MAX, or SUM
- if grouping columns contain NULL values, all null values are grouped together
#### HAVING
    
- Specifiy a condition on groups using HAVING

      - e.g. SELECT year, COUNT(year) year_count FROM movies GROUP BY year HAVING year_count>1000;

##### Order or execusion
1. GROUP BY to create groups 
2. apply the aggregate functions
3. apply having condition
#### JOIN
- combine data in mutiple tables
- EX: TABLE A
     | ID | NAME    |
     | -- | ------- |
     | 1  | ALICE   |
     | 2  | BOB     |
     | 3  | CHARLIE |

   TABLE B
     | ID | COURSE  |
     | -- | ------- |
     | 2  | MATHS   |
     | 3  | SCIENCE |
     | 4  | HISTORY |
  - ##### INNER JOIN
    EX:
    
        -SELECT A.ID, A.name, B.course
         FROM TableA 
         INNER JOIN TableB 
         ON A.ID=B.ID 
  OUTPUT:
     | ID | NAME    | COURSE  |
     | -- | ------- | ------  |
     | 2  | BOB     | MATHS   |
     | 3  | CHARLIE | SCIENCE |
     

  - ##### LEFT JOIN
    EX:
    
        -SELECT A.ID, A.name, B.course
         FROM TableA 
         LEFT JOIN TableB 
         ON A.ID=B.ID 
    OUTPUT:
     | ID | NAME    | COURSE  |
     | -- | ------- | ------  |
     | 1  | ALICE   | NULL    |
     | 2  | BOB     | MATH    |
     | 3  | CHARLIE | SCIENCE |
    
  - ##### RIGHT JOIN
    EX:

        -SELECT A.ID, A.name, B.course
         FROM TableA 
         RIGHT JOIN TableB 
         ON A.ID=B.ID 
    OUTPUT:
     | ID | NAME    | COURSE  |
     | -- | ------- | ------  |
     | 2  | BOB     | MATH    |
     | 3  | CHARLIE | SCIENCE |
     | 4  | NULL    | HISTORY |
    
  - ##### FULL OUTER JOIN
    EX:

         -SELECT A.ID, A.name, B.course
          FROM TableA 
          FULL OUTER JOIN TableB 
          ON A.ID=B.ID 
    OUTPUT:
     | ID | NAME    | COURSE  |
     | -- | ------- | ------  |
     | 1  | ALICE   | NULL    |
     | 2  | BOB     | MATH    |
     | 3  | CHARLIE | SCIENCE |
     | 4  | NULL    | HISTORY |

    - ##### NATURAL JOIN
    - Same function as inner join.But,we don't need to mention the condition.

          -SELECT *
           FROM TableA
           NATURAL JOIN TableB
      OUTPUT:
       | ID | NAME    | COURSE  |
       | -- | ------- | ------  |
       | 2  | BOB     | MATHS   |
       | 3  | CHARLIE | SCIENCE |
    
#### CREATE, READ, UPDATE, DELETE (CRUD)

#### CREATE
    - CREATE TABLE table_name (
    col1 col1_dtype,
    col2 col2_dtype,
    );

    CREATE TABLE students (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    age INT,
    grade CHAR(1)
    );



#### INSERT

    - INSERT INTO movies(id, name, year, rankscore) VALUES (412321, 'Thor', 2011, 7);

    - INSERT INTO movies(id, name, year, rankscore) VALUES (412321, 'Thor', 2011, 7),
                                                           (412322, 'Iron Man', 2008, 7.9),
                                                           (412323, 'Iron Man 2', 2010, 7);
    - INSERT INTO students (id, name, age, grade) 
      VALUES (1, 'John Doe', 20, 'A');
      
    - INSERT INTO students (id, name, age, grade) 
        VALUES 
            (2, 'Jane Smith', 22, 'B'),
            (3, 'Mark Brown', 19, 'A');


#### UPDATE

    - UPDATE <TableName> SET col1=val1, col2=val2 WHERE condition;
    - UPDATE movies SET rankscore=9 where id=412321;
- Can be used to update multiple rows at once

      - UPDATE students 
        SET grade = 'A+' 
        WHERE id = 2;

      - UPDATE students 
        SET age = 21, grade = 'B+' 
        WHERE name = 'Mark Brown';

#### ALTER: The ALTER TABLE statement is used to modify the structure of the table.
- Adding new columns

      - ALTER TABLE students 
          ADD email VARCHAR(100);
- Rename column

       - ALTER TABLE students 
         RENAME COLUMN grade TO final_grade;



#### DELETE
    - DELETE FROM movies WHERE id=412321


#### DROP
- Deletes both tableand all of the data permanently
    
      - DROP TABLE Tablename;
      - DROP TABLE tablename IF EXISTS;

#### TRUNCATE
- TRUNCATE delete the contents of the table but the not the table
- where as DROP deletes the whole table itself
    
      - TRUNCATE TABLE tablename;
