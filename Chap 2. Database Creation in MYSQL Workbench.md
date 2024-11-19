# Database Creation in MYSQL Workbench
### 1. Introduction to DDL and DML Statement
### 2. DDL Statement: A Demonstration
### 3. DmL Statement: A Demonstration
### 4. Modifying Columns


## 1. Introduction to DDL and DML Statement

The commands available in SQL can be broadly categorised as follows:

- Data Definition Language (DDL): used to define, modify, and manage database structures such as tables, schemas, and indexes. DDL commands are primarily concerned with the structure of the database rather than the actual data stored in it.
  1. Create
  2. Alter
  3. Drop
  4. TRUNCATE
  
- Data Manipulation Language (DML):used to manipulate and manage the data within database tables. DML commands are focused on the actual data stored in the database rather than the structure or schema of the database itself.
  1. Insert
  2. Update
  3. Delete

- Transaction Control Language(TCL): used to manage transactions within a database. TCL commands are used to ensure that database operations are processed in a reliable, consistent, and controlled manner
  1. Commit
  2. Savepoint
  3. Rollback
  
- Data Control Language (DCL):used to control access and permissions to the data in a database. DCL commands are primarily concerned with granting or revoking user privileges for performing operations on database objects.
  1. Grant
  2. Revoke

DDL, as the name suggests, is used to create a new schema as well as modify an existing schema. The typical commands available in DDL include CREATE, ALTER and DROP. Now, as a data analyst, the majority of your work will focus on insight generation, and you will be working with DML commands, specifically, the SELECT command. In the next segment, Professor Ramanathan will discuss this in detail.

## DDL Statements: A Demonstration

### Create:

- To create a database in SQL, you use the CREATE DATABASE command. :

Syntax:

```sql
CREATE DATABASE database_name;
```

- To start using the database
Syntax:
```sql
use <database_name>
```

- Creating Table: To create a table in SQL, we use the CREATE TABLE command

Syntax:
```sql
CREATE TABLE table_name (
    column1 datatype [constraint],
    column2 datatype [constraint],
    ...
);
```

# Char vs Varchar

| Feature        | CHAR                                                                      | VARCHAR                                                                                                      |
|----------------|---------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Length         | Fixed length (pad with spaces if shorter)                                 | Variable length (stores only actual characters)                                                              |
| Storage        | Uses fixed space for the defined length, even if the data is shorter      | Uses space based on the actual data length plus some overhead                                                |
| Performance    | Slightly faster for fixed-length data as the length is fixed              | More flexible but can be slower for very small strings or large datasets due to the need to store the length |
| Use Case       | Ideal for data with consistent length (e.g., codes, flags, abbreviations) | Ideal for data with varying lengths (e.g., names, addresses, descriptions)                                   |
| Maximum Length | Set at column definition (e.g., CHAR(10))                                 | Set at column definition, but can store up to the defined limit (e.g., VARCHAR(10))                          |
| Padding        | Pads shorter values with spaces to fit the fixed length                   | No padding, stores only the actual length of data                                                            |









