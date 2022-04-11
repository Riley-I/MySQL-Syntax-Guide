    
# MySQL Cheatsheet
    

    
   ## How to login into mysql from terminal:

       >  sudo mysql -u root -p

            

    ## How to SHOW USERS:

        >   SELECT User, Host FROM mysql.user;



    ## How to CREATE USERS:

        >   CREATE USER 'newuser'@'localhost' IDENTIFIED BY 'password';



    ## How to GRANT PRIVILEGES, Show granted privileges and remove:

        >   GRANT ALL PRIVILEGES ON * . * TO 'newuser'@'localhost';
                    or
        >   GRANT type_of_permission ON database_name.table_name TO 'username'@'localhost';
        >   FLUSH PRIVILEGES;

        >   SHOW GRANTS FOR 'username'@'localhost';

        >   REVOKE type_of_permission ON database_name.table_name FROM 'username'@'localhost';

        >   DROP USER 'username'@'localhost';



    ## How to SHOW, DELETE & CREATE DATABASES & SELECT DATABASES:

        >   SHOW DATABASES;

        >   DROP DATABASE database_name;

        >   CREATE DATABASE database_name;

        >   USE database_name;



    ## How to CREATE a TABLE with Columns and their data types:

        >   CREATE TABLE Inventory (
                Inventory_ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
                Item_Name VARCHAR(25), 
                Item_Category VARCHAR(25),
                Initial_Cost INT,
                Aquired_Date DATE,
                Number_Total INT,
                Item_Weight VARCHAR(25)
            );


    ## How to SHOW, DELETE & DROP Tables:

        >   SELECT * FROM Inventory;

        >   DROP TABLE Inventory;


    ## How to Insert ROWS & RECORDS (single and multiple):

        >   INSERT INTO Inventory (Item_Category)
            VALUES ('skis');

        >   INSERT INTO Inventory (
                Item_Name, 
                Item_Category, 
                Initial_Cost,
                Aquired_Date,
                Number_Total,
                Item_Weight
                ) 
                VALUES
                    (
                    'Burton Jacket', 
                    'Winter Apparel', 
                     500,
                    '2020-12-03',
                     3,
                    '500 grams'
                    );



    ## How to SELECT with the WHERE Clause

        >   SELECT * FROM Inventory
            WHERE Item_Name = 'Burton Jacket';


    ## How to SELECT with the WHERE Clause using a range

        >   SELECT * FROM Inventory
            WHERE Aquired_Date BETWEEN '2020-12-01' AND '2020-12-08';



    ## How to DELETE an individual ROW

        >   DELETE FROM Inventory
            WHERE Inventory_ID = 1;


    ## How to UPDATE a ROW

        >   UPDATE Inventory
            SET Item_Weight = '500 grams'
            WHERE Inventory_ID = 2;


    ## How to add a new column and modify it:

        >   ALTER TABLE Inventory
            ADD COLUMN Item_Colour VARCHAR(15) AFTER Item_Weight; 


    ## How to Order by and use Distinct:

        >   SELECT * FROM Inventory
            ORDER BY Item_Weight DESC;

        >   SELECT DISTINCT Item_Name FROM Inventory;


    ## How to Concatenate Columns:

        >   SELECT CONCAT(Item_Name, " ", Item_Colour) AS Item_Description
            FROM Inventory; 


    ## How to Select Distinct Rows:

        >   SELECT DISTINCT Item_Name FROM Inventory;


    ## How to use LIKE to Search:

        >   SELECT * FROM Inventory
            WHERE Item_Name LIKE 'a%'; 


    ## How Select using IN:

        >   SELECT * FROM Customers
            WHERE Customer_ID IN (10, 16);


    ## How to Create & Remove Index:

        >   CREATE INDEX Customer_Id 
            ON Customers;

        >   DROP INDEX Customer_Id 
            ON Customers;

        >   DROP INDEX `PRIMARY` 
            ON Customers;

        >   ALTER TABLE Customers 
            DROP INDEX Customer_Id;

        >   ALTER TABLE Customers 
            DROP PRIMARY KEY;



    ## Create Two Tables demonstrating a one to many relationship that shows a PK & FK:

        >   CREATE TABLE Movies (
                MovieID int NOT NULL,
                MovieName varchar(255) NOT NULL,
                Director varchar(255),
                Length int,

                PRIMARY KEY (MovieID)
            );


            CREATE TABLE Tickets (
                TicketID int NOT NULL,
                TicketNumber int NOT NULL,
                date datetime,

                PRIMARY KEY (TicketID),
                FOREIGN KEY (MovieID) REFERENCES Movies(TicketID)
            );


    ## How to use Inner Join

            >>  SELECT table1.col, table2.col
                FROM table1
                JOIN table2 ON table1.primarykey = table2.foreignkey

            >   SELECT Tickets.TicketID, Tickets.MovieID, Customer.FirstName
                FROM Tickets
                INNER JOIN Customer
                ON Customer.PersonID = Tickets.PersonID
                INNER JOIN Movies ON Movies.MovieID = Tickets.TicketID;


    ## How to JOIN Multiple Tables

            -   All the 3 tables should be in a relationship with a foreign key.
            -   Each table must have a common column (that contains matching values)
            -   a common column of the first tables must have a primary key and another common column of the second tables must have a foreign key

            >   SELECT table1.column1_name, table1.column2_name,..., 
                table2.column1_name, table2.column2_name,..., 
                table3.column1_name, table3.column2_name,..., 
                FROM table1
                INNER JOIN table2 ON table1.table1_id = table2.table1_id 
                INNER JOIN table3 ON table2.table2_id  = table3.table2_id;


       ### EXAMPLE
    
            -   3 tables = Tickets, Customers, Contacts
            -   Customers table joined to Tickets tables with common column Customer_Id
            -   Contacts table joined to Customers table with common column Person_Id


            >   SELECT Customers.full_name, Contacts.mobile_number, Contacts.email_address, Tickets.date, Tickets.description 
                FROM Tickets
                INNER JOIN Customers ON Tickets.Customer_Id = Customers.Customer_Id
                INNER JOIN Contacts ON Customers.Person_Id = Contacts.Person_Id;

            


