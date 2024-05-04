# Library Database

### Project Overview

This Library database project aims to efficiently manage book inventory, member data, and borrowing activities with this comprehensive database system tailored for libraries,utilizing relational database principles and SQL queries for seamless operations and insightful analytics.


##   Documentation

### Entity Relationship Diagram
![Entity Relationship Diagram](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/113e98e3-b20a-42ce-8d90-67b5aead4c75)

### Database Legend 
<img width="403" alt="Lengend for genre and author tables" src="https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/1d6630b1-e837-4e84-986b-14bb61423bde">



### Key Highlights  

- **Comprehensive Structure**: Meticulously crafted tables for books, authors, genres, members, and borrowings, reflecting a deep understanding of relational database principles.
  
- **Data Integrity**: Implemented with precision, ensuring each column has appropriate data types and constraints for reliable data management and accuracy.
  
- **Automation with Triggers**: Utilized triggers to automate crucial processes, such as updating book availability status, enhancing efficiency and maintaining database integrity.
  
- **Realistic Sample Data**: Includes realistic sample data for thorough testing and demonstration, providing recruiters with a tangible understanding of my SQL skills.

### Preperation 

I created the entity relationship diagram (ERD) for my library database using the website https://www.quickdatabasediagrams.com/. This tool made it easy to design and visualise how the different parts of my database connect. I started by defining tables like books, authors, genres, members, and borrowings, and then I showed how they relate to each other. It was straightforward to drag and drop to make connections and set up the structure of the database.


### SQL script used to create database/tables

```sql

CREATE DATABASE library;

USE library;

-- Table for storing data about books in the library

CREATE TABLE books 
(
    book_id INT  NOT NULL AUTO_INCREMENT ,
    title varchar(50) NOT NULL ,
    author_id INT NOT NULL ,
    genre_id INT NOT NULL ,
    publish_year INT NOT NULL ,
    available_to_rent ENUM('Y','N') DEFAULT 'Y' ,
    PRIMARY KEY (book_id)
);

-- Table for storing data regarding book authors.

CREATE TABLE authors 
(
    author_id INT  NOT NULL AUTO_INCREMENT,
    author_name VARCHAR(50)  NOT NULL ,
    nationality VARCHAR(50)  NOT NULL ,
    birth_year VARCHAR(20)  NOT NULL ,
    PRIMARY KEY (author_id)
);

-- Table for storing data about the genere of books.

CREATE TABLE genres
 (
    genre_id INT  NOT NULL AUTO_INCREMENT,
    genre_name VARCHAR(50)  NOT NULL ,
    PRIMARY KEY (genre_id)
);

-- Table for storing data about the library members.

CREATE TABLE members
 (
    member_id INT  NOT NULL AUTO_INCREMENT,
    first_name varchar(50)  NOT NULL ,
    last_name varchar(50)  NOT NULL ,
    gender ENUM('M','F')  NOT NULL ,
    email_address varchar(200)  NOT NULL ,
    membership_status ENUM('Active','Inactive','Expired')  DEFAULT 'Active',
    PRIMARY KEY (member_id), UNIQUE KEY (email_address)
);

-- Table for storing data about book borrowings.

CREATE TABLE borrowings
 (
    borrowing_id INT  NOT NULL AUTO_INCREMENT ,
    member_id INT  NOT NULL ,
    book_id INT  NOT NULL ,
    borrowing_date DATE  NOT NULL ,
    return_date DATE  NOT NULL ,
    PRIMARY KEY (borrowing_id)
);
```
### SQL script used to add foreign key constraints to tables

```sql

/* Add foreign key constraint to link author_id column in books table
   to the author_id column in the Authors table. */

ALTER TABLE books 
ADD FOREIGN KEY(author_id)
REFERENCES Authors (author_id) ON DELETE CASCADE;

/* Add foreign key constraint to link genre_id column in Books table
   to genre_id in Genres table. */

ALTER TABLE books 
ADD FOREIGN KEY(genre_id)
REFERENCES Genres (genre_id)ON DELETE CASCADE;

/* Add foreign key constraint to link member_id column in Borrowings table
   to members_id column in Members table */

ALTER TABLE borrowings 
ADD FOREIGN KEY(member_id)
REFERENCES Members (member_id)ON DELETE CASCADE;

/* Add foreign key constraint to link book_id column in Borrowings table 
   to book_id column in Books table */

ALTER TABLE borrowings 
ADD FOREIGN KEY(book_id)
REFERENCES Books (book_id)ON DELETE CASCADE;

```
### SQL script used for populating tables

