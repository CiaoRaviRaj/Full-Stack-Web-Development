* # MySQL
    * Introduction
        * SQL => Structured Query Language
        * 1970 => EF Codd => Relational Model(Relational algebra) => IBM => (SEQUEL) => SQL
        * (RDBMS) Relational Database Management System => all table are intern-related with each other
        * CORRECT SQL KEYWORD ORDER
            * SELECT ...
            * FROM ...
            * WHERE ...
            * GROUP BY ...
            * HAVING ...
            * ORDER BY...

    * features
        * domain-specific language
            * Table - relation table
        * declarative language
            * what to do only
        * DDL , DML, DCL, TCL command
        * Keys and Constraints
            * primary key and foren
        * Operators
            * like, between, In , Not in, 
            * Condition (CASE THEN END), Exist/Not exist
        * Clauses
            * distinct, order by, group by , from
        * aggregate function
            * max(), Sum(), Count()
            * window functions
        * joins and nested Queries
        * PL SQL
            * Triggers function, VIEW , Cursor , procedures
    * SQL Commands 
        * DDL (Data Definition language)
            * it deals with structure / schema (table) of database
            * Create
                * CLI 
                    * roots
                        * New
                            * createDatabase => create
                * SQL Commands
                    * CREATE DATABASE aFirst => go

                * Create Table
                    * CLI
                        * database/new
                            * table name => TableName
                            * Name(id) Type(INT) LengthValues Default(None) Collation Attributes Null Index(PRIMARY) AI(Click) Comments
                            * Name(name) Type(VARCHAR) LengthValues(30) Default(None) Collation Attributes Null Index(PRIMARY) AI() Comments
                            * Name(gender) Type(ENUM) LengthValues('Female','Male') Default(As defined(Male)) Collation Attributes Null Index(PRIMARY) AI() Comments
                            ...
                            * Name(create_at) Type(TIMESTAMP) LengthValues Default(None) Collation Attributes Null Index(PRIMARY) AI() Comments
                            * Name(modified_at) Type(TIMESTAMP) LengthValues Default(CURRENT_TIME) Collation Attributes Null Index(PRIMARY) AI() Comments

                    * SQL Commands
                        * in Database 
                            * CREATE TABLE TableName {
                                id INT(6) UNSIGNED AUTO_INCREMENT PRIMARY KEY,
                                firstName VARCHAR(30) NOT NULL,
                                lastName VARCHAR(30) NOT NULL,
                                email VARCHAR(50),
                                reg_data TIMESTAMP DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
                            }


            * Alter
                * adding A new field
                    * Database => structure 
                        * Add(1) column(s)(after ColumnName) => Go
                        * Name(id) Type(INT) LengthValues Default(None) Collation Attributes Null Index(PRIMARY) AI(Click) Comments
                    * SQL Commands
                        * ALTER TABLE 'tableName' ADD 'NewColumnName' Type Not NULL AFTER 'ColumnName';
                        * for multiple Number
                            * ALTER TABLE 'tableName' ADD 'NewColumnName1' Type Not NULL AFTER 'ColumnName', ADD 'NewColumnName' Type Not NULL AFTER 'NewColumnName1';
                * DROP Column Name
                    * ALTER TABLE "tableName" DROP 'columnName'
                * for Change Column Attributes
                    * STRUCTURE => change
                    * SQL
                        * ALTER TABLE 'TableName' CHANGE "ColumnName" 'newColumnName' VARCHAR(14) ... NOT NULL



            * Drop
                * DROP DATABASE aFirst
                * DROP TABLE TableName
                * ALTER TABLE "tableName" DROP 'columnName'
            * Truncate
                * it is used to delete data from a table
                * Truncate Table table_name;
            * Rename
            * BACKUP
                * BACKUP DATABASE databasename
                    TO DISK = 'filepath';
        * DML (Data Manipulation language)
            * it deals with data fetch and data change on database
            * Select
                * To Fetch data
                    * SELECT * from TableName
                    * SELECT fieldName1 as (ReName in OutPut) , fieldName2, fieldName3 from TableName;
                    * FETCH DISTINCT
                        * SELECT DISTINCT 'fieldName' from 'TableName'
                    * Count column
                        * SELECT count(*) as total FROM 'TableName'
                    * Count with Distinct
                        * * SELECT count(DISTINCT 'fieldName') as total FROM 'TableName'
                * with Where AND OR
                    * SELECT * FROM 'tableName' Where name = "hello"
                    * SELECT * FROM 'tableName' Where email = "hello@gmail.com" AND gender = "Female"
                    * SELECT * FROM 'tableName' Where name="last" OR gender = 'Female' OR phone_no = '7899'
            * Insert
                * INSERT INTO TableName (fieldNames...)
                    VALUES(fieldNameValues...);
                    * for multiple data
                        VALUES(fieldNameValues1...),
                        (fieldNameValues2...),
                        (fieldNameValues3...);
                * INSERT INTO set name= 'Last' , email= "...", gender="Male", PhoneNumber = "..."
            * update
                * UPDATE 'TableName' SET fieldName1 = 'name' , fieldName1 = 'name', fieldName1 = 'name' Where id = 4
            * Delete
                * DELETE FROM 'TableName' Where id = 4
        * DCL (Data Control Language)
            * auth/permission for use of function
            * Grant
                * give permissions
            * Revoke
                * take permission
        * TCL (Transaction Control Language)
            * DML commands are tampere
            * transition data 
            * AUTO_COMMIT - by default
            * to make transaction work
                * START TRANSACTION;
                * it start a AUTO_COMMIT OFF FOR THIS WINDOW
                * What ever do in this window is not auto commit in table, NEED TO manually commit the change.
                * so to commit change 
                * COMMIT;
            * commit
                * for success transition
            * Rollback
                * for fail transition
                * START TRANSITION
                * make change 
                * but you want to go back to initial state
                * ROLLBACK;
                * it Rollback at state where last commit it made
            * SavePoint
                * for portion of state to save 
                * at 30%, 50% 
                * it is used to make SAVEPOINT for our data
                * START TRANSACTION
                * SAVEPOINT first;
                    * make CHANGES
                * SAVEPOINT second;
                    * make changes..
                * SAVEPOINT third;
                    * change changes..
                * ROLLBACK second;
                    * it rollback our state to named savepoint;
        * Constraints
            * Rules for data entering
            * Primary key
                * It is uniquely Identify
                
            * Foreign key
                * tableSecond/Structure/RelationView
                    * columnName(foreignKey) DatabaseName TableFirst column
                        * ON DELETE => RESTRICT //it is restrict to parent 
                        * ON UPDATE => RESTRICT => 
                        * ON DELETE => CASCADE // On update on parent it show on child
                        * ON UPDATE => CASCADE
                        * ON DELETE => SET NULL // On DELETE on parent data it show on NULL on Child
                        * ON UPDATE => SET NULL 
                * CREATE TABLE Orders (
                    OrderID int NOT NULL PRIMARY KEY,
                    OrderNumber int NOT NULL,
                    PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
                );
                * Now , SQL make sure you always references a person on orders table , it is not allow you to create record with a person_id which is not available in persons table.
                * ALTER TABLE Orders
                    ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);
            * check
                * it used to add check statement into column value enter
            * Unique
            * default
            * Not Null
    * SQL Conditions
        * WHERE
            * SELECT * FROM 'tableName' Where name = "hello"
        * AND
            * SELECT * FROM 'tableName' Where email = "hello@gmail.com" AND gender = "Female"
        * OR
            * SELECT * FROM 'tableName' Where name="last" OR gender = 'Female' OR phone_no = '7899'
    * SQL Clauses
        * distinct
            * SELECT DISTINCT 'fieldName' from 'TableName'
        
        * IS NULL / IS NOT NULL
            * SELECT * FROM 'TableName' Where "phone1" IS NULL AND EXTRA_CONDITION
            * SELECT * FROM 'TableName' Where "phone1" IS NOT NULL AND EXTRA_CONDITION
        * order By
            * SELECT * FROM 'TableName' Where "phone1" IS NOT NULL AND EXTRA_CONDITION ORDER BY FieldName ASC/DESC
    * SQL OPERATORS
        * Comparison Operators
            * =
            * > , < , <= , >= , 
            * <> for not equal
        * Logical Operators
            * Between
                * SELECT * FROM 'TableName' where id BETWEEN 2 AND 5
            * IN
                * SELECT * FROM 'TableName' where id IN(2,4,5,6)
                * SELECT * FROM 'TableName' where name IN('name1','name2',...) 
            * limit
                * SELECT * FROM 'TableName' limit 2;
                * SELECT * FROM 'TableName' limit 1(start - 1), 2(range); //it start form next index value
            * Like
                * include condition
                * SELECT * FROM 'tableName' Where email LIKE '%@gmail.com%' // return email that have include @gmail.com and start with any thing(%__) and end with any thing(__%) 
                * start with test 
                    * SELECT * FROM 'tableName' Where email LIKE 'test_'
                * end with test
                    * SELECT * FROM 'tableName' Where email LIKE '_test'
            * EXISTS
                * SELECT column_name(s)
                    FROM table_name
                        WHERE EXISTS
                            (SELECT column_name FROM table_name WHERE condition);
                * The EXISTS operator returns TRUE if the subquery returns one or more records.
                * then it return all all record as true

            * ANY/SOME
                * it is used with where 
                * if your subQuery return multiple 
                * SELECT ProductName
                    FROM Products
                        WHERE ProductID = ANY (SELECT ProductID FROM OrderDetails WHERE Quantity > 99);
            * ALL
                * it check with all output of subQuery

    * Aggregate function
        * Count
            * SELECT Count(fieldName) from 'tableName'
        * max
            * SELECT max(fieldName) from 'tableName'
        * min 
            * SELECT min(fieldName) from 'tableName'
        * sum
            * SELECT sum(fieldName) from 'tableName'
        * AVG
            * SELECT avg(fieldName) from 'tableName'
        * group by
            * when you have unique id but another use this id as foreign key but have many data
            * it must use group by here
            * ALL column names from the select clause which are not used in aggregate functions must also appear in the GROUP BY clause
            * SELECT COUNT(table2.foreignKey ) as totals,Table1.* FROM Table1 
                LEFT JOIN table2 On table2.foreignKey = Table1 
                GROUP BY Table2.foreignKey 
                ORDER BY Table1.id DESC
        * Having 
            * having is as where condition in group by outcome
            * it make condition on column made by group by
            * SELECT COUNT(table2.foreignKey ) as totals,Table1.* FROM Table1 
                LEFT JOIN table2 On table2.foreignKey = Table1 
                GROUP BY Table2.foreignKey 
                having totals > 2 //
                ORDER BY Table1.id DESC 

    * joins and nested Queries
        * Both tables must have relation
            * SELECT * FROM Table1 
                JOIN Table2 ON condition1 AND condition2
                WHERE Table1 extra condition
        * Inner Join
            TABLE1 AND TABLE2
            * SELECT * FROM 'Table1'
                INNER JOIN 'Table2' ON Table2.foreignKey = Table2 // it return and data of between table 1  and table2 And return Both table data
        * Left Join
            Table1 full with common of table1 and  Table2
            * SELECT * FROM 'Table1'
                LEFT JOIN 'Table2' ON Table2.foreignKey = Table2 // rest are Null
        * Right Join
            * Table2Full with common of Table2 with Table1
            * SELECT * FROM 'Table1'
                RIGHT JOIN 'Table2' ON Table2.foreignKey = Table2 Where Table1.name = "name"// REST ARE NULL
        * FULL OUTER JOIn
            * Table1 or Table2
            * SELECT Table2.* FROM 'Table1'
                RIGHT JOIN 'Table2' ON Table2.foreignKey = Table2 Where Table1.name = "name"// Only return table 2 data/
        * Union
            * to combine many tables data

            * SELECT name from 'table1'
                UNION
                SELECT name from 'table2'
                // it must have equal number of column number
        * UNION ALL
            * all records with double intersect records
        * INTERSECT
            * return only common record
        * EXCEPT/MINUS
            * only return unique in table 1
        * group by
            * when you have unique id but another use this id as foreign key but have many data
            * it must use group by here
            
            * SELECT COUNT(table2.foreignKey ) as totals,Table1.* FROM Table1 
                LEFT JOIN table2 On table2.foreignKey = Table1
                GROUP BY Table2.foreignKey 
                ORDER BY Table1.id DESC
            
        * Having 
            * having is as where condition in group by outcome / aggregated function
            * SELECT COUNT(table2.foreignKey ) as totals,Table1.* FROM Table1 
                LEFT JOIN table2 On table2.foreignKey = Table1 
                GROUP BY Table2.foreignKey 
                having totals > 2 //
                ORDER BY Table1.id DESC 
        * Use join to INTER another table
            * INSERT INTO table3 (name, email) 
                SELECT table1.name,table2.image from table1
                INNER JOIN table2 ON table2.foreignKey = table1.id
        * Use join to UPDATE another table
            * UPDATE table3 
                INNER JOIN table1 ON  table1.id = table3.id
                INNER JOIN table2 ON table2.id = table3.id
                SET table3.phone = table1.phone_no, table3.email = table2.email;
        * use join to DELETE another table
            * to delete all related table record of same id
            * DELETE table3, table2 , table1 table from table3
                INNER JOIN table2 ON table2.id = table3.id
                INNER JOIN table1 ON table1.id = table3.id
                where table3.id = 3

    * CONCAT(),GROUP_CONCAT() ,FIND_IN_SET() AND  DATE_FORMAT
        * CONCAT()
            * To add two field data and show together
            * SELECT CONCAT(name, " " , email) from table1
        * GROUP_CONCAT()
            * if you want show all fieldData enters in one field
            * SELECT GROUP_CONCAT(name) as name FROM 'table1' where id < 4
        * FIND_IN_SET()
            * to find a value in field where multiple value is enter
            * SELECT * FROM table1 WHERE FIND_IN_SET('12' , address)
        * DATA_FORMAT(created_at, "%y- %M -%d) from table1
    * window Functions
        * SELECT 
            e.* ,
            max(salary) OVER( PARTITION BY dept_name) as max_salary
            FROM employee e;
        * it create a separate window for max()
        * OVER tell to create as window function
        * PARTITION BY split that window data on what based
            * that going to apply that window function separately.
        * alternate way of write 
            if you have multiple windows function
            * SELECT * ,
                FIRST_VALUE(product_name)
                    OVER w
                    as most_exp_product,
                LAST_VALUE(product_name)
                    OVER w
                    as least_exp_product
                FROM products
                WINDOW w as (PARTITION BY product_category ORDER BY price DESC
                FRAME...CLause_IF_YOU_NEED)

                
        * ROW_NUMBER
            * SELECT 
                e.*,
                ROW_NUMBER() OVER(PARTITION BY dept_name ORDER BY emp_id) as rm 
                FROM employee e
            * to fetch top 3 employ in particular department
            * SELECT * FROM 
                (
                    SELECT 
                    e.*,
                    ROW_NUMBER() OVER(PARTITION BY dept_name ORDER BY emp_id) as rm 
                    FROM employee e
                ) as x
                WHERE x.rm < 3; // it is also done by rank
        * RANK
            * top 3 in each department
                * SELECT * FROM 
                    SELECT 
                        (e.*,
                        RANK() OVER (PARTITION BY dept_name ORDER BY salary DESC) AS rnk
                        FROM employee e) as x
                        WHERE X.rnk < 3
            * if salary duplicate then it expe
            * DENSE RANK is noy expe
                
        * DENSE RANK

        * LEAD/LAG
            * Higher / lower or equal check on previous record
            * SELECT e.* 
                LAG (salary, 2,0) OVER (PARTITION BY dept_name ORDER BY emp_id) AS prev_emp_salary
                FROM employee e; 
                * similarly, LEAD next value
        * FIRST_VALUE
            * the most expensive product in each partition
            * SELECT * ,
                FIRST_VALUE(Column_Name_you_want to_display_THAT_VALUE) OVER(PARTITION BY product_category ODER BY price DESC) AS most_expensive_Product
                FROM products
        * LAST VALUE 
            * Similarly it return last record value in each partitions
            * it is not doing currently
            * it is due to frame
            * FRAME is record of each window function
            * DEFAULT FRAME clause
                RANGE BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW
                // That new Unbounded row has only record of bonded row previously and check condition on it only That why first record is same and second row compare it with first row only.
            * CHANGE DEFAULT FRAME
                * ....OVER(
                    ....
                    RANGE BETWEEN PRECEDING AND UNBOUNDED FOLLOWING
                ) 
                // now it access of the last record of partition


        * NTH_VALUE
            * similarly like FIRST_VALUE and LAST_VALUE, it return NTH_VALUE
            * ...
                NTH_VALUE(product_name, 3) OVER...
                FROM products
            * if it do not find nth value, it return NULL

        * NTILE
            * group of record in 
            * Q :- Write a query segregate all the expensive phone, mid range phone and the cheaper phone
            * SELECT * ,
                NTILE(3) OVER(ORDER BY price DESC) as buckets
                FROM products
                WHERE product_category ="Phone"
            * let phone has 10 records
                * then the first 4 record have 1  value
                * next 3 record have 2
                * Next 3 record have 3
                * BY this you can category the expensive , mid range and cheaper phone.

        * CUME_DIST
            * it calculate relative contribution of each record in following table
            * Q query to fetch all products which are constituting the first 30% of the data in products tablebased on price
            * cume_dist() return value between 0 and 1
            *   current Row no / total no. of Row
            * SELECT * FROM 
                (SELECT * ,
                    ROUND(CUME_DIST() OVER(ORDER BY price DESC)::numeric * 100, 2) as cume_dist_percentage
                    FROM products
                    // it return % value of contribution it the table.) as x
                WHERE x.cume_dist_percentage < 30
                * it return first 30% cheapest product 
        * PERCENT_RANK
            * it give rank on the based of percentage
            * it also return 
                0 to 1
            * it similar to CUME_DIST()
            * FORMULA
                * CURRENT ROW - 1 / TOTAL ROW - 1
            * SELECT * FROM 
                (SELECT * ,
                    ROUND(CUME_DIST() OVER(ORDER BY price DESC)::numeric * 100, 2) as cume_dist_percentage
                    FROM products
                    // it return % value of contribution it the table.) as x
                WHERE x.product_name = "Galaxy Z Fold 3"
            * it return how much Galaxy Z Fold 3 phone is expensive then other mobile
            

    * CTE
        * COMMON TABLE EXPRESSION
        * temp value that use in SQL
        * WITH cte_name AS (cte query)...;
        * WITH CTE1 AS (SELECT EMP_ID, DEPT_ID FROM EMPLOYEES)
            SELECT * FROM CTE1;

        * WITH CTE2 AS (SELECT DEPT_D, AVG(SALES) AS AVG_SAL FROM EMPLOYEES GROUP BY DEPT_ID)
        SELECT MAX(AVG_SAL) FROM CTE2;
            //it return max of avg_sale of department

    * Trigger
        * After or Before action run on a particular action a table
        * CLI
            * table -> More -> Trigger
                * TriggerName
                * TableName
                * Time => Before/After
                * Event => Insert/(Delete)/UPDATE
                * Definition => 
                    INSERT INTO USER SET name = OLD.name, email = OLD.email
                * definer : root
        * SQL command
            * CREATE DEFINER="root" TRIGGER 'triggerName' BEFORE EVENT_NAME ON TABLE_NAME FOR EACH ROW INSERT INTO NewTable SET name = OLD.name, email = OLD.email
            * CREATE TRIGGER
                TRIGER_NAME
                BEFORE
                UPDATE
                ON TABLE_NAME
                FOR EACH ROW
                    INSERT INTO NEW_TABLE
                        SET name = OLD.name, email = OLD.email
    * Views
        * output of join 2 and more tables
        * CREATE VIEW VIEW_NAME AS
            SELECT * FROM 'table1'
            LEFT JOIN table2 ON table2.id = table1.id
            GROUP BY table2.id 
            ORDER BY table1.id ASC
    * CASE Function 
        * if you want to change gender option as 
            Male => M
            Female => F
            Then you should use case
        * SELECT (CASE 
            WHEN gender = 'Male' THEN 'M" 
            WHEN gender = 'Female' THEN 'F"
            ELSE 'NA' END) as genders, table.*
            FROM 'TABLE_NAME'
        * count with case
            * SELECT COUNT((CASE WHEN gender = 'Male' THEN gender = "M" END ) as male) from Table1
        * if you want to set distinct phone number on case male check
            * SELECT 
                COUNT (DISTINCT 
                    (CASE WHEN gender = "Male" THEN phone_no END) )as Males, 
                COUNT (DISTINCT 
                    (CASE WHEN gender = "Female" THEN phone_no END) )as Females
                FROM table1 HAVING Males IS NOT NULL OR Females IS NOT NULL
    * SELF JOIN
        * When in a table there is a field which is refer by another field 
        * SELECT t1.*, t2.name FROM table1 as T1
            LEFT JOIN table1 as T2 ON T2.id = T1.refer
            //JOIN => default INNER JOIN
    * How to delete duplicate inters using self join
        * USING SELF JOIN
            * DELETE T1 from Table1
                JOIN Table1 as T2 WHERE T1.id < T2.id AND T1.phone_no = T2.phone_no
    * Sub Queries
        * the iterator need only one output on one step 
        * SELECT * , (SELECT name FROM table2 WHERE id = 1) as name
        FROM table1
         * 
        * IN
            * SELECT 
        * ANY / SOME 
        * EXISTS / NOT EXISTS
        * ALL
        * FROM
            * SELECT name FROM (SELECT * FROM university WHERE country = 'USA');
        * CORRELATED SUB_QUERY
            * Correlated subqueries are subquesries which refer to main, outer query and can not be run as independent queries without the main query
            * SELECT name FROM city as big_city
                Where population > (
                    SELECT AVG(population)
                        FROM city 
                        WHERE big_city.country_id = city.country_id
                )
            * with EXISTS
                * SELECT name FROM supplier
                    WHERE EXIST (
                        SELECT * FROM products
                        WHERE category = "food"
                            AND supplier_id = supplier.id
                    )
                * SELECT name FROM supplier
                    WHERE NOT EXISTS (
                        SELECT * FROM products
                            WHERE price > 1.0 AND 
                                supplier_id = supplier.id
                    )
            * with SELECT 
                * it must return only one row with exactly one column.
                * SELECT name, (SELECT AVG(price) FROM products WHERE supplier_id = supplier.id)
                    FROM supplier;

                * SELECT 
                    name, 
                    (SELECT COUNT(id) FROM products WHERE supplier_id = supplier.id) AS count_all,
                    (SELECT COUNT(id) FROM products WHERE supplier_id = supplier.id AND category = 'food) AS count_food
                    FROM supplier;

    * REPLACE AND Substring 
        * Substring work as split function
            * SELECT SUBSTRING_INDEX(fieldName(email), "condition(@)" , 1/-1) from table1
        * Replace
            * SELECT REPLACE(fieldName(email), "@" ,"#") from table1
    * IFNULL() and CAST()
        * IFNULL is if condition on NULL
            * SELECT IFNULL(FieldName, "NA") FROM 'Table1"
        * CAST() is used to view a field into maintain data type 
            * SELECT CAST(field_name(fees) AS DATA_TYPE(UNSIGNED)) FROM table1
    * JSON FUNCTION
        * if you have json data in a field
            * SELECT fieldName->"$.name" from tableName
            * SELECT JSON_EXTRACT(fieldName, '$[0]') from tableName

            * SELECT JSON_UNQUOTE(JSON_EXTRACT(fieldName, '$[0].name')) from table1 // for remove ""

            * SELECT JSON_SEARCH(fieldName, "all", "vishnu") form Table1 // output => "$[1].name"
            * JSON_MERGE
            * JSON_OBJECT
            * JSON_SET
            * JSON_INSERT
            * JSON_REPLACE
            * JSON_REMOVE
    * Stored Procedure
        * it is used to make utilities queries with params values
        * Defination
            * CREATE PROCEDURE procedure_name
                AS
                sql_statement
                GO;
        * CAll
            * EXEC procedure_name;
    * comments
        * -- for single line comment

    * COMMAND LINE
        * mysql -u root -p
            password: 
        * to Fetch a all user
            select user from mysql.user
        * to show all databases
            * show databases
        * to enter into a database
            * use databseName
            * show tables
        * To make users
            * select user from mysql.user
            * to create user
                * CREATE USER 'username'@'localhost' IDENTIFIED BY 'password'
                // still not has permission to view database
            * to delete user
                * DROP USER 'username'@'localhost'
            * to give permission
                * to view permission for user
                    * show grants for 'username'@'localhost'
                * to give permission
                    * GRANT ALL PRIVILEGES ON * . (for all database) * to 'username'@'localhost'
                    * GRANT ALL PRIVILEGES ON * `databaseName`.* to 'username'@'localhost'
                    
                * to take permission
                    * REVOKE ALL PRIVILEGES ON * . (for all database) * to 'username'@'localhost'  
            * Reset or Change the password
                * set password FOR username'@'localhost = password('NewPassword')
            * import table export table
                * IMPORT 
                    * mysql -u root -p databaseName < newTable.sql
                * EXPORT 
                    * mysqldump -u -p databaseName table1 table2 > newFileName.sql
            * create , delete and show database
                * create databse databaseName
                * drop database databaseName
                * use databaseName
                    * show tables
                    * select * from table1
                    * all sql queries can run there
            * Import table/database from local to serve
                * scp fileName.sql remote@121.11.11.22:/tmp/ 
                * cd tmp
                * mysql -u root -p database < fileName.sql
                * rm -rf fileName.sql
            * 


        
             




// for mode error      
* SET GLOBAL sql_mode = ""

* TIPS
    * Highest / Ordering / Nth USE AGGREGATE FUNCTION
    * Highest -> it is also solve my sub query
    * Condition on SQL in done by CASE THEN ELSE
    * condition count is writer in
        SUM(CASE salary > 100000 THEN 1 ELSE 0)
        * it return the count of employ who salary is greater then 100000


                
        



    
    
        
