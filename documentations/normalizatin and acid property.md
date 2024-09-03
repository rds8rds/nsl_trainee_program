# Table of Contents

- 1. [DBMS Keys: Candidate, Super, Primary, Foreign Key Types with Example](#1-dbms-keys-candidate-super-primary-foreign-key-types-with-example)
  - 1.1. [What are Keys in DBMS?](#11-what-are-keys-in-dbms)
  - 1.2. [Types of Keys in DBMS (Database Management System)](#12-types-of-keys-in-dbms-database-management-system)
  - 1.2.1. [What is the Super Key?](#121-what-is-the-super-key)
  - 1.2.2. [What is a Primary Key?](#122-what-is-a-primary-key)
  - 1.2.3. [What is the Alternate Key?](#123-what-is-the-alternate-key)
  - 1.2.4. [What is a Candidate Key?](#124-what-is-a-candidate-key)
  - 1.2.5. [What is the Foreign Key?](#125-what-is-the-foreign-key)
  - 1.2.6. [What is the Compound Key?](#126-what-is-the-compound-key)
  - 1.2.7. [What is the Composite Key?](#127-what-is-the-composite-key)
  - 1.2.8. [What is a Surrogate Key?](#128-what-is-a-surrogate-key)
  - 1.2.9. [Difference Between Primary Key & Foreign Key](#129-difference-between-primary-key--foreign-key)
  - 1.3. [Why we need a Key?](#13-why-we-need-a-key)
- 2. [Introduction to Database Normalization](#2-introduction-to-database-normalization)
  - 2.1. [Objectives of Normalization](#21-objectives-of-normalization)
  - 2.2. [Normal Forms](#22-normal-forms)
    - 2.2.1. [First Normal Form (1NF)](#221-first-normal-form-1nf)
    - 2.2.2. [Second Normal Form (2NF)](#222-second-normal-form-2nf)
    - 2.2.3. [Third Normal Form (3NF)](#223-third-normal-form-3nf)
  - 2.3. [Higher Normal Forms](#23-higher-normal-forms)
    - 2.3.1. [Boyce-Codd Normal Form (BCNF)](#231-boyce-codd-normal-form-bcnf)
    - 2.3.2. [Fourth Normal Form (4NF)](#232-fourth-normal-form-4nf)
    - 2.3.3. [Fifth Normal Form (5NF)](#233-fifth-normal-form-5nf)
  - 2.4. [Benefits of Normalization](#24-benefits-of-normalization)
  - 2.5. [Trade-Offs](#25-trade-offs)
- 3. [ACID Properties in DBMS](#3-acid-properties-in-dbms)
  - 3.1. [Atomicity](#31-atomicity)
  - 3.2. [Consistency](#32-consistency)
  - 3.3. [Isolation](#33-isolation)
  - 3.4. [Durablity](#34-durability)
  - 3.5. [Advantages of ACID Properties in DBMS](#35-advantages-of-acid-properties-in-dbms)
  - 3.6. [Disadvantages of ACID Properties in DBMS](#36-disadvantages-of-acid-properties-in-dbms)



# [1. DBMS Keys: Candidate, Super, Primary, Foreign Key Types with Example](#table-of-contents)
## [1.1 What are Keys in DBMS?](#table-of-contents)
KEYS in DBMS is an attribute or set of attributes which helps you to identify a row(tuple) in a relation(table). They allow you to find the relation between two tables. Keys help you uniquely identify a row in a table by a combination of one or more columns in that table. Key is also helpful for finding unique record or row from the table. Database key is also helpful for finding unique record or row from the table.

| Employee ID | FirstName | LastName |
|-------------|-----------|----------|
| 11          | Andrew    | Johnson  |
| 22          | Tom       | Wood     |
| 33          | Alex      | Hale     |


In the above-given example, employee ID is a primary key because it uniquely identifies an employee record. In this table, no other employee can have the same employee ID.


## [1.2 Types of Keys in DBMS (Database Management System)](#table-of-contents)
There are mainly Eight different types of Keys in DBMS and each key has it’s different functionality:

**Super Key** – A super key is a group of single or multiple keys which identifies rows in a table.\
**Primary Key** – is a column or group of columns in a table that uniquely identify every row in that table.\
**Candidate Key** – is a set of attributes that uniquely identify tuples in a table. Candidate Key is a super key with no repeated attributes.\
**Alternate Key** – is a column or group of columns in a table that uniquely identify every row in that table.\
**Foreign Key** – is a column that creates a relationship between two tables. The purpose of Foreign keys is to maintain data integrity and allow navigation between two different instances of an entity.\
**Compound Key** – has two or more attributes that allow you to uniquely recognize a specific record. It is possible that each column may not be unique by itself within the database.\
**Composite Key** – is a combination of two or more columns that uniquely identify rows in a table. The combination of columns guarantees uniqueness, though individual uniqueness is not guaranteed.\
**Surrogate Key** – An artificial key which aims to uniquely identify each record is called a surrogate key. These kind of key are unique because they are created when you don’t have any natural primary key.

### [1.2.1 What is the Super key?](#table-of-contents)
A superkey is a group of single or multiple keys which identifies rows in a table. A Super key may have additional attributes that are not needed for unique identification.

| EmpSSN      | EmpNum | Empname |
|-------------|--------|---------|
| 9812345098  | AB05   | Shown   |
| 9876512345  | AB06   | Roslyn  |
| 199937890   | AB07   | James   |

In the above-given example, EmpSSN(Employe Social Security Number) and EmpNum name are superkeys.

### [1.2.2 What is a Primary Key?](#table-of-contents)

**PRIMARY KEY** in [DBMS](https://www.guru99.com/dbms-tutorial.html) is a column or group of columns in a table that uniquely identify every row in that table. The Primary Key can’t be a duplicate meaning the same value can’t appear more than once in the table. A table cannot have more than one primary key.

#### Rules for defining Primary key:

- Two rows can’t have the same primary key value
- It must for every row to have a primary key value.
- The primary key field cannot be null.
- The value in a primary key column can never be modified or updated if any foreign key refers to that primary key.

**Example:**

In the following example, `StudID` is a Primary Key.

| StudID | Roll No | First Name | LastName | Email |
| --- | --- | --- | --- | --- |
| 1 | 11 | Tom | Price | abc@gmail.com |
| 2 | 12 | Nick | Wright | xyz@gmail.com |
| 3 | 13 | Dana | Natan | mno@yahoo.com |

### [1.2.3 What is the Alternate key?](#table-of-contents)

**ALTERNATE KEYS** is a column or group of columns in a table that uniquely identify every row in that table. A table can have multiple choices for a primary key but only one can be set as the primary key. All the keys which are not primary key are called an Alternate Key.

**Example:**
In this table, StudID, Roll No, Email are qualified to become a primary key. But since StudID is the primary key, Roll No, Email becomes the alternative key.

| StudID | Roll No | First Name | LastName | Email |
| --- | --- | --- | --- | --- |
| 1 | 11 | Tom | Price | abc@gmail.com |
| 2 | 12 | Nick | Wright | xyz@gmail.com |
| 3 | 13 | Dana | Natan | mno@yahoo.com |


### [1.2.4 What is a Candidate Key?](#table-of-contents)
**CANDIDATE KEY** in SQL is a set of attributes that uniquely identify tuples in a table. Candidate Key is a super key with no repeated attributes. The Primary key should be selected from the candidate keys. Every table must have at least a single candidate key. A table can have multiple candidate keys but only a single primary key.

**Properties of Candidate key:**

- It must contain unique values
- Candidate key in SQL may have multiple attributes
- Must not contain null values
- It should contain minimum fields to ensure uniqueness
- Uniquely identify each record in a table

Candidate key Example: In the given table Stud ID, Roll No, and email are candidate keys which help us to uniquely identify the student record in the table.

| StudID | Roll No | First Name | LastName | Email |
| --- | --- | --- | --- | --- |
| 1 | 11 | Tom | Price | abc@gmail.com |
| 2 | 12 | Nick | Wright | xyz@gmail.com |
| 3 | 13 | Dana | Natan | mno@yahoo.com |


<p align="center">
  <img src="https://www.guru99.com/images/1/100518_0517_DBMSKeysPri1.png" />
</p>
<p style = "text-align:center">Candidate Key in DBMS</p>

### [1.2.5 What is the Foreign key?](#table-of-contents)

**FOREIGN KEY** is a column that creates a relationship between two tables. The purpose of Foreign keys is to maintain data integrity and allow navigation between two different instances of an entity. It acts as a cross-reference between two tables as it references the primary key of another table.

**Example:**

| DeptCode | DeptName |
| --- | --- |
| 001 | Science |
| 002 | English |
| 005 | Computer |

| Teacher ID | Fname | Lname |
| --- | --- | --- |
| B002 | David | Warner |
| B017 | Sara | Joseph |
| B009 | Mike | Brunton |

In this key in dbms example, we have two table, teach and department in a school. However, there is no way to see which search work in which department.

In this table, adding the foreign key in Deptcode to the Teacher name, we can create a relationship between the two tables.

| Teacher ID | DeptCode | Fname | Lname |
| --- | --- | --- | --- |
| B002 | 002 | David | Warner |
| B017 | 002 | Sara | Joseph |
| B009 | 001 | Mike | Brunton |

This concept is also known as Referential Integrity.


### [1.2.6 What is the Compound key?](#table-of-contents)

**COMPOUND KEY** has two or more attributes that allow you to uniquely recognize a specific record. It is possible that each column may not be unique by itself within the database. However, when combined with the other column or columns the combination of composite keys become unique. The purpose of the compound key in database is to uniquely identify each record in the table.

**Example:**

| OrderNo | PorductID | Product Name | Quantity |
| --- | --- | --- | --- |
| B005 | JAP102459 | Mouse | 5 |
| B005 | DKT321573 | USB | 10 |
| B005 | OMG446789 | LCD Monitor | 20 |
| B004 | DKT321573 | USB | 15 |
| B002 | OMG446789 | Laser Printer | 3 |

In this example, OrderNo and ProductID can’t be a primary key as it does not uniquely identify a record. However, a compound key of Order ID and Product ID could be used as it uniquely identified each record.

### [1.2.7 What is the Composite key?](#table-of-contents)

**COMPOSITE KEY** is a combination of two or more columns that uniquely identify rows in a table. The combination of columns guarantees uniqueness, though individually uniqueness is not guaranteed. Hence, they are combined to uniquely identify records in a table.

The difference between compound and the composite key is that any part of the compound key can be a foreign key, but the composite key may or maybe not a part of the foreign key.

### [1.2.8 What is a Surrogate key?](#table-of-contents)

**SURROGATE KEYS** is An artificial key which aims to uniquely identify each record is called a surrogate key. This kind of partial key in dbms is unique because it is created when you don’t have any natural primary key. They do not lend any meaning to the data in the table. Surrogate key in DBMS is usually an integer. A surrogate key is a value generated right before the record is inserted into a table.

| Fname | Lastname | Start Time | End Time |
| --- | --- | --- | --- |
| Anne | Smith | 09:00 | 18:00 |
| Jack | Francis | 08:00 | 17:00 |
| Anna | McLean | 11:00 | 20:00 |
| Shown | Willam | 14:00 | 23:00 |

Above, given example, shown shift timings of the different employee. In this example, a surrogate key is needed to uniquely identify each employee.

Surrogate keys in [sql](https://www.guru99.com/sql.html) are allowed when

- No property has the parameter of the primary key.
- In the table when the primary key is too big or complicated.

### [1.2.9 Difference Between Primary key & Foreign key](#table-of-contents)

Following is the main difference between primary key and foreign key:

| Primary Key | Foreign Key |
| --- | --- |
| Helps you to uniquely identify a record in the table. | It is a field in the table that is the primary key of another table. |
| Primary Key never accept null values. | A foreign key may accept multiple null values. |
| Primary key is a clustered index and data in the DBMS table are physically organized in the sequence of the clustered index. | A foreign key cannot automatically create an index, clustered or non-clustered. However, you can manually create an index on the foreign key. |
| You can have the single Primary key in a table. | You can have multiple foreign keys in a table. |


### [1.2.10 Summary](#table-of-contents)

- What is key in DBMS: A key in DBMS is an attribute or set of attributes which helps you to identify a row(tuple) in a relation(table)
- Keys in [RDBMS](https://www.guru99.com/relational-data-model-dbms.html) allow you to establish a relationship between and identify the relation between tables
- Eight types of key in DBMS are Super, Primary, Candidate, Alternate, Foreign, Compound, Composite, and Surrogate Key.
- A super key is a group of single or multiple keys which identifies rows in a table.
- A column or group of columns in a table which helps us to uniquely identifies every row in that table is called a primary key
- All the different keys in DBMS which are not primary key are called an alternate key
- A super key with no repeated attribute is called candidate key
- A compound key is a key which has many fields which allow you to uniquely recognize a specific record
- A key which has multiple attributes to uniquely identify rows in a table is called a composite key
- An artificial key which aims to uniquely identify each record is called a surrogate key
- Primary Key never accept null values while a foreign key may accept multiple null values.


## [1.3 Why we need a Key?](#table-of-contents)
Here are some reasons for using sql key in the DBMS system.

Keys help you to identify any row of data in a table. In a real-world application, a table could contain thousands of records. Moreover, the records could be duplicated. Keys in RDBMS ensure that you can uniquely identify a table record despite these challenges.
Allows you to establish a relationship between and identify the relation between tables
Help you to enforce identity and integrity in the relationship.





# [2. Introduction to Database Normalization](#table-of-contents)

**Database normalization** is a systematic approach of organizing data in a relational database to minimize redundancy and improve data integrity. The process involves dividing a database into two or more tables and defining relationships between the tables to ensure data dependencies are logical and stored efficiently.

## [2.1 Objectives of Normalization](#table-of-contents)

Normalization has several key objectives:

- **Reduce Data Redundancy**: Eliminate duplicate data to save storage and prevent inconsistencies.
- **Improve Data Integrity**: Ensure that the data is accurate and consistent across the database.
- **Optimize Query Performance**: Organize data in a way that reduces the amount of data that needs to be processed during queries.
- **Ensure Logical Data Dependencies**: Maintain a clear, logical relationship between the data, ensuring that changes in one area of the database do not inadvertently affect unrelated data.

## [2.2 Normal Forms](#table-of-contents)

Normalization is carried out through a series of stages known as *normal forms*. Each normal form addresses specific types of anomalies and dependencies, refining the database structure step by step.

### [2.2.1 First Normal Form (1NF)](#table-of-contents)
**Objective**: Ensure each column contains only atomic values, meaning that the values in each column are indivisible.

> Criteria:
1. **Atomicity**: Each column should contain only atomic (indivisible) values. This means no multi-valued attributes are allowed; each field must contain only a single value.
2. **Uniqueness**: Each row must be unique, meaning that there is a primary key that uniquely identifies each record.
3. **No Repeating Groups**: There should be no repeating groups or arrays in a table. This means you should not have multiple columns for the same type of data.

> Example of a Table Not in 1NF:

| StudentID | Name | Courses |
| --- | --- | --- |
| 1 | Alice | Math, Physics |
| 2 | Bob | Chemistry |
| 3 | Charlie | Biology, Math |

In this table, the `Courses` column contains multiple values (e.g., "Math, Physics"), which violates the atomicity requirement.

> Example of the Same Table in 1NF:

| StudentID | Name | Course |
| --- | --- | --- |
| 1 | Alice | Math |
| 1 | Alice | Physics |
| 2 | Bob | Chemistry |
| 3 | Charlie | Biology |
| 3 | Charlie | Math |

In this 1NF-compliant table:

- Each `Course` entry is atomic, containing only one value.
- No repeating groups exist, and the `StudentID` combined with `Course` can be used as a composite key if needed.
This structure ensures that the database is in the first normal form, allowing for better data management and querying.
### [2.2.2 Second Normal Form (2NF)](#table-of-contents)
**Objective**: Ensure that all non-key attributes are fully functionally dependent on the entire primary key, not just a part of it.
> Criteria
 - It is in 1NF: The table must first satisfy all the conditions of First Normal Form (1NF), meaning that it has atomic columns, no repeating groups, and a unique primary key.
 - No Partial Dependency: All non-key attributes (columns that are not part of the primary key) must depend on the entire primary key, not just part of it. This means there should be no partial dependency of any column on the primary key.
  
> Example of a Table in 1NF but Not in 2NF:

| StudentID | Course | Instructor | InstructorLocation |
| --- | --- | --- | --- |
| 1 | Math | Dr. Smith | Room 101 |
| 1 | Physics | Dr. Brown | Room 102 |
| 2 | Chemistry | Dr. White | Room 103 |
| 2 | Biology | Dr. Green | Room 104 |

Here, the composite primary key is `(StudentID, Course)`. However, `Instructor` and `InstructorLocation` depend only on `Course`, not the entire composite key `(StudentID, Course)`. This creates a partial dependency, violating 2NF.

> Example of the Same Table in 2NF:

**Student-Course Table:**

| StudentID | Course |
| --- | --- |
| 1 | Math |
| 1 | Physics |
| 2 | Chemistry |
| 2 | Biology |

**Course-Instructor Table:**

| Course | Instructor | InstructorLocation |
| --- | --- | --- |
| Math | Dr. Smith | Room 101 |
| Physics | Dr. Brown | Room 102 |
| Chemistry | Dr. White | Room 103 |
| Biology | Dr. Green | Room 104 |

In the 2NF-compliant structure:

- The `Student-Course` table contains only the primary key (no partial dependencies).
- The `Course-Instructor` table links each course to its instructor and location, ensuring that the non-key attributes (`Instructor` and `InstructorLocation`) depend only on the `Course`, which is now the primary key in that table.

This normalization eliminates partial dependencies, reducing redundancy and improving data integrity.

### [2.2.3 Third Normal Form (3NF)](#table-of-contents)
**Objective**: Ensure that no non-key attribute depends on another non-key attribute (eliminate transitive dependencies).
> Criteria:
  - Meet all requirements of 2NF.
  - Ensure that non-key attributes depend only on the primary key.
  - Eliminate transitive dependencies, where a non-key attribute depends on another non-key attribute.

> Example of a Table in 2NF but Not in 3NF:

| StudentID | Course | Instructor | InstructorLocation |
| --- | --- | --- | --- |
| 1 | Math | Dr. Smith | Room 101 |
| 1 | Physics | Dr. Brown | Room 102 |
| 2 | Chemistry | Dr. White | Room 103 |
| 2 | Biology | Dr. Green | Room 104 |

Here:

- The table is in 2NF, as there are no partial dependencies.
- However, there is a transitive dependency: `InstructorLocation` depends on `Instructor`, which is a non-key attribute.

> Example of the Same Table in 3NF:

**Student-Course Table:**

| StudentID | Course |
| --- | --- |
| 1 | Math |
| 1 | Physics |
| 2 | Chemistry |
| 2 | Biology |

**Course-Instructor Table:**

| Course | Instructor |
| --- | --- |
| Math | Dr. Smith |
| Physics | Dr. Brown |
| Chemistry | Dr. White |
| Biology | Dr. Green |

**Instructor-Location Table:**

| Instructor | InstructorLocation |
| --- | --- |
| Dr. Smith | Room 101 |
| Dr. Brown | Room 102 |
| Dr. White | Room 103 |
| Dr. Green | Room 104 |

In this 3NF-compliant structure:

- The `Student-Course` table has only a primary key and no transitive dependencies.
- The `Course-Instructor` table maps each course to its instructor, with no additional non-key attributes.
- The `Instructor-Location` table links each instructor to their location.

This normalization step ensures that there are no transitive dependencies, further reducing redundancy and improving data integrity.

## [2.3 Higher Normal Forms](#table-of-contents)

Beyond the third normal form, there are additional, more stringent normal forms:

### [2.3.1 Boyce-Codd Normal Form (BCNF)](#table-of-contents)
**Objective**: Ensure that every determinant is a candidate key.
> Criteria:
  - Meet all requirements of 3NF.
  - Every determinant (an attribute on which some other attribute is fully functionally dependent) should be a candidate key.
  - Example: If a table has a functional dependency where a non-candidate key determines another attribute, BCNF is violated. The table needs to be decomposed to satisfy BCNF.

### [2.3.2 Fourth Normal Form (4NF)](#table-of-contents)
**Objective**: Ensure no multi-valued dependencies.
> Criteria:
  - Meet all requirements of BCNF.
  - A table should not have more than one independent multi-valued dependency.
  - Example: If a table has two or more multi-valued attributes, such as a list of phone numbers and email addresses, 4NF requires splitting this table so that each attribute is stored in a separate table.

### [2.3.3 Fifth Normal Form (5NF)](#table-of-contents)
**Objective**: Decompose tables into smaller tables without losing information or introducing redundancy.
> Criteria:
  - Meet all requirements of 4NF.
  - Ensure that data can be reconstructed from the smaller tables without any loss of information.
  - Example: 5NF is applied in complex databases where tables are decomposed into even smaller tables while preserving the ability to reconstruct the original data without redundancy.

## [2.4 Benefits of Normalization](#table-of-contents)

Normalization offers several benefits:

- **Reduces Data Redundancy**: By ensuring data is stored only once, normalization saves storage space and prevents anomalies that can arise from duplicate data.
- **Improves Data Integrity and Consistency**: With data organized efficiently, it becomes easier to enforce integrity constraints, ensuring data remains accurate and consistent across the database.
- **Eases Database Maintenance**: Normalized databases are easier to maintain, as updates, inserts, and deletions are simpler to manage without causing unintended side effects.
- **Optimizes Query Performance**: Though sometimes normalization can lead to complex queries, it often results in a more optimized and faster database, as the data is logically structured.

## [2.5 Trade-Offs](#table-of-contents)

While normalization improves the structure and efficiency of databases, it also has some trade-offs:

- **Complexity**: Over-normalization can make the database structure complex and harder to understand.
- **Performance**: Highly normalized databases may require more complex joins, potentially impacting query performance. In some cases, denormalization is used to strike a balance between normalization and performance.

Normalization is a crucial aspect of database design, ensuring that the database is both efficient and easy to maintain. However, it is important to consider the specific needs of the application and strike a balance between normalization and performance.


# [3. ACID Properties in DBMS:](#table-of-contents)

A [****transaction****](https://www.geeksforgeeks.org/sql-transactions) is a single logical unit of work that accesses and possibly modifies the contents of a database. Transactions access data using read and write operations.  
In order to maintain consistency in a database, before and after the transaction, certain properties are followed. These are called ****ACID**** properties.

[acid](#link)

## [3.1 Atomicity:](#table-of-contents)

By this, we mean that either the entire transaction takes place at once or doesn’t happen at all. There is no midway i.e. transactions do not occur partially. Each transaction is considered as one unit and either runs to completion or is not executed at all. It involves the following two operations.  
— ****Abort**** : If a transaction aborts, changes made to the database are not visible.  
— ****Commit**** : If a transaction commits, changes made are visible.  
Atomicity is also known as the ‘All or nothing rule’.

Consider the following transaction ****T**** consisting of ****T1**** and ****T2**** : Transfer of 100 from account ****X**** to account ****Y**** .
[atomicity-1](#link)


If the transaction fails after completion of ****T1**** but before completion of ****T2**** .( say, after ****write(X)**** but before ****write(Y)**** ), then the amount has been deducted from ****X**** but not added to ****Y**** . This results in an inconsistent database state. Therefore, the transaction must be executed in its entirety in order to ensure the correctness of the database state.

## [3.2 Consistency:](#table-of-contents)

This means that integrity constraints must be maintained so that the database is consistent before and after the transaction. It refers to the correctness of a database. Referring to the example above,  
The total amount before and after the transaction must be maintained.  
Total ****before T**** occurs = ****500 + 200 = 700**** .  
Total ****after T occurs**** \= ****400 + 300 = 700**** .  
Therefore, the database is ****consistent**** . Inconsistency occurs in case ****T1**** completes but ****T2**** fails. As a result, T is incomplete.

## [3.3 Isolation:](#table-of-contents)

This property ensures that multiple transactions can occur concurrently without leading to the inconsistency of the database state. Transactions occur independently without interference. Changes occurring in a particular transaction will not be visible to any other transaction until that particular change in that transaction is written to memory or has been committed. This property ensures that the execution of transactions concurrently will result in a state that is equivalent to a state achieved these were executed serially in some order.  
Let ****X**** \= 500, ****Y**** \= 500.  
Consider two transactions ****T**** and ****T”.****

[atomiticity-2](#link)


Suppose ****T**** has been executed till ****Read (Y)**** and then ****T’’**** starts. As a result, interleaving of operations takes place due to which ****T’’**** reads the correct value of ****X**** but the incorrect value of ****Y**** and sum computed by  
****T’’: (X+Y = 50, 000+500=50, 500)****  
is thus not consistent with the sum at end of the transaction:  
****T: (X+Y = 50, 000 + 450 = 50, 450)**** .  
This results in database inconsistency, due to a loss of 50 units. Hence, transactions must take place in isolation and changes should be visible only after they have been made to the main memory.

## [3.4 Durability:](#table-of-contents)

This property ensures that once the transaction has completed execution, the updates and modifications to the database are stored in and written to disk and they persist even if a system failure occurs. These updates now become permanent and are stored in non-volatile memory. The effects of the transaction, thus, are never lost.

****Some important points:****

| ****Property**** | ****Responsibility for maintaining properties**** |
| --- | --- |
| Atomicity | Transaction Manager |
| Consistency | Application programmer |
| Isolation | Concurrency Control Manager |
| Durability | Recovery Manager |

The ****ACID**** properties, in totality, provide a mechanism to ensure the correctness and consistency of a database in a way such that each transaction is a group of operations that acts as a single unit, produces consistent results, acts in isolation from other operations, and updates that it makes are durably stored.

ACID properties are the four key characteristics that define the reliability and consistency of a transaction in a Database Management System (DBMS). The acronym ACID stands for Atomicity, Consistency, Isolation, and Durability. Here is a brief description of each of these properties:

1. Atomicity: Atomicity ensures that a transaction is treated as a single, indivisible unit of work. Either all the operations within the transaction are completed successfully, or none of them are. If any part of the transaction fails, the entire transaction is rolled back to its original state, ensuring data consistency and integrity.
2. Consistency: Consistency ensures that a transaction takes the database from one consistent state to another consistent state. The database is in a consistent state both before and after the transaction is executed. Constraints, such as unique keys and foreign keys, must be maintained to ensure data consistency.
3. Isolation: Isolation ensures that multiple transactions can execute concurrently without interfering with each other. Each transaction must be isolated from other transactions until it is completed. This isolation prevents dirty reads, non-repeatable reads, and phantom reads.
4. Durability: Durability ensures that once a transaction is committed, its changes are permanent and will survive any subsequent system failures. The transaction’s changes are saved to the database permanently, and even if the system crashes, the changes remain intact and can be recovered.

Overall, ACID properties provide a framework for ensuring data consistency, integrity, and reliability in DBMS. They ensure that transactions are executed in a reliable and consistent manner, even in the presence of system failures, network issues, or other problems. These properties make DBMS a reliable and efficient tool for managing data in modern organizations.

## [3.5 Advantages of ACID Properties in DBMS:](#table-of-contents)

1. Data Consistency: ACID properties ensure that the data remains consistent and accurate after any transaction execution.
2. Data Integrity: ACID properties maintain the integrity of the data by ensuring that any changes to the database are permanent and cannot be lost.
3. Concurrency Control: ACID properties help to manage multiple transactions occurring concurrently by preventing interference between them.
4. Recovery: ACID properties ensure that in case of any failure or crash, the system can recover the data up to the point of failure or crash.

## [3.6 Disadvantages of ACID Properties in DBMS:](#table-of-contents)

1. Performance: The ACID properties can cause a performance overhead in the system, as they require additional processing to ensure data consistency and integrity.
2. Scalability: The ACID properties may cause scalability issues in large distributed systems where multiple transactions occur concurrently.
3. Complexity: Implementing the ACID properties can increase the complexity of the system and require significant expertise and resources.  
    Overall, the advantages of ACID properties in DBMS outweigh the disadvantages. They provide a reliable and consistent approach to data
4. management, ensuring data integrity, accuracy, and reliability. However, in some cases, the overhead of implementing ACID properties can cause performance and scalability issues. Therefore, it’s important to balance the benefits of ACID properties against the specific needs and requirements of the system.