```sql

-- I have chosen to make the starting value for the author_id 1000 -- 

ALTER TABLE authors 
AUTO_INCREMENT = 1000;

INSERT INTO authors (author_name, nationality, birth_year)
VALUES
('Roald Dahl','British','1916-09-13'),
('J.K. Rowling','British','1965-07-31'),
('Jill Murphy','British','1949-07-05'),
('Nick Butterworth','British','1946-05-24'),
('Julia Donaldson','British','1948-09-16'),
('David McKee','British','1935-01-02'),
('George Orwell','British','1903-06-25'),
('Malorie Blackman','British','1962-02-08'),
('Agatha Christie','British','1890-09-15'),
('Charles Dickens','British','1812-02-07'),
('Alice Walker','American','1944-02-09'),
('Stan Lee','American','1922-12-28'),
('F.Scott Fitzgerald','American','1896-09-24'),
('John Steinbeck','American','1902-02-27'),
('Mark Twain','American','1835-11-30'),
('Harper Lee','American','1926-04-28'),
('Stephen King','American','1947-09-21'),
('Eric Carle','American','1929-06-25'),
('James Patterson','American','1947-03-22'),
('Victor Hugo','French', '1885-05-22'),
('Alexandre Dumas','French','1870-12-05'),
('Albert Camus','French','1913-11-07');

-- I have chosen to make the starting value for the member_id 2000 -- 

ALTER TABLE members
AUTO_INCREMENT = 2000;

/* emails have been manually randomised for authenticity and realism 
   based off the kinds of emails that I have seen customers have at my current job role */

INSERT INTO members (first_name, last_name, gender, email_address)
VALUES
('Joshua','Asante','M','joshua_asante123@hotmail.com'),
('George','Martin','M','martinman765@gmail.com'),
('Kelly','Rowland','F','rowland_kelly@yahoo.co.uk'),
('Romeo','Smith','M','romeosmith_98@btinternet.com'),
('Emily','Johnson','F','emily.johnson@aol.com'),
('Michael','Smith','M','smith4life@hotmail.com'),
('Sophia','Williams','F','sophia29@hotmail.co.uk'),
('Jacob','Brown','M','rocketmann_jacob@yahoo.co.uk'),
('Olivia','Davis','F','olivia_davis@gmail.com'),
('Ethan','Martinez','M','hewhoseesall127@sky.com'),
('Harry','Potter','M','harry.potter@outlook.com'),
('Isabella','Taylor','F','taylor23852000@hotmail.co.uk'),
('Daniel','Anderson','M','anderson_1986@sky.com'),
('Ava','Wilson','F','ava_wilson@aol.com'),
('Alexander','Thomas','M','thomas.alexander@icloud.com'),
('Mia','Garcia','F','miagarcia1@gmail.com'),
('William','Jones','M','jones1287@sky.com'),
('Harper','Rodriguez','F','tocoolforschool@btinternet.com'),
('James','Miller','M','james1miller@hotmail.co.uk'),
('Charlotte','Martinez','F','charlotte_martinez@sky.com'),
('Benjamin','Harris','M','bennyboy23@blueyonder.com'),
('Amelia','Robinson','F','a.robinson@hotmail.com'),
('Samuel','Lee','M','lee_familyman@hotmail.com'),
('Ella','Clark','F','ellaclark1964@sky.com'),
('Lucas','Thompson','M','thompson29@outlook.com');

-- I have chosen to make the starting value for the book_id 3000 -- 

ALTER TABLE books
AUTO_INCREMENT = 3000;

-- I have chosen to make the starting value for the genre_id 4000 -- 

ALTER TABLE genres
AUTO_INCREMENT = 4000;

-- inserting values into the genres table --

INSERT INTO genres(genre_name)
VALUES
('Fantasy'),
('Childrens Humour'),
('Autobiography'),
('Adventure'),
('Childrens Fiction'),
('Political Satire'),
('Biography'),
('Speculative Fiction'),
('Young Adult Fiction'),
('Mystery'),
('Bildungsroman'),
('Coming of Age'),
('Art/Instructional'),
('Romance'),
('Tragedy'),
('Horror');

-- Inserting values into the books table --

INSERT INTO books (title, author_id, genre_id, publish_year, available_to_rent)
VALUES
('Charlie and the Chocolate Factory',1000,4000,1964,'Y'),
('The Witches',1000,4000,1983,'Y'),
('Matilda',1000,4000,1988,'Y'),
('The BFG',1000,4000,1982,'Y'),
('James and the Giant Peach',1000,4000,1961,'Y'),
('Fantastic Mr Fox',1000,4000,1970,'Y'),
('The Twits',1000,4001,1980,'Y'),
('Charlie and the Great Glass Elevator',1000,4000,1972,'Y'),
('Boy: Tales of Childhood',1000,4002,1984,'Y'),
('The Wonderful Story of Henry Sugar and Six More',1000,4003,1977,'Y'),
('Danny,the Champion of the World',1000,4004,1975,'Y'),
("George's Marvellous Medicine",1000,4000,1981,'Y'),
("Harry Potter and the philosopher's Stone",1001,4000,1997,'Y'),
('Harry Potter and the Deathly Hallows',1001,4000,2007,'Y'),
('Fantastic Beasts and Where to Find Them',1001,4000,2001,'Y'),
('Harry Potter and the Chamber of Secrets',1001,4000,1998,'Y'),
('Harry Potter and the Prisoner of Azkaban',1001,4000,1999,'Y'),
('Harry Potter and the Goblet of Fire',1001,4000,2000,'Y'),
('Harry Potter and the Order of the Pheonix',1001,4000,2003,'Y'),
('Harry Potter and the Half-Blood Prince',1001,4000,2005,'Y'),
('The Ickabog',1001,4000,2020,'Y'),
('The Tales of Beedle the Bard',1001,4000,2008,'Y'),
('The Worst Witch Strikes Again',1002,4004,1980,'Y'),
('Peace at Last',1002,4004,1980,'Y'),
('Whatever Next',1002,4004,1983,'Y'),
('The Worst Witch',1002,4004,1974,'Y'),
('Five Minutes Peace',1002,4004,1986,'Y'),
('One snowy night',1003,4004,1989,'Y'),
('Percy the Park Keeper',1003,4004,1993,'Y'),
('A Flying Visit - A Percy the Park Keeper Story',1003,4004,2022,'Y'),
("Jasper's beanstalk",1003,4004,1992,'Y'),
('One Warm Fox',1003,4004,1997,'Y'),
('Room On The Broom',1004,4004,2001,'Y'),
('Zog',1004,4005,2010,'Y'),
('The Snail and the Whale',1004,4004,2003,'Y'),
("The Gruffalo's Child",1004,4004,2004,'Y'),
('Superworm',1004,4004,2012,'Y'),
('Tabby McTat',1004,4004,2009,'Y'),
('Monkey Puzzle',1004,4004,2000,'Y'),
('Elmer',1005,4004,1968,'Y'),
("Elmer's Special Day",1005,4004,1994,'Y'),
('Not Now Bernard',1005,4004,1980,'Y'),
("Elmer's Day",1005,4004,1994,'Y'),
('Two monsters',1005,4004,1985,'Y'),
('Two Can Toucan',1005,4004,1964,'Y'),
('Animal Farm',1006,4005,1945,'Y'),
('Homage to Catalonia',1006,4006,1938,'Y'),
('The Road to Wigan Pier',1006,4002,1936,'Y'),
('Noughts and Crosses',1007,4007,2001,'Y'),
('Cloud Busting',1007,4004,2004,'Y'),
("Boys Don't Cry",1007,4008,2010,'Y'),
('Murder on the Orient Express',1008,4009,1934,'Y'),
('Death on the Nile',1008,4009,1937,'Y'),
('The Murder of Roger Ackroyd',1008,4009,1926,'Y'),
('Great Expectations',1009,4010,1861,'Y'),
('David Copperfield',1009,4010,1850,'Y'),
('The Color Purple',1010,4011,1982,'Y'),
('The Way Forward is with a Broken Heart',1010,4002,2000,'Y'),
('How to Draw Comics the Marvel Way',1011,4012,1978,'Y'),
('The Great Gatsby',1012,4014,1925,'Y'),
('Tender Is the Night',1012,4014,1934,'Y'),
('The Beautiful and Damned',1012,4014,1934,'Y'),
('Of Mice and Men',1013,4014,1937,'Y'),
('Adventures of Huckleberry Finn',1014,4003,1884,'Y'),
('The Adventures of Tom Sawyer',1014,4003,1876,'Y'),
('Life on the Mississippi',1014,4006,1883,'Y'),
('To Kill a Mockingbird',1015,4010,1960,'Y'),
('The Shining',1016,4015,1977,'Y'),
('IT',1016,4015,1986,'Y'),
('Holly',1016,4015,2023,'Y'),
('Pet Sematary',1016,4015,1983,'Y'),
('The Very Hungry Caterpillar',1017,4004,1969,'Y'),
('Brown Bear, Brown Bear, What Do You See?',1017,4004,1967,'Y'),
('The Grouchy Ladybug',1017,4004,1977,'Y'),
('1st to Die',1018,4009,2001,'Y'),
('Along Came a Spider',1018,4009,1993,'Y'),
('The Murder Inn',1018,4009,2024,'Y'),
('Les Misérables',1019,4014,1862,'Y'),
('The Hunchback of Notre_dame',1019,4013,1831,'Y'),
('Captain Pamphile',1020,4003,1839,'Y'),
('The Three Musketeers',1020,4003,1844,'Y'),
('The Count of Monte Cristo',1020,4003,1845,'Y'),
('The First Man',1021,4002,1994,'Y');

```
Before populating my final table which was the borriwings table, I wanted to showcase my proficiency by using triggers to maintain database integrity. The triggers I used are basic in terms of how they function but are fit for purpose.

