
## Mysql Commands

### To create a database 
These sql commands are case insensative so we can write in uppercase or lowercase 

    create database [db_name];

### To delete a database

    drop database [db_name];

### To use a created database

    use [db_name];

### To alter a database 
This ALTER command sets the database "my_db" to read-only mode, meaning it can be viewed but not modified or updated or deleted.Inorder to disable to read_only mode set the read_only=0;

    alter database [db_name] read_only=1; 

### To create a table in mysql database
In this case we are creating a table named employee with employee id , first_name, last_name, hire_date,and hourly_pay

    CREATE TABLE emploee(
        employee_id INT,
        first_name VARCHAR(50),
        last_name VARCHAR(50),
        hourly_pay DECIMAL(5,2),
        hire_date DATE
    );

### To select the data of employee table now 
This selects all the data from the employee table 

    SELECT * FROM employee;

### To rename the employee table 
This renames the employee table into workers

    RENAME TABLE employee TO workers;

### To delete the table 
This delete the workers table 

    DROP TABLE workers;

### To add new field in the existing database 
In this case we are adding the additional phone_number field in the employee table 

    ALTER TABLE employee ADD phone_number Varchar(15);

### To Rename Table Column 
THis renames the employee table phone_number column into ph_no

    ALTER TABLE employee RENAME COLUMN phone_number TO ph_no;

### To change the datatype 
This changes the email columns datatype into varcar with
maximum characters of 50 and the after keyword helps to place the email column right after the last_name column 


    ALTER TABLE employee MODIFY email VARCHAR(50) AFTER last_name;

### To add the column at first
Instead of writing the AFTER [table_column] just write FIRST; This will keep your coulmn at the first 


### To delete the column of a table 
This helps to drops the hire_date column of the employee table 

    ALTER TABLE employee DROP COLUMN hire_date;


### To insert single data in mysql database 
This helps to insert the dat into the employee table relative to the emploee table column

    Note: My table employee has the column in this format 
    1-employee_id (INT)
    2-first_name (VARCHAR)
    3-last_name (VARCHAR)
    4-email (VARCHAR)
    5-ph_no (VARCHAR)


    INSERT INTO employee 
    VALUE (
    1,"Ayush","Tmg","ayush@gmail.com","98784904"
    );

### To insert multiple data in mysql database 
This helps to insert multiple data in the employee database 
The data's are seperated by parenthesis and a commad this way -->(),

    INSERT INTO employee 
    VALUE 
    (1,"Ayush","Tmg","ayush@gmail.com","98784904"),
    (2,"Adarsh","Tmg","adarsh@gmail.com","9878373"),
    (3,"Sunita","Tmg","sunita@gmail.com","987337839");


### To insert with some data missing 
This insert the data without the ph_no column and it works

    INSERT INTO employee 
    (employee_id,first_name,last_name,email)
    VALUE (4,"Dummy","Tmg","sunita@gmail.com");

### To select specific column of a table 
This helps to select the first_name and the last_name column only of all the emploee in the database. You can order column as you like you can use last_name in first and the first_name later too 

    SELECT first_name,last_name FROM employee;

### To filter a user using where 
This helps to show all the column of employee with the id =1 

    SELECT * FROM employee WHERE employee_id=1;

We can also assgin it like this which select all the users with the employee_id equal to or greater than 1

    SELECT * FROM employee WHERE employee_id=1;

We can also assgin it like this which select all the employee table data except the employee with id=1

    SELECT * FROM employee WHERE employee_id!=1;

This selects all the employee whose ph_no column is NUll we can also use is not NUll

    SELECT * FROM employee WHERE ph_no IS NULL;

### To update databse column 
This update the ph_no of employee with id =1 in employee table we can also update multiple values by seperating SET x=x,y=y etc 
Note: If you want to update in all the column just exclude the WHERE clause 

    UPDATE employee SET ph_no="94876893" WHERE employee_id=1;

### To delete all the row in the table 
This deletes all the row in the employee table 

    DELETE FROM employee;

### To delete a specific row 
This delete the row where the employee id is equals to 1 

    DELETE FROM employee WHERE employee_id=1;

### To create a safepoint using auto commit 
By default the AUTOCOMMIT is on and when we make changes it directy saves those changes but with the AUTOCOMMIT off we need to use COMMIT; after we make some change to the database 

    SET AUTOCOMMIT = OFF;

Suppose you have set AUTOCOMMIT to OFF and you mistakly deleted the emploee table all rows 

    DELETE FROM employee;

To get your changes back use this commad you get your mistakly deleted data back 

    ROLLBACK;

And If you are sure about deleting the data instead of getting it back use this 

    COMMIT;

### To add current date,time and datetime
This helps to  add the current date ,current time , and current datetime in to test table 

    INSERT INTO test VALUE(CURRENT_DATE(),CURRENT_TIME(),NOW());


### To add a unique constraint in MySQL 
we can see there a unique constraint in the id of the product table  


    CREATE TABLE products
    (
    id INT UNIQUE,
    title VARCHAR,
    price DECIMAL(4,2),
    );

### To add unique constraint after the table is defined 
If you forger to include the unique constraint in table at the time of creating it you can modify it later this way. In here we have added a unique constraint after the product table is created 

    ALTER TABLE product ADD CONSTRAINT UNIQUE(id);


### To create table column that cant be left empty 
This NOT NULL is used to specify that the column has be left NULL 

    CREATE TABLE product (
    id INT NOT NULL,
    title VARCHAR(50) NOT NULL
    );

### To add not null on existing table 
This makes the price column on the existing table products not nullable 

    ALTER TABLE products MODIFY price DECIMAL(4,2) NOT NULL;

