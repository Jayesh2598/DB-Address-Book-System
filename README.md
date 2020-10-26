# DB-Address-Book-System
## UC1- Creating a database address_book_service
`create database address_book_service;`
### Use the database
`use address_book_service;`

## UC2- Creating a table Address Book in database
```
create table address_book
    -> (
    -> FirstName varchar(100) NOT NULL,
    -> LastName varchar(100) NOT NULL,
    -> Address varchar(250) NOT NULL,
    -> City varchar(100) NOT NULL,
    -> State varchar(100) NOT NULL,
    -> ZIP mediumint(6) NOT NULL,
    -> Phone_Number varchar(15) NOT NULL,
    -> Email varchar(150) NOT NULL,
    -> PRIMARY KEY (FirstName)
    -> );
```

## UC3- Inserting contacts into address_book table
```
INSERT INTO address_book(FirstName, LastName, Address, City, State, ZIP, Phone_Number, Email) VALUES
    -> ('Jayesh', 'Chaudhari', 'Thane', 'Thane', 'Maharashtra', 400604, 7045279233, 'jayesh2598@gmail.com'),
    -> ('Ajeesh', 'Ajayan', 'Mumbai', 'Mumbai', 'Maharashtra', 400610, 7045279234, 'ajeesh@gmail.com'),
    -> ('Devesh', 'Srivastav', 'Lucknow', 'Lucknow', 'Uttar Pradesh', 400614, 7045279235, 'devesh@gmail.com');
```

## UC4- Edit existing contact using name
`UPDATE address_book SET Address = 'Kalyan' WHERE FirstName = 'Ajeesh';`

## UC5- Delete existing contact using name
`DELETE FROM address_book WHERE FirstName = 'Devesh';`

## UC6- Retrieve contacts belonging to a city or state
### Contacts from a particular city
`SELECT * FROM address_book WHERE City = 'Thane';`
### Contacts from a particular state
`SELECT * FROM address_book WHERE State = 'Maharashtra';`
