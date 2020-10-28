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

## UC7- Understand the size of address book (count) by City or State
### Count of contacts from a particular City
`SELECT City, COUNT(City) FROM address_book GROUP BY City;`
### Count of contacts from a particular State
`SELECT State, COUNT(State) FROM address_book GROUP BY State;`

## UC8- Retrieve alphabetically sorted entries by name for a particular city
`SELECT * FROM address_book WHERE city='Thane' ORDER BY FirstName;`

## UC9- Identify each address book with name and type
### Adding more contacts
```
INSERT INTO address_book(FirstName, LastName, Address, City, State, ZIP, Phone_Number, Email) VALUES
    -> ('Devesh', 'Srivastav', 'Lucknow', 'Lucknow', 'Uttar Pradesh', 400614, 7045279235, 'devesh@gmail.com'),
    -> ('Saurav', 'Sinha', 'Patna', 'Patna', 'Bihar', 400620, 7045279236, 'saurav@gmail.com');
```
### Altering table to add columns Type and Book_Name
```
alter table address_book add Book_Name varchar(100) after email;
alter table address_book add Type varchar(100) after email;
```
### Setting Type
```
update address_book set Type = 'Family' where FirstName = 'Jayesh' or FirstName = 'Ajeesh';
update address_book set Type = 'Friends' where FirstName = 'Devesh';
update address_book set Type = 'Profession' where FirstName = 'Saurav';
```
### Setting Book_Name
```
update address_book set Book_Name = 'Personal' where Type = 'Family' or Type = 'Friends';
update address_book set Book_Name = 'Work' where Type = 'Profession';
```

## UC10- Get number of contacts of type
`select Type, count(Type) from address_book group by Type;`

## UC11- Add contacts to friends and family
```
INSERT INTO address_book(FirstName, LastName, Address, City, State, ZIP, Phone_Number, Email, Type, Book_Name) VALUES
    -> ('Ajay', 'Yadav', 'Nagpur', 'Nagpur', 'Maharashtra', 400624, 7045279237, 'ajay@gmail.com', 'Friends', 'Personal'),
    -> ('Aditya', 'Raj', 'Jaipur', 'Jaipur', 'Rajasthan', 400630, 7045279238, 'aditya@gmail.com', 'Family', 'Personal');
```

## UC13- Ensure all retrieve querries are working properly with new structure
### Creating table book
```
create table book
    -> (
    -> name VARCHAR(150) NOT NULL PRIMARY KEY,
    -> type VARCHAR(150) NOT NULL
    -> );
```

### Creating table contact
```
create table contact
    -> (
    -> id INT unsigned NOT NULL AUTO_INCREMENT PRIMARY KEY,
    -> book_name VARCHAR(150) NOT NULL,
    -> FirstName VARCHAR(100) NOT NULL,
    -> LastName VARCHAR(100) NOT NULL,
    -> Phone_Number VARCHAR(15) NOT NULL,
    -> Email VARCHAR(150) NOT NULL,
    -> FOREIGN KEY (book_name) REFERENCES book (name)
    -> );
```

### Creating table address
```
create table address
    -> (
    -> id INT unsigned NOT NULL,
    -> address VARCHAR(250) NOT NULL,
    -> city VARCHAR(100) NOT NULL,
    -> state VARCHAR(100) NOT NULL,
    -> ZIP mediumint NOT NULL,
    -> FOREIGN KEY (id) REFERENCES contact (id)
    -> );
```

### Inserting values into book
```
INSERT INTO book VALUES
    -> ('Personal','Family'),
    -> ('Work', 'Profession'),
    -> ('Associates', 'Friends');
```

### Inserting values into contact
```
INSERT INTO contact (book_name, FirstName, LastName, Phone_Number, Email) VALUES
    -> ('Personal', 'Jayesh', 'Chaudhari', '7045279233', 'jayesh@gmail.com'),
    -> ('Associates', 'Ajeesh', 'Ajayan', '7045279234', 'ajeesh@gmail.com'),
    -> ('Work', 'Devesh', 'Srivastav', '7045279235', 'devesh@gmail.com'),
    -> ('Associates', 'Saurav', 'Sinha', '7045279236', 'saurav@gmail.com');
```
### Inserting values into address
```
INSERT INTO address VALUES
    -> (1,'CSMT', 'Mumbai', 'Maharashtra', 400600),
    -> (2,'Dadar', 'Mumbai', 'Maharashtra', 400601),
    -> (3,'Chowk', 'Lucknow', 'Uttar Pradesh', 400602),
    -> (4,'Janpath', 'Patna', 'Bihar', 400603),
    -> (3,'Museum', 'Agra', 'Uttar Pradesh', 400605),
    -> (2,'Zoo', 'Kochi', 'Kerala', 400606);
```

### Retrieve contacts belonging to a city or state
```
select FirstName, City from address a, contact c where a.id = c.id and a.city = 'Mumbai';
select FirstName, State from address a, contact c where a.id = c.id and a.state = 'Maharashtra';
```
### Understand the size of address book of a city or state
```
select a.city, count(c.id) from address a, contact c where a.id = c.id and city = 'Mumbai';
select a.state, count(c.id) from address a, contact c where a.id = c.id and state = 'Maharashtra';
```
### Retrieve alphabetically sorted entries by name for a particular city
`select c.FirstName, c.LastName, a.city from address a, contact c where a.id = c.id and city = 'Mumbai' ORDER BY c.FirstName;`
### Get number of contacts of type
`select b.type, count(c.id) from book b, contact c where b.name = c.book_name group by b.type;`
