# DB-Address-Book-System
## UC1- Creating a database address_book_service
`create database address_book_service;`
### Use the database
`use address_book_service;`

## UC2- Creating a table Address Book in database
```
create table address_book
    -> (
    -> FirstName varchar(90) NOT NULL,
    -> LastName varchar(90) NOT NULL,
    -> Address varchar(250) NOT NULL,
    -> City varchar(90) NOT NULL,
    -> State varchar(90) NOT NULL,
    -> ZIP int(5) NOT NULL,
    -> Phone_Number int(14) NOT NULL,
    -> Email varchar(150) NOT NULL,
    -> PRIMARY KEY (FirstName)
    -> );
```
