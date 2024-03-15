# MySQL-Commands


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

