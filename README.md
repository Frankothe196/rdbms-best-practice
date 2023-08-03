# Relational Database Normalization; A Normalization Guide

Database normalization is a process that involves organizing the data in a relational database to minimize redundancy and improve data integrity. It helps maintain data consistency and reduces the risk of data anomalies. There are several normal forms that a database can be normalized into, each with its own set of rules. 
In this guide, we will explore the first three normal forms (1NF, 2NF, and 3NF) with examples at each step.

## Table of Contents
   - [Introduction](#intro)
1. [First Normal Form (1NF)](#1nf)
2. [Second Normal Form (2NF)](#2nf)
3. [Third Normal Form (3NF)](#3nf)

## Introduction <a name='intro'></a>
Database normalization is a technique used to design efficient and robust databases by reducing data redundancy. It involves breaking down a large table into smaller, related tables that can be linked using relationships. By doing so, we ensure that each piece of data is stored in only one place, reducing the chances of inconsistency and update anomalies.

## 1. First Normal Form (1NF) <a name='1nf'></a>
In the first normal form, the table is organized so that each cell contains a single value, and there are no repeating groups or arrays within a record. To achieve 1NF, we split the data into multiple tables, each with a unique primary key.
### Rules:
1. Creating multiple columns to convey information is not permitted
2. Mixing data types in the same column is not permitted
3. Every table needs a primary key
4. Grouping data into a value is not permitted, e.g 'Python, Java, SQL'
5. Do
### Example:
Original Table - Employee
| Employee_ID | Employee_Name | Skills                |
|-------------|---------------|-----------------------|
| 1           | John          | Python, Java, SQL     |
| 2           | Jane          | HTML, CSS, JavaScript |

Normalized Tables:
Table - Employee
| Employee_ID | Employee_Name |
|-------------|---------------|
| 1           | John          |
| 2           | Jane          |

Table - Skills
| Skill_ID | Skill       |
|-------------|-------------|
| 1           | Python      |
| 1           | Java        |
| 1           | SQL         |
| 2           | HTML        |
| 2           | CSS         |
| 2           | JavaScript  |

## 2. Second Normal Form (2NF)<a name='2nf'></a>
In the second normal form, the table should be in 1NF, and each non-key attribute should be fully dependent on the entire primary key. If an attribute is only partially dependent on the primary key, it should be moved to a separate table.
### Rules:
1. Each non key attribute in the table must be entirely dependent on the primary key on not just a part of it

### Example:
Original Table - Order_Details
| Order_ID | Product_ID | Product_Name | Quantity |
|----------|------------|--------------|----------|
| 1001     | 1          | Laptop       | 2        |
| 1001     | 2          | Smartphone   | 3        |
| 1002     | 1          | Laptop       | 1        |

Normalized Tables:
Table - Products
| Product_ID | Product_Name |
|------------|--------------|
| 1          | Laptop       |
| 2          | Smartphone   |

Table - Order_Details
| Order_ID | Product_ID | Quantity |
|----------|------------|----------|
| 1001     | 1          | 2        |
| 1001     | 2          | 3        |
| 1002     | 1          | 1        |

## 3. Third Normal Form (3NF)<a name='3nf'></a>
In the third normal form, the table should be in 2NF, and no non-key attribute should be transitively dependent on the primary key. If a non-key attribute depends on another non-key attribute, it should be moved to a separate table.
### Rules:
1. Each non-key attribute in the table must be dependent on the key, and nothing but the key

### Example:
Original Table - Student_Courses
| Student_ID | Student_Name | Course_ID | Course_Name | Instructor    |
|------------|--------------|-----------|-------------|---------------|
| 101        | Jamie        | 1         | Math        | Prof. Smith   |
| 101        | Jamie        | 2         | Science     | Prof. Johnson |
| 102        | Carlson      | 1         | Math        | Prof. Smith   |

Normalized Tables:
Table - Students
| Student_ID | Student_Name |
|------------|--------------|
| 101        | Jamie        |
| 102        | Carlson      |

Table - Student Enrollemnt
| Enrollment_id | Student_ID | Course_ID |
|---------------|------------|-----------|
| 1             | 101        | 1         |
| 2             | 101        | 2         |
| 3             | 102        | 1         |

Table - Courses
| Course_ID | Course_Name |
|-----------|-------------|
| 1         | Math        |
| 2         | Science     |

Table - Course_Instructors
| Course_ID | Instructor    |
|-----------|---------------|
| 1         | Prof. Smith   |
| 2         | Prof. Johnson |



