# Library Database 📖

#### Full sql code can be found above as file ( library.sql   FULL PROJECT )

### Key Table of Contens

- [Entity Relationship Diagram](#entity-relationship-diagram) 🖼️
- [Database Legend](#database-legend) 💻
- [Sql script used for triggers](#sql-script-used-for-triggers) 🖊️
- [Sql script to populate borrowings table](#sql-script-to-populate-borrowings-table) 🖋️
- [Script used to update membership status](#script-used-to-update-membership-status)🖊️
- [Challenges faced](#challenges-faced) 🤯
- [Lessons learned](#lessons-learned) 💡

### Project Overview

This Library database project aims to efficiently manage book inventory, member data, and borrowing activities with this comprehensive database system tailored for libraries,utilising relational database principles and SQL queries for seamless operations and insightful analytics.


### Key Highlights  

- **Comprehensive Structure**: Meticulously crafted tables for books, authors, genres, members, and borrowings, reflecting a deep understanding of relational database principles.
  
- **Data Integrity**: Implemented with precision, ensuring each column has appropriate data types and constraints for reliable data management and accuracy.
  
- **Automation with Triggers**: Utilized triggers to automate crucial processes, such as updating book availability status, enhancing efficiency and maintaining database integrity.
  
- **Realistic Sample Data**: Includes realistic sample data for thorough testing and demonstration, providing recruiters with a tangible understanding of my SQL skills.


##   Documentation

### Entity Relationship Diagram
![Entity Relationship Diagram](https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/113e98e3-b20a-42ce-8d90-67b5aead4c75)

### Database Legend 

I manually populated all tables. To assign genre IDs to the books table accurately, I created a legend, ensuring each book was categorised correctly and avoiding errors. Similarly, I created a legend for the authors table to easily assign the correct author ID in the books table.

<img width="403" alt="Lengend for genre and author tables" src="https://github.com/JoshuaAsante1997/Library-Database/assets/149339304/1d6630b1-e837-4e84-986b-14bb61423bde">



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