### Sql script used for triggers

```sql

-- Trigger to automatically update availability status in books table --

DELIMITER //

CREATE TRIGGER book_availability
AFTER INSERT ON borrowings 
FOR EACH ROW
BEGIN
	UPDATE books
    SET available_to_rent = 'N'
    WHERE
        book_id = NEW.book_id;
END //
DELIMITER ;

-- Trigger that will set book status back to available if return date is less than current real time date--

DELIMITER //

CREATE TRIGGER update_availability
AFTER INSERT ON borrowings
FOR EACH ROW 
BEGIN
	IF NEW.return_date < CURDATE() THEN 
           UPDATE books
           SET available_to_rent = 'Y'
           WHERE book_id = NEW.book_id;
	END IF ;
END //
DELIMITER ;


-- Trigger to update book availability back to 'Y' if row removed from borrowings table --

DELIMITER //

CREATE TRIGGER return_book_availability
AFTER DELETE ON borrowings
FOR EACH ROW 
BEGIN 
	UPDATE books
    SET available_to_rent = 'Y'
    WHERE 
		book_id = OLD.book_id;
END //

DELIMITER ;

```

### Sql script to populate borrowings table

```sql

 INSERT INTO borrowings (member_id, book_id, borrowing_date, return_date)
VALUES
(2000,3000,'2024-04-30','2024-05-28'), 
(2001,3001,'2024-04-03','2024-04-29'),
(2023,3000,'2024-01-05','2024-05-28'),
(2000,3060,'2024-02-02','2024-02-16'),
(2002,3003,'2024-01-03','2024-01-15'),
(2022,3070,'2024-01-16','2024-02-06'),
(2000,3050,'2024-01-03','2024-02-17'),
(2020,3079,'2024-05-01','2024-05-29'),
(2005,3010,'2024-05-01','2024-05-14'),
(2001,3002,'2023-03-01','2023-01-10'),
(2000,3004,'2023-02-01','2023-02-15'),
(2018,3033,'2023-04-07','2023-02-19'),
(2010,3080,'2024-03-11','2023-03-28'),
(2015,3019,'2023-06-02','2023-06-27'),
(2015,3070,'2023-06-26','2023-07-07'),
(2016,3045,'2024-04-28','2024-05-26'),
(2009,3022,'2024-01-06','2024-01-23'),
(2004,3010,'2024-01-06','2024-01-23'),
(2005,3077,'2024-02-08','2024-02-24'),
(2023,3022,'2024-04-01','2024-04-07'),
(2018,3045,'2023-10-02','2023-10-30'),
(2000,3067,'2023-10-07','2023-10-21'),
(2002,3028,'2023-10-15','2023-11-05'),
(2022,3012,'2023-10-04','2023-10-22'),
(2009,3060,'2023-10-01','2023-10-14'),
(2010,3039,'2023-11-09','2023-11-21'),
(2004,3059,'2023-11-02','2023-11-19'),
(2001,3079,'2023-11-04','2023-11-26'),
(2015,3033,'2023-11-18','2023-12-02'),
(2000,3065,'2023-11-03','2023-11-19'),
(2002,3078,'2023-11-14','2023-12-12'),
(2016,3060,'2023-11-01','2023-11-18'),
(2003,3055,'2023-11-02','2023-11-20'),
(2005,3011,'2023-11-23','2023-12-21'),
(2022,3024,'2023-11-19','2023-12-13'),
(2022,3065,'2023-01-04','2023-01-26'),
(2003,3025,'2023-01-04','2023-01-28'),
(2009,3076,'2023-01-06','2023-01-30'),
(2000,3056,'2023-01-04','2023-01-29'),
(2007,3042,'2023-01-04','2023-01-15'),
(2023,3013,'2023-01-09','2023-01-29'),
(2004,3068,'2023-01-05','2023-01-24'),
(2005,3065,'2023-01-27','2023-02-15'),
(2018,3032,'2023-01-05','2023-01-29'),
(2011,3023,'2023-01-09','2023-01-25'),
(2006,3014,'2023-01-10','2023-01-26'),
(2024,3011,'2023-01-04','2023-01-22'),
(2004,3072,'2023-01-29','2023-02-26'),
(2001,3019,'2023-02-28','2023-03-18'),
(2003,3027,'2023-02-28','2023-03-20'),
(2022,3059,'2023-02-02','2023-02-20'),
(2019,3038,'2023-02-09','2023-02-20'),
(2012,3001,'2023-02-11','2023-03-01'),
(2002,3028,'2023-03-01','2023-03-30'),
(2006,3024,'2023-03-02','2023-03-19'),
(2007,3007,'2023-03-01','2023-03-26'),
(2019,3005,'2023-03-01','2023-03-20'),
(2010,3010,'2023-03-02','2023-03-30'),
(2015,3016,'2023-03-01','2023-03-17'),
(2004,3000,'2023-03-02','2023-03-28'),
(2005,3039,'2023-03-02','2023-03-23'),
(2018,3022,'2023-03-09','2023-03-29'),
(2016,3073,'2023-03-10','2023-02-28'),
(2003,3056,'2023-03-22','2023-04-10'),
(2020,3018,'2023-03-15','2023-03-25'),
(2001,3028,'2023-04-04','2023-04-20'),
(2000,3050,'2023-04-01','2023-04-20'),
(2005,3069,'2023-04-01','2023-04-25'),
(2008,3077,'2023-04-12','2023-04-22'),
(2011,3043,'2023-04-03','2023-04-29'),
(2020,3079,'2023-04-10','2023-05-01'),
(2018,3055,'2023-04-01','2023-04-16'),
(2000,3049,'2023-05-01','2023-05-29'),
(2001,3027,'2023-05-09','2023-05-20'),
(2023,3076,'2023-05-19','2023-05-31'),
(2007,3068,'2023-05-06','2023-05-14'),
(2011,3042,'2023-05-03','2023-05-22'),
(2003,3080,'2023-06-01','2023-06-19'),
(2002,3053,'2023-06-03','2023-07-01'),
(2012,3021,'2023-06-09','2023-06-22'),
(2006,3048,'2023-06-01','2023-06-29'),
(2019,3049,'2023-07-02','2023-07-12'),
(2000,3029,'2023-07-01','2023-07-23'),
(2016,3074,'2023-07-09','2023-07-29'),
(2007,3038,'2023-07-01','2023-07-25'),
(2001,3030,'2023-08-01','2023-08-19'),
(2018,3022,'2023-08-01','2023-08-22'),
(2011,3071,'2023-08-02','2023-08-15'),
(2003,3039,'2023-08-19','2023-09-02'),
(2018,3078,'2023-09-01','2023-09-22'),
(2023,3043,'2023-09-01','2023-09-29'),
(2000,3057,'2023-09-01','2023-09-30'),
(2020,3038,'2023-10-03','2023-10-23'),
(2007,3039,'2023-10-01','2023-10-30'),
(2015,3015,'2023-10-09','2023-10-31'),
(2009,3077,'2023-10-01','2023-10-20'),
(2000,3063,'2023-11-01','2023-11-28'),
(2001,3020,'2023-11-01','2023-11-22'),
(2005,3030,'2023-11-09','2023-11-23'),
(2018,3056,'2023-11-19','2023-12-01'),
(2023,3072,'2023-12-01','2023-12-20'),
(2020,3047,'2023-12-02','2023-12-19'),
(2021,3018,'2023-12-01','2023-12-20'),
(2000,3055,'2023-12-01','2023-12-20'),
(2002,3060,'2023-12-01','2023-12-18'),
(2014,3033,'2024-01-04','2024-01-29'),
(2010,3010,'2024-01-04','2024-01-30'),
(2015,3049,'2024-01-04','2024-02-01'),
(2018,3022,'2024-01-08','2024-02-05'),
(2019,3028,'2024-02-02','2024-02-24'),
(2000,3018,'2024-03-07','2024-03-31'),
(2011,3011,'2024-03-01','2024-03-29'),
(2020,3064,'2024-03-04','2024-03-20'),
(2002,3079,'2024-03-06','2024-04-03'),
(2005,3057,'2024-03-07','2024-04-01'),
(2021,3021,'2024-03-01','2024-03-30'),
(2014,3014,'2024-03-01','2024-03-28'),
(2019,3019,'2024-03-03','2024-03-31'),
(2011,3027,'2024-03-03','2024-03-30'),
(2003,3053,'2024-03-03','2024-03-28'),
(2016,3076,'2024-03-05','2024-04-01'),
(2002,3013,'2024-04-28','2024-05-26'),
(2018,3070,'2024-04-19','2024-05-29'),
(2020,3023,'2024-05-01','2024-05-28');

```
Selecting a list of all the member_id's in the borrowings table allowed me to see which members had not borrowed any books.This then lead me to change their membership statuses to 'Inactive' to make the database more realistic.

### Script used to update membership status

```sql

-- No Borrowings for members 2013 and 2017 so will make membership status 'Inactive' --

UPDATE members
SET membership_status = 'Inactive'
WHERE member_id IN(2013,2017);

```
### Challenges faced 

One major challenge encountered during this project was populating the borrowings table before the genre table, resulting in error code 1452. Research revealed that attempting to populate the books table, which contains a foreign key constraint referencing the genres table, before the genres table was created led to this issue. This experience underscores the importance of understanding the sequence for populating tables in database creation to avoid such errors in the future.


### Lessons learned 

**Sequencing Importance**: Understanding the order of table population is crucial to prevent errors like code 1452 encountered when populating dependent tables before their references.

**Trigger Efficiency**: Leveraging triggers for data integrity maintenance automated processes, ensuring real-time database accuracy and enforcing business rules effectively.

**Documentation Clarity**: Comprehensive documentation, including design documents and data dictionaries, enhances project clarity and facilitates future maintenance and enhancements.

**Problem-Solving Adaptability**: Encountering challenges like foreign key constraints reinforced the importance of adaptability and persistence in finding optimal solutions and overcoming obstacles efficiently.
