
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

