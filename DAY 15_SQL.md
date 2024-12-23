## Database Management System (DBMS)
- A Database Management System (DBMS) is a software system that allows users to create, store, organize, and access data in a database. It can be divided into Relational and Non Relational DBMS.

### Relational DBMS  

  - An RDBMS, or Relational Database Management System, is a type of database management system (DBMS) that stores data in a structured format, using rows and columns.
    - Example Databases : Oracle, MySQL, SQL Server

 ###  Non-Relational DBMS
 - Non-relational database  offers more flexibility by storing data in various formats like documents, key-value pairs, or graphs, allowing for less structured and more dynamic data sets.
- Example : MongoDB (NoSQL)

    ## Tables
 - In a relational database all of our data is stored in tables.
                
                - movie_id    movie_name    year      actor_id    actor_name     gender
                   1          Spiderman     2009      aid_1        name          Male
                   1          Spiderman     2009      aid_2        name          Male

  - In this table there is lot of data that is redundant which makes it inefficient while interacting with database as well as during storage 

 - Therefore in RDBMS data is stored across multiple tables to avoid data duplication.

            - Table 1: movie_id, movie_name, year
            - Table 2: actor_id, actor_name, gender
            - Table 3: movie_id, actor_id
            - Here movie_id and actor_id are unique

  - There is a Primary Key associated with each table, they cannot have null values and have unique values.
  - Also there will be a Foreign Key associated with each table that can link with other tables effectively.

## Why SQL? 
   - SQL, or Structured Query Language, is a programming language that manages and manipulates relational databases.. It performs tasks such as querying data, updating records, inserting data, and deleting data in a relational database management system (RDBMS).
  - SQL is not a general purpose programming language, it is domain specific language.
- SQL is declarative programming language.

![Image](https://storage.googleapis.com/download/storage/v1/b/designgurus-prod.appspot.com/o/df38494d3f7509d1a695f5700?generation=1718858518601123&alt=media)

## Execution of an SQL statement
    - The execution follows the following actions
    - SQL->parser,compiler: tries to understand the query
         ->query optimizer: (optimal way to execute) & generates code
         ->query executer->DB->results
         
## Creating Database and Interacting Through Terminal  
       
- Loading data.

             mysql -u username -p password # Accessing MySql in terminal
             CREATE DATABASE imdb;
             USE imdb;
             source /path/to/imdb.sql;
             SHOW tables; 


- USE,  DESCRIBE,  SHOW Tables
  
    - **USE** <DB NAME>  # To use the DB for further operations
    - **SHOW** tables;     # To see created tables
    - **DESCRIBE** <table_name>;    # shows the schema of a particular table
       
 ## Data Query Language (DQL)
- DQL is used to fetch the data from the database.
- **SELECT**
    - The SELECT statement allows you to fetch data from one or more columns of a table, making it an essential tool for data retrieval.
    -
           SELECT * FROM movies;
    - In reality there will be tables with 100's of columns. "*" indicates selecting all columns at once.
           
           SELECT name, year FROM movies;
        
    - The output row order is same as the one in the table.
    
- **LIMIT, OFFSET**
    -  View information like a page by page way,( e.g. flipkart view gadgets by price/review.)
    - LIMIT function limits the anchors the no. of rows fetched to the desired no. 
    - OFFSET function allows to remove the desired no. of rows from the result and fetch the remaining.
    
               - SELECT name, rankscore FROM movies LIMIT 20;
               - SELECT name, rankscore FROM movies LIMIT 20 OFFSET 40;


- **ORDER BY**
  - The `ORDER BY` clause is used to sort the result set of a query based on one or more columns. It is typically used with the `SELECT` statement to arrange the rows in a specific order.
  
         - SELECT name, year FROM movies ORDER BY year DESC LIMIT 10;
  - Default sorting order in ascending.
  - The output row order may not be same as the one in the table due to query optimizer and internal data-structures/indices.
    
- **DISTINCT**
    - The `DISTINCT` keyword is used in the `SELECT` statement to eliminate duplicate rows from the result set. It is commonly used when you want to retrieve unique values from a specific column or a combination of columns in a table.
    
           - SELECT DISTINCT genre FROM movie_genres;
           - SELECT DISTINCT first_name, last_name FROM directors ORDER BY first_name;

- **WHERE**
   - The `WHERE` clause is used to filter the rows returned by a `SELECT`, `UPDATE`, or `DELETE` statement. It allows you to specify a condition that must be met for a row to be included in the result set.
             
             - SELECT name, year, rankscore FROM movies WHERE rankscore>9;
             - SELECT name, year, rankscore FROM movies WHERE rankscore ORDER BY rankscore DESC  LIMIT 10;
    - Conditions can be TRUE, FALSE, NULL
 - **COMPARISON OPERATORS** 
    - =,<> or !=, <,<=,>,>=
    - SELECT * FROM movie_genres WHERE genre='Comedy';
    - SELECT * FROM movie_genres WHERE genre<>'Horror';
   
  - **NULL**
    -  Null values in MySQL indicate the absence of a value in a column. 
    -  Unlike an empty string or zero, null is not a valid data value and typically represents missing or unknown information. 
    - Columns in a MySQL table can be defined to allow or disallow null values based on the data requirements.
    - 
          - SELECT name, year, rankscore FROM movies WHERE rankscore=NULL;
          - SELECT name, year, rankscore FROM movies WHERE rankscore IS NULL;
          - SELECT name, year, rankscore FROM movies WHERE rankscore IS NOT NULL;

- **LOGICAL OPERATORS**
    - AND, OR, NOT, ALL, ANY, BETWEEN, EXIST, IN, LIKE, SOME
    
          - SELECT name, year, rankscore FROM movies WHERE rankscore>9 AND year>2000;
          - SELECT name, year FROM movies WHERE NOT year<=2000 LIMIT 20;
