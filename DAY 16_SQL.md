
----- Continued from DAY 15 --------

- **AGGREGATE FUNCTIONS** 
        
  They allow us to perform calculations on sets of data within a table. These functions are often used in conjunction with the `GROUP BY` clause to operate on groups of rows.       
     1. **COUNT()**
     
    The  `COUNT()`  function is used to count the number of rows in a set, satisfying a given condition.
        

      SELECT COUNT(*) FROM movies;
      SELECT COUNT(*) FROM movies where year>2000;
      SELECT COUNT(year) FROM movies;
        
     2. **SUM()**
     
    The  `SUM()`  function calculates the sum of values in a numeric column.
          
          SELECT  SUM(grade)  FROM students;
     3. **AVG()**

     The  `AVG()`  function calculates the average of values in a numeric column.     
           
          SELECT  AVG(grade)  FROM students;
        
     4. **MIN()**

    The  `MIN()`  function returns the minimum value in a set of values.
           
           SELECT MIN(year) FROM movies;
     
     5. **MAX()**

    The  `MAX()`  function returns the maximum value in a set of values.
           
           SELECT MAX(year) FROM movies;
           
- **GROUP BY**

  - The `GROUP BY` clause is used to group rows that have the same values in specified columns. This is often used in conjunction with aggregate functions, such as `COUNT,`  `SUM,`  `AVG,`  `MAX,` or `MIN,` to perform calculations on each group of rows.
  - If grouping columns contain NULL values, all null values are grouped together

         SELECT year, count(year) FROM movies GROUP BY year; # to know #ofmovies released/year
         SELECT year, count(year) year_count FROM movies GROUP BY year ORDER BY year_count;here year_count is an alias

- **HAVING**
    - The  `HAVING`  clause is used in conjunction with the  `GROUP BY`  clause to filter the results of a query based on aggregate functions.

    - The  `HAVING`  clause is applied after the  `GROUP BY`  clause and allows you to specify conditions for groups of rows. It is primarily used with aggregate functions like  `SUM,`  `COUNT,`  `AVG,`  etc.
            
             - Print years which have>1000 movies in our DB
             - Specifiy a condition on groups using HAVING
             - SELECT year, COUNT(year) year_count FROM movies GROUP BY year HAVING year_count>1000;

 - **HAVING Vs  WHERE** 
    - HAVING is often used with GROUP BY but not mandatory.
       
          - SELECT name, year FROM movies HAVING year>2000;
    - HAVING without GROUP BY is same as WHERE
    - WHERE is applied on individual rows while HAVING is applied on groups
    - HAVING is applied after grouping while WHERE is used before grouping
            
            - SELECT year, COUNT(year) year_count, FROM movies, WHERE rankscore>9, GROUP BY year, HAVING year_count>20;

## Order of KEYWORDS
 - https://dev.mysql.com/doc/refman/8.4/en/select.html
![Image](https://storage.googleapis.com/download/storage/v1/b/designgurus-prod.appspot.com/o/372b6b2ec73ef416f8caef905?generation=1705390601790955&alt=media)


## JOINS

SQL Joins helps  to combine data from different tables in a database. They bring together data from different tables based on a common attribute, creating a seamless connection between them.

![Image](https://storage.googleapis.com/download/storage/v1/b/designgurus-prod.appspot.com/o/6e07a16551265abb03d79a404?generation=1705354279437564&alt=media)
- **INNER JOIN** 

Fetches rows where there is a match in both tables based on a specified condition. It's straightforward and effective, just like finding your perfect match.

       SELECT A.ID, A.name, B.course
       FROM TableA A
       INNER JOIN TableB B
       ON A.ID=B.ID
       
- **NATURAL  JOIN**

Automatically matches columns with the same name in both tables. In other words, it relies on the commonality of column names to establish the join condition. While it offers a convenient way to join tables, it's essential to use Natural Joins cautiously, as it may lead to unintended matches if the column names are not unique or if changes occur in the table structure.

       SELECT *
       FROM TableA
       NATURAL JOIN TableB;


 - **LEFT JOIN** 

Fetches all rows from the left table and matching rows from the right table. If there's no match, the result will show NULL values for the right table columns.

       SELECT A.ID, A.name, B.course
       FROM TableA A
       LEFT JOIN TableB B
       ON A.ID=B.ID

- **RIGHT JOIN** 

Focuses on the right table, ensuring that all rows from the right table are included, along with matching rows from the left table.

      SELECT A.ID, A.name, B.course
      FROM TableA A
      RIGHT JOIN TableB B
      ON A.ID=B.ID

- **FULL OUTER JOIN**

It is the ultimate gathering, showcasing all rows from both tables, with matches displayed where they occur and NULL values where there's no match. It's like bringing everyone together for a grand reunion.

      SELECT A.ID, A.name, B.course
      FROM TableA A
      FULL OUTER JOIN TableB B
      ON A.ID=B.ID

## Data Manipulation Language (DML)

- **INSERT**

The `INSERT` statement in SQL adds new records to a table. It allows you to specify the values for each column or insert data into the table.

       - INSERT INTO movies(id, name, year, rankscore) VALUES (412321, 'Thor', 2011, 7);
       - INSERT INTO movies(id, name, year, rankscore) VALUES (412321, 'Thor', 2011, 7), (412322, 'Iron Man', 2008, 7.9), (412323, 'Iron Man 2', 2010, 7);
       - INSERT INTO students (id, name, age, grade) VALUES (1, 'John Doe', 20, 'A');
       - INSERT INTO students (id, name, age, grade) VALUES (2, 'Jane Smith', 22, 'B'), (3, 'Mark Brown', 19, 'A');

- **UPDATE**

The `UPDATE` statement in SQL is used to modify existing records in a table. It allows you to change the values of one or more columns in a specific row.

       - UPDATE <TableName> SET col1=val1, col2=val2 WHERE condition;
       - UPDATE movies SET rankscore=9 where id=412321; (# Can be used to update multiple rows at once)
       - UPDATE students SET grade = 'A+' WHERE id = 2;
       - UPDATE students SET age = 21, grade = 'B+' WHERE name = 'Mark Brown';
    
- **DELETE**

The `DELETE` statement in SQL removes one or more records from a table based on a specified condition.
    
       - DELETE FROM movies WHERE id=412321

 ## Data Definition Language (DDL)
     
- **CREATE**

In SQL, the `CREATE` statement is used to create various database objects, i.e., tables, indexes, or the database itself.

      - CREATE TABLE table_name ( col1 col1_dtype, coL2 col2_dtype );
      - CREATE TABLE students (id INT PRIMARY KEY, name VARCHAR(50), age INT, grade CHAR(1));


- **ALTER**

The ALTER TABLE statement is used to modify the structure of the table. It allows you to add, modify, or drop columns, constraints, or other elements of a table without having to drop and recreate the entire table.
            
      - Adding new columns :
         ALTER TABLE students ADD email VARCHAR(100);
      - Rename column :  ALTER TABLE students 
         RENAME COLUMN grade TO final_grade;
     
- **DROP**

  Deletes both table and all of the data permanently
         
           - DROP TABLE Tablename;
           - DROP TABLE tablename IF EXISTS;

- **TRUNCATE**

  TRUNCATE delete the contents of the table but the not the table where as DROP deletes the whole table itself
         
         - TRUNCATE TABLE tablename;
