# SQL-
## Code for students database managemnet administartion
```
CREATE DATABASE db1;
USE db1;

CREATE TABLE Students (
    roll_number INT PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    date_of_birth DATE,
    gender VARCHAR(10),
    email VARCHAR(100),
    phone_number VARCHAR(15)
);
```
![alt text](query1.png)
```
CREATE TABLE Courses (
    course_id INT PRIMARY KEY,
    course_name VARCHAR(100),
    course_grade INT
    
);

CREATE TABLE Enroll (
    enroll_id INT PRIMARY KEY,
    roll_number INT,
    course_id INT,
    enroll_date DATE,
	FOREIGN KEY (roll_number) REFERENCES Students(roll_number),
	FOREIGN KEY (course_id) REFERENCES Courses(course_id)
);
```