### To add check constraint
This helps to check if the price is greater to or equals to 10 while creating a product table 
Note: In this case the check will forbid any insertion of price smaller than 10.

    create table product(
    id int not null unique,
    title varchar not null,
    price decimal(4,2) not null,
    constraint price_check check (price>=10)
    );

### To add the check constraint on existing table 
This helps to modify the table and add the check constraint named price_check in the product table 

    ALTER TABLE product ADD CONSTRAINT  price_check CHECK(price>=10); 

### To delete a check 
This helps to delete the check named price_check from the product table 

    ALTER TABLE product DROP CHECK price_check;

### To add the default constraint 
This helps to add the default value 0 in the price while creating it 

    create table test(
    id int not null unique,
    price decimal(4,2) not null default 0
    );

### To add the default constraint on existing table
This helps to add the default constraint for the existing table  

    ALTER TABLE product ALTER price SET DEFAULT 0;

### To Use Group Clause 
This helps of get list of common category in the sales table and sum of those category price 

    SELECT category, SUM(price) AS total_price FROM sales GROUP BY category;


### To Add Foregin Key In Table 
In this query we have created a table Orders which has foreign key as user_id which references the user_id column for the Users Table 

    CREATE TABLE Orders (
        order_id INT PRIMARY KEY,
        user_id INT,  -- Foreign Key referring to Users table
        order_date DATE,
        total_amount DECIMAL(10,2),
        FOREIGN KEY (user_id) REFERENCES Users(user_id)  -- FK Constraint
    );

### Store Procedure in SQL 
A Stored Procedure is a set of SQL statements that are saved in the database and can be executed whenever needed. its like a function in programming

The DELIMITER in MySQL is used to change the default ; (semicolon) delimiter so that MySQL doesn't stop execution too early when defining procedures, triggers, or functions.

    ## In this case we have change the delimiter to // for creating 
    procedure and againg changing it back to the semicolon

    DELIMITER //

    CREATE PROCEDURE GetStudentsByAge(IN student_age INT)
    BEGIN
        SELECT * FROM students WHERE age = student_age;
    END //

    DELIMITER ;

    ## We can call the procedure this way next time to execute this query 

    CALL GetStudentsByAge(22);

This is the example of a dynamic procedure which takes the student age to 
query we can even create procedure with takes no parameters 

###  To Drop Procedure

    Drop Procedure [procedure_name];

### Triggers In SQL 

A trigger is a special SQL code that runs before or after INSERT, UPDATE, or DELETE operations on a table.

    # this triggers insert the new record in the audit log table 
    # about before updation of user table 
      
    CREATE TRIGGER before_user_update
    BEFORE UPDATE ON users
    FOR EACH ROW
    INSERT INTO audit_log (user_id, action, changed_at)
    VALUES (OLD.id, 'User updated', NOW());

Another Example of trigger 

    # This triggers updates the total price column with 
    new updated quantity and unit_price before update on table orders 

    CREATE TRIGGER before_order_insert
    BEFORE UPDATE ON orders
    FOR EACH ROW
    SET NEW.total_price = (NEW.quantity * NEW.unit_price);

### To see all the triggers in the database 

    show triggers; 


### On Delete Clause In SQL 

The ON DELETE clause in SQL is used to define what happens when a referenced row in a parent table is deleted. It is mostly used in foreign key constraints to maintain referential integrity.

### Types of ON DELETE Actions
- ON DELETE CASCADE → Deletes related rows in the child table when the parent row is deleted.
- ON DELETE SET NULL → Sets the foreign key column to NULL instead of deleting the row.
- ON DELETE RESTRICT → Prevents deletion if there are related records in the - child table.
- ON DELETE NO ACTION → Similar to RESTRICT, but follows SQL standards.

        # Creation of table with the foreign key to customer table 
        customer id and when the foreign key is deleted its related
        orders are also deleted in this case because of Cascase on 
        delete clause 

        CREATE TABLE orders (
            id INT PRIMARY KEY,
            customer_id INT,
            order_details VARCHAR(255),
            FOREIGN KEY (customer_id) REFERENCES customers(id) ON DELETE CASCADE
        );

### Joins In SQL 

Suppose We have two tables:

employees – Stores employee details has foreign key with departments table column department_id.
departments – Stores department details.

### Best Way to Think About Join
INNER JOIN → Intersection (Only matching data from both tables)
LEFT JOIN → All from the Left + Matching from Right
RIGHT JOIN → All from the Right + Matching from Left


Inner Join 
Suppose we want to find the employees with the departments 

    SELECT employees.id, employees.name, departments.department_name 
    FROM employees 
    INNER JOIN departments ON employees.department_id = departments.id;

Left Join  
Suppose we want to show the employees with the departments plus all the employes with out the departments from the employee table too 

    SELECT employees.id, employees.name, departments.department_name 
    FROM employees 
    LEFT JOIN departments ON employees.department_id = departments.id;


Right Join  
Suppose we want to show the employees with the departments plus all the department in the departments table too 

    SELECT employees.id, employees.name, departments.department_name 
    FROM employees 
    LEFT JOIN departments ON employees.department_id = departments.id;

### Indexing In MYSQL 

Indexing is used to search using a tables column more efficiently and fast 

    # To create a index 
    Create Index [index_name]
    On [table_name( [it's column_name]) ];

    # To view indexes from a specific table 
    Show indexes from [table_name]'

### To Limit Data IN SQL 
    #This is used for pagination for loading useful while working 
    with a lot of data
    #In this case it only shows 3 data from the customer table because of
    limit clause to 3 
    
    Select * from customer limit 3;
