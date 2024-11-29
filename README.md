# Library Management System SQL Project

## Project Overview

**Project Title**: Library Management System

This project demonstrates the implementation of a Library Management System using SQL. It includes creating and managing tables, performing CRUD operations, and executing advanced SQL queries. The goal is to showcase skills in database design, manipulation, and querying.

## Objectives

**1. Set up the Library Management System Database**: Create and populate the database with tables for branches, employees, members, books, issued status
**2. CRUD Operations**: Perform Create, Read, Update, and Delete operations on the data.
**3. CTAS (Create Table As Select)**: Utilize CTAS to create new tables based on query results.

## Project Structure

### 1. Database Setup

**- Database Creation**: Created a database named library_db.
**- Table Creation**: Created tables for branches, employees, members, books, issued status. Each table includes relevant columns and relationships.

create table branch(

branch_id varchar(10)primary key,

manager_id varchar(10),

branch_address varchar(55),

contact_no varchar(10));


alter table branch

alter column contact_no type varchar(20);


create table employees(

emp_id varchar(10) primary key,

emp_name varchar(25),

position varchar(15),

salary int,

branch_id varchar(25));


create table books(

isbn varchar(20) primary key,	

book_title varchar(75),	

category varchar(10),	

rental_price float,

status varchar(15),

author varchar(35),

publisher varchar(55));


alter table books

alter column category type varchar(20);


create table members(

member_id varchar(10)primary key,

member_name varchar(25),

member_address varchar(75),

reg_date date);


create table issued_status(

issued_id varchar(10) primary key,

issued_member_id varchar(10),

issued_book_name varchar(75),

issued_date date,

issued_book_isbn varchar(25),	

issued_emp_id varchar(10));


alter table issued_status

add constraint fk_members

foreign key(issued_member_id)references members(member_id);

alter table issued_status

add constraint fk_books

foreign key(issued_book_isbn)references books(isbn);

alter table employees

add constraint fk_branch

foreign key(branch_id)references branch(branch_id);

alter table issued_status

add constraint fk_employees

foreign key(issued_emp_id)references employees(emp_id);

### 2. CRUD Operations
**- Create**: Inserted sample records into the books table.

**- Read**: Retrieved and displayed data from various tables.

**- Update**: Updated records in the employees table.

**- Delete**: Removed records from the members table as needed.

**Task 1. Create a New Book Record** -- "('978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.')"

INSERT INTO books(isbn, book_title, category, rental_price, status, author, publisher)

VALUES('978-1-60129-456-2', 'To Kill a Mockingbird', 'Classic', 6.00, 'yes', 'Harper Lee', 'J.B. Lippincott & Co.');

SELECT * FROM books;

**Task 2: Update an Existing Member's Address**

UPDATE members

SET member_address = '125 Oak St'

WHERE member_id = 'C103';

**Task 3: Delete a Record from the Issued Status Table** -- Objective: Delete the record with issued_id = 'IS121' from the issued_status table.

DELETE FROM issued_status

WHERE   issued_id =   'IS121';

**Task 4: Retrieve All Books Issued by a Specific Employee** -- Objective: Select all books issued by the employee with emp_id = 'E101'.

SELECT * FROM issued_status

WHERE issued_emp_id = 'E101'

**Task 5: List Members Who Have Issued More Than One Book** -- Objective: Use GROUP BY to find members who have issued more than one book.

SELECT issued_emp_id, COUNT(*)

FROM issued_status

GROUP BY 1

HAVING COUNT(*) > 1
