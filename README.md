
# Students Database Management Administartion
##  SQL_Queries-DDL(Data Definition Language)
1. CREATE a Table
```
CREATE DATABASE db1;           /*creating a databse as db1*/
USE db1;                      /*getting the acess to the database for Creating table*/  

CREATE TABLE Students ( 
    roll_number INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE,
    gender VARCHAR(10),
    email VARCHAR(100),
    phone_number VARCHAR(15)
);                             /*created a table for Students with diffrent coloumn name*/

```
Output:

![query1](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/d33a2b99-4b8a-45c0-8f05-d713f32039f0)

```
CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    course_grade INT
    );                          /*created a table for Courses with diffrent coloumn name*/

```
Output:

![query3](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/87ee9217-f732-40fa-80d7-17b05d2897dd)


```
CREATE TABLE Enroll (
    enroll_id INT PRIMARY KEY,
    roll_number INT,
    course_id INT,
    enroll_date DATE,
    FOREIGN KEY (roll_number) REFERENCES Students(roll_number),               
    FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);                            /*created a table for Enroll with diffrent coloumn name and also created a refrences */
```
Output:

![query2](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/af194cb6-fc90-487f-afdb-0aa59f6b8554)
```
CREATE TABLE  Fees (
     course_id INT PRIMARY KEY,
     course_fee INT           
 );                            /*created a table for Fees with diffrent coloumn name*/
```
Output:

![query4](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/873d04e1-b327-4c0c-a52c-e249e71e0567)


2. DROP a table
```
DROP TABLE Fees;            /*deleting a table completely form a database which cannot be retrive*/ 
```
Output:

![query5](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/77c5890b-59bb-42ad-ab49-575e5220dbb6)


3. ALTER a table
```
 ALTER TABLE Courses
 ADD course_fee INT;     /*Adding a coloumn to a table with the help of ALTER TABLE*/ 
```
Output:

![query6](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/e08442bd-3720-4c86-9cf1-f91e3b199008)


```
 ALTER TABLE students
 DROP COLUMN phone_number;      /*Droping a coloumn that is of no use*/
```
Output:

![Screenshot 2023-08-01 140409](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/96df6fff-32e4-4a05-a79b-57ab7c50171b)


4. TRUNCATE a table
```
TRUNCATE TABLE Fees;      /*deleting a table and data inside completely form a database which can be backuped*/
```
Output:

![query7](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/29ac5e5d-ff95-40ec-851e-9359b338bb3c)

## SQL_Queries-DML(Data Manipulation Language)
1. INSERT
```
                -- Insert data into 'students' table
INSERT INTO students (roll_number, first_name, last_name, date_of_birth, gender, email)
VALUES
  (202310, 'Venky', 'S', '1997-01-27', 'M', 'venky.s@gmail.com'),
  (202311, 'Lingaraj', 'Samantray','1996-11-12', 'M', 'lingaraj.samantray@gmail.com'),
  (202312, 'Asutosh', 'Padhy', '1999-08-07','M',  'asutosh.padhy@gmail.com'),
  (202313, 'Asutosh', 'Gouda', '1995-08-07','M',  'asutosh.gouda@outlook.com'),
  (202314, 'Sudip', 'Gouda', '1997-09-03','M',  'sudipgouda123@gmail.com'),
  (202315, 'Sumit', 'Pattnaik', '1997-04-07','M',  'sumit.pattnaik@gmail.com'),
  (202316, 'Sasmita', 'Sen', '1998-03-30','F',  'sasmita.sen@gmail.com'),
  (202317, 'Gayatri', 'Behera', '1997-03-25','F',  'gayatri.behera@gmail.com'),
  (202318, 'Venaktesh', 'G', '1990-04-27','M',  'venaktesh.g@gmail.com'),
  (202319, 'Sunil', 'Setthy', '1997-06-19','M',  'sunil.setthy@gmail.com');
```
Output:

![query8](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/9e10f61e-d0fb-4c16-abff-ba0f1ca4ee65)

                -- Insert data into 'courses' table
```
INSERT INTO courses (course_id, course_name, course_grade)
VALUES
  (101, 'Mathematics', 4),
  (102, 'History', 3),
  (103, 'Biology', 4),
  (104, 'English', 2),
  (105, 'Geography', 3),
  (106, 'Genaral Knowlegde', 3);
```
Output:

![query9](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/3f950a94-639f-4a15-834c-68d484562da5)

                   -- Insert data into 'enroll' table
```                   
INSERT INTO enroll (enroll_id, roll_number, course_id,enroll_date)
VALUES  (21501, 202314, 103, '2023-06-15'),
		(21502, 202319, 106, '2023-04-22'),
        (21503, 202310, 103, '2023-06-10'),
        (21504, 202318, 105, '2023-05-05'),
        (21505, 202316, 101, '2023-05-02'),
        (21506, 202311, 102, '2023-06-27'),
        (21507, 202312, 104, '2023-04-25'),
        (21508, 202315, 102, '2023-05-19');
```
Output:

![query10](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/60dfa367-407c-435a-be4c-3e3fff96bae8)

2.UPDATE
```
UPDATE courses
SET course_grade=4
WHERE course_id=105;                /* Updating the vlaues in a courses table */
```
Output:

![query11](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/208fd9ed-559a-490c-95af-125067de2a7e)

```
UPDATE students
SET first_name='Preeti', email='preeti.behera@gmail.com'
WHERE roll_number=202317;           /* Updating multiple vlaues in a students table */
```
Output:

![query12](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/585a1997-651c-41c0-834b-730d3dd59eef)

3.DELETE
```
-- Here I added a fees table and inserted a data to show the execution of DELETE Command
DELETE FROM fees
WHERE course_id=106;
```
Output:

![query13](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/ef60b748-32c1-4ef1-a2d8-3559fd05f798)     ![query14](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/ee71a411-1ec6-4583-a827-bde4f4ffd245)

4.SELECT
```
SELECT roll_number, first_name, date_of_birth
FROM students;
```
Output:

![query15](https://github.com/Sudipta-Gouda/SQL-/assets/139854937/c89a9d2d-0d31-44fb-b872-3f33dd68eb4b)

# SQL_Queries




