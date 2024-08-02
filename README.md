# PostGresSQL_101
Learn PGSQL basic concepts , uses and examples.

# Index

- [What is Postgres](#whatispostgres)
- [Change Database to Dark Theme](#darktheme)
- [Create a Database](#createDB)
- [Design a Database](#designdb)
- [Make a Table](#createtable)
- [Data Types](#datatypes)
- [Adding Data to Table](#datatotable)
- [To See Data](#seedata)
- [Create Custom Type](#customtype)
- Change Column Data Type
- Thinking About Tables
- Breaking Up Tables
-  Primary & Foreign Keys
- Foreign & Primary Keys
- Altering Tables Many Examples
- Getting Data from One Table
- Where
- Conditional Operators
- Logical Operators
- Order By
- Limit
- GROUP BY
- Distinct
- Getting Data from Multiple Tables
- Inner Join
- Join 3 Tables
-  Arithmetic Operators
- Join with Where
- Outer Joins
- Cross Joins
- Unions
- Extract
- IS NULL
- SIMILAR LIKE & ~ 
- GROUP BY
-  HAVING
- AGGREGATE FUNCTIONS
- WORKING WITH VIEWS
- SQL Functions
- Dollar Quotes
- Functions that Return Void
- Get Maximum Product Price
- Get Total Value of Inventory
- Get Number of Customers
- Named Parameters
- Return a Row / Composite
- Get Multiple Rows
- PL/pgSQL
2:11:35 Variables in Functions
2:15:55 Store Rows in Variables
2:19:17 IN INOUT and OUT
2:21:01 Using Multiple Outs
2:25:56 Return Query Results
2:33:42 IF ELSEIF and ELSE
2:38:48  CASE Statement
2:42:01 Loop Statement
2:45:20 FOR LOOP
2:48:34 Result Sets, Blocks & Raise Notice
2:51:11 For Each and Arrays
2:53:20 While Loop
2:54:54 Continue
3:01:34 Stored Procedures
3:09:35 Triggers
3:29:25 Cursors
3:39:45 Installation

<a id="whatispostgres"></a>

# What is Postgres ?

Is a powerful, open-source relational database management system (RDBMS) that emphasizes extensibility and SQL compliance.

To start using `PostgreSQL`, you can install it on your local machine, set up a PostgreSQL server, and use client tools like `psql` (command-line interface) or graphical interfaces like `pgAdmin`. The official PostgreSQL documentation provides detailed installation guides and tutorials to help you get up and running.

### Key Features of PostgreSQL

1. **Open Source**: PostgreSQL is released under the PostgreSQL License, a permissive free software license. This means it is free to use, modify, and distribute.

2. **SQL Compliance**: PostgreSQL supports a substantial portion of the SQL standard and offers many modern features such as foreign keys, triggers, views, and stored procedures.

3. **Extensibility**: One of the standout features of PostgreSQL is its extensibility. You can define your own data types, operators, index types, and even functional languages to use in your queries.

4. **Advanced Data Types**: In addition to standard SQL data types, PostgreSQL supports advanced data types like arrays, hstore (key-value store), JSON/JSONB, XML, and geometric types.

5. **ACID Compliance**: PostgreSQL is fully ACID (Atomicity, Consistency, Isolation, Durability) compliant, ensuring reliable transactions and data integrity.

6. **Concurrency Control**: PostgreSQL uses Multi-Version Concurrency Control (MVCC) to handle concurrent transactions efficiently without requiring read locks.

7. **Full-Text Search**: Built-in support for full-text search, enabling efficient searching within text fields.

8. **Replication and Backup**: PostgreSQL supports various forms of replication (streaming replication, logical replication) and offers tools for robust backup and recovery (pg_dump, pg_basebackup).

9. **Indexing**: It offers a wide range of indexing techniques, including B-tree, hash, GiST, GIN, and BRIN indexes, which can significantly improve query performance.

10. **Community and Ecosystem**: PostgreSQL has a vibrant community and a rich ecosystem of tools, extensions, and third-party applications. Popular extensions include PostGIS for geographic data, pg_stat_statements for tracking query performance, and many more.

### Why Choose PostgreSQL?

- **Reliability and Stability**: PostgreSQL is known for its robustness and stability, making it a trusted choice for critical applications.
- **Performance**: With its advanced features and optimization capabilities, PostgreSQL can handle large-scale, high-transaction databases efficiently.
- **Flexibility**: Whether you need to handle simple relational data or complex, unstructured data, PostgreSQL's flexible data model can accommodate various needs.
- **Community Support**: The active and supportive PostgreSQL community provides extensive documentation, forums, and third-party resources to help you troubleshoot issues and learn new features.

### Use Cases for PostgreSQL

- **Web Applications**: Many web applications use PostgreSQL as their backend database due to its reliability and performance.
- **Data Warehousing**: PostgreSQL's powerful querying and indexing capabilities make it suitable for data warehousing and business intelligence applications.
- **Geospatial Data**: With the PostGIS extension, PostgreSQL becomes a powerful database for handling geographic information system (GIS) data.
- **Financial Systems**: Its ACID compliance and support for complex transactions make PostgreSQL a popular choice for financial applications.

<a id="darktheme"></a>

# Change Database to Dark theme

In `pgAdmin`:

- File -> Preferences -> Miscellaneous -> Themes -> Theme -> Dark

<a id="createDB"></a>

# Create a Database

- Servers -> PostgreSQL -> Databases (right click) -> Create -> Database

- <img width="1626" alt="image" src="https://github.com/user-attachments/assets/78e85642-8b37-45c8-b9e5-866076188ace">

When you start creating a DB, you need to: 

- Make sure 1 table only represent 1 real world object, for example: 
  - customers
  - orders
  - sales

- Columns are going to store only 1 piece of information, like:
  - name
  - address
  - state
 
- How do different tables relate?
  - If we have a sales order we are going to need to relate our customer table to the sales table.
 
<a id="createtable"></a>

# Create a Table

Go into the `Query`tool and 

```
CREATE TABLE customer(
first_name VARCHAR(30) NOT NULL,
last_name VARCHAR(30) NOT NULL,
email VARCHAR(60) NOT NULL,
company VARCHAR(60) NOT NULL,
street VARCHAR(50) NOT NULL,
city VARCHAR(40) NOT NULL,
state CHAR(2) NOT NULL,
zipcode SMALLINT NOT NULL,
phone VARCHAR(20) NOT NULL,
birth_data DATE NULL,
sex CHAR(1) NOT NULL,
date_entered TIMESTAMP NOT NULL,
id SERIAL PRIMARY KEY
)

```

<img width="1687" alt="image" src="https://github.com/user-attachments/assets/85c09c51-f92f-4427-8bc2-cb0cfd550dbd">


It should appear under your dbname-> Schemas -> Tables -> tableName (customer)


<a id="datatypes"></a>
# Data Types

### Numeric Types
- **SMALLINT**: Small-range integer
- **INTEGER**: Standard integer
- **BIGINT**: Large-range integer
- **DECIMAL**: Exact numeric with user-defined precision
- **NUMERIC**: Exact numeric with user-defined precision
- **REAL**: Single precision floating-point number
- **DOUBLE PRECISION**: Double precision floating-point number
- **SERIAL**: Auto-incrementing integer
- **BIGSERIAL**: Auto-incrementing large integer

### Character Types
- **CHAR(N)**: Fixed-length character string
- **VARCHAR(N)**: Variable-length character string
- **TEXT**: Variable-length character string with no length limit

### Binary Data Types
- **BYTEA**: Binary data ("byte array")

### Date/Time Types
- **DATE**: Calendar date (year, month, day)
- **TIME**: Time of day (without time zone)
- **TIME WITH TIME ZONE**: Time of day (with time zone)
- **TIMESTAMP**: Date and time (without time zone)
- **TIMESTAMP WITH TIME ZONE**: Date and time (with time zone)
- **INTERVAL**: Time span

### Boolean Type
- **BOOLEAN**: Boolean value (true/false)

### Enumerated Type
- **ENUM**: Enumeration of predefined values

### Geometric Types
- **POINT**: Geometric point
- **LINE**: Infinite line
- **LSEG**: Line segment
- **BOX**: Rectangular box
- **PATH**: Geometric path (open or closed)
- **POLYGON**: Closed geometric path
- **CIRCLE**: Circle

### Network Address Types
- **CIDR**: IPv4 or IPv6 network
- **INET**: IPv4 or IPv6 host address
- **MACADDR**: MAC address

### Bit String Types
- **BIT(N)**: Fixed-length bit string
- **VARBIT(N)**: Variable-length bit string

### Text Search Types
- **TSVECTOR**: Text search vector
- **TSQUERY**: Text search query

### UUID Type
- **UUID**: Universally unique identifier

### JSON Types
- **JSON**: Textual JSON data
- **JSONB**: Binary JSON data, optimized for storage and querying

### Arrays
- **ARRAY**: Array of any data type

### Composite Types
- **Composite Types**: Custom user-defined composite types

### Range Types
- **INT4RANGE**: Range of integers
- **INT8RANGE**: Range of big integers
- **NUMRANGE**: Range of numerics
- **TSRANGE**: Range of timestamps without time zone
- **TSTZRANGE**: Range of timestamps with time zone
- **DATERANGE**: Range of dates


<a id="datatotable"></a>

# Adding data to Table

<img width="1673" alt="image" src="https://github.com/user-attachments/assets/075d886b-e1e7-4380-8fda-0108b14824b2">

<a id="seedata"></a>

# To see data

![image](https://github.com/user-attachments/assets/f515a723-84c0-43f1-8ece-7f146432a25c)

<a id="customtype"></a>

# Create Custom Type

<img width="1704" alt="image" src="https://github.com/user-attachments/assets/37c94174-e939-4df5-bcfe-57465502c318">
