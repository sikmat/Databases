# Databases
## Module 1: SQL
SQL stands as a widely used tool for accessing information from relational databases like SQL Server, MySQL, MariaDB, and PostgreSQL

- **Statements** to query the database(ask, modify, create, tweak tables)
- **DML(Data Manipulation Language)** - Used to tweak existing tables, performing CRUD operations.
- **DDL(Data Definition Language)** - Used when restructuring tables or altering the database

#### Statements

SELECT - extracts data from a database
UPDATE - updates data in a database
DELETE - deletes data from a database
INSERT INTO - inserts new data into a database
CREATE DATABASE - creates a new database
ALTER DATABASE - modifies a database
CREATE TABLE - creates a new table
ALTER TABLE - modifies a table
DROP TABLE - deletes a table
CREATE INDEX - creates an index (search key)
DROP INDEX - deletes an index
WHERE - filters by the condition provided
AND OR - Logical Operators(One or Two conditions met)
LIKE - to find a part of a field that matches
% in LIKE statement - zero or more characters that match
ORDER BY - sorting by a field, with ASC or DESC(ASC is the default)
DISTINCT - unique values
COUNT - get total rows/records in a table

- Link for more commands
https://www.dataquest.io/blog/sql-commands/

### Data Types
- BINARY - BINARY, BINARY LARGE OBJECT(BLOB), BINARY VARYING
- DATE/TIME - DATE, INTERVAL, TIME, TIMESTAMP
- NUMBERS - BIGINT, DECIMAL, DOUBLE PRECISION, FLOAT, INTEGER, NUMERIC, SMALLINT, REAL
- TEXT - CHARACTER, CHARACTER LARGE OBJECT, VARCHAR, NCHAR, NCHAR VARYING
- OTHER -  BOOLEAN
**null** - does not mean zero or no, just nothing in a particular field

-  Compound SELECT - Sub-queries or sub-selects

### Math Operators
Can be used to filter data

### Transforming SQL Data
- LOWER/UPPER - to change case
- SUBSTR - gets a chunk of the string (start at position(n), exract (n) characters)
- REPLACE - to replace/swap bits of string('this', (with) 'this')
-  CAST - interpret one data type as another, useful when you cannot tweat database schema

**Aliases** - used to give other names to field names using AS keyword

**CRUD**
- CREATE = INSERT
- READ/RETRIEVE = SELECT
- UPDATE
- DELETE

## Module 2: MongoDB
MongoDB is a NoSQL database (the most popular one) which means that it doesn’t use SQL to handle data. Mongo also doesn’t use tables. Instead, it uses a structure known as collections to store the data in the form of a document—the same way you would write information on a sheet of paper but with the same structure as a JSON object. MongoDB's flexible document store is a key feature, where data is stored in documents rather than tables.

### Documents and Collections

**Binary JSON** - MongoDB documents are field-value pairs stored in BSON, a JSON-like format

**Commands**
- find (SELECT version). It requires a query document as its first parameter; an empty query document retrieves all documents by default.

**Collections**
Collections, analogous to tables in relational databases, offer a solution by allowing related documents to be grouped for enhanced organization and performance. Unlike relational databases, MongoDB collections can contain documents with varying schemas. These collections reside within databases.

### Querying
#### Sorting and Querying Data in MongoDB

- **Cursors**: MongoDB queries return Cursors, which allow for efficient management of the data returned and enable chaining of additional query operations.
  
- **Find Command**: When executing a `find()` query, the results are not returned immediately. Instead, the query waits until data is requested, supporting chaining of commands for complex queries.

- **Limiting Results**:
  - Use the `limit()` function to control the number of documents returned.
  - Example: `db.recipes.find().limit(2)` limits the results to two recipes.

- **Sorting Results**:
  - Use the `sort()` function to arrange documents by a specified field in ascending (`1`) or descending (`-1`) order.
  - Example: `db.recipes.find().sort({title: 1})` sorts recipes alphabetically by title.

- **Skipping Documents**:
  - The `skip()` function allows skipping a specified number of documents in the result set.
  - Example: `db.recipes.find().skip(1).limit(1)` skips the first document and returns the second one.

- **Chaining Queries**:
  - Combine `skip()`, `limit()`, and `sort()` to create dynamic queries.
  - Example: `db.recipes.find().skip(2).limit(1).sort({title: 1})` skips the first two documents, returns one document, and sorts by title.

- **Advanced Queries**:
  - Additional operators allow for querying data within arrays and further refining results, providing flexibility for complex query operations.

#### Filtering Data in MongoDB Using Operators

- **MongoDB Operators**: MongoDB provides operators to filter fields like strings, numbers, arrays, objects, or subdocuments. These operators use a dollar sign (`$`) prefix.

- **Comparison Operators**:
  - `$gt` for greater than, `$lt` for less than.
  - Example: To find recipes with a cook time of 30 minutes or less:  
    `{ cook_time: { $lte: 30 } }`.

- **Combining Conditions**:
  - Use commas to combine conditions (AND query).
  - Example: To filter by both cook time and prep time, combine conditions in the query.

- **Array Filtering**:
  - To find recipes tagged as "easy":  
    `{ tags: "easy" }`.
  - For multiple tags like "easy" and "Mexican," use `$all`:  
    `{ tags: { $all: ["easy", "Mexican"] } }`.
  - Use `$in` for "OR" conditions.

- **Object Fields & Dot Notation**:
  - Use dot notation to navigate object fields. Example: To find recipes with "egg" as an ingredient:  
    `{ "ingredients.name": "egg" }`.

#### Updating Documents in MongoDB

- **Single-Field Updates**:
  - Use `updateOne()` with operators like `$set`, `$unset`, and `$inc` to modify individual fields in a document.
  - Example: Change a recipe title using `$set`:  
    `{ $set: { title: "Thin Crust Pizza" } }`.

- **Upsert Functionality**:
  - If a field doesn't exist, you can add it using the `upsert` option.
  - Example: Add a new field (`vegan`) to a document:  
    `{ $set: { vegan: false } }`.

- **Removing Fields**:
  - Use `$unset` to remove fields from a document.
  - Example: Remove the `vegan` field:  
    `{ $unset: { vegan: "" } }`.

- **Incrementing Fields**:
  - Use `$inc` to increment numeric fields, useful in scenarios like counting likes.
  - Example: Increment the `likes_count` field:  
    `{ $inc: { likes_count: 1 } }`.

- **Atomic Operations**:
  - MongoDB ensures eventual consistency and prevents data inconsistencies, especially in concurrent updates.

- **Array Updates**:
  - The tutorial also touches on updating and manipulating arrays, which will be explored further.

#### Updating Arrays in MongoDB

- **Adding to Arrays**:
  - Use `$push` to append an item to an array.
  - Example: Add a user ID (`60`) to the `likes` array in a recipe:  
    `db.examples.updateOne({ title: "Tacos" }, { $push: { likes: 60 } })`.

- **Removing from Arrays**:
  - Use `$pull` to remove an item from an array.
  - Example: Remove user ID (`60`) from the `likes` array:  
    `db.examples.updateOne({ title: "Tacos" }, { $pull: { likes: 60 } })`.

- **Array Elements**:
  - Elements added or removed can be of any valid type (integer, string, object, or another array).

- **Further Exploration**:
  - Additional array operators can be explored for more advanced array manipulations.

#### Deleting Documents in MongoDB

- **Deletion Methods**:
  - **`deleteOne()`**: Deletes the first document matching the specified filter.
  - **`deleteMany()`**: Deletes all documents matching the filter.

- **Filter Usage**:
  - Filters are similar to those used in `find()` and `update()` commands.
  - Example: Delete a document using its `_id`:  
    `db.collection.deleteOne({ _id: ObjectId("your_object_id_here") })`.
  - Example: Delete a document with zero likes:  
    `db.collection.deleteOne({ likes: 0 })`.

- **Safety Considerations**:
  - When expecting to delete only one document, it’s safer to use `deleteOne()` to avoid unintended mass deletions.

#### MongoDB Shell (Mongo SH)

- **Mongo SH Introduction**:
  - MongoDB introduced Mongo SH, set to replace the old Mongo shell.
  - Downloadable from the MongoDB website or via Brew for Mac.

- **Features**:
  - **Help Command**: Append "help" to a command for detailed information and examples.
  - **Syntax Highlighting**: Queries and output are color-coded for better readability.
  - **Node.js Integration**: Supports JavaScript execution and more, allowing users to assign query results to variables and format output with functions like `console.table`.

- **Auto-Complete**:
  - Auto-complete assists in constructing queries, offering suggestions when pressing "tab".

- **Embedded Editor**:
  - Mongo SH includes an embedded editor for scripting, with optional snippets and extensions.

### Data and Schema Modeling

#### MongoDB Schema Design

- **Data Modeling Approach**:
  - In MongoDB, data accessed together should be stored together to reduce the need for multiple queries.
  - **Embedding Data**: Frequently used related data can be embedded, such as storing an array of user IDs who liked a recipe directly within the recipe document.
  
- **Embedding vs. Referencing**:
  - **Embedding**: Efficient when data is closely related and often accessed together (e.g., a user's address within the user document).
  - **Referencing**: Suitable for data rarely accessed together (e.g., storing music details separately to optimize RAM usage).

- **Example**:
  - Embedding likes in a recipe document saves query time when displaying the recipe.
  - Storing saved recipes as an array inside a user document makes sense due to the close association with the user.

- **Handling Complex Data**:
  - Arrays of objects (e.g., ingredients) should be kept within reasonable limits to avoid overloading RAM when loading documents.
  
- **One-to-Many Relationships**:
  - For relationships like a recipe and its comments, store top comments in the recipe document and the rest in a separate collection to improve page load times.

- **Indexing**:
  - Once the schema is designed, indexing is crucial for optimizing query performance.

#### Indexes in MongoDB

- **Purpose of Indexes**:
  - Indexes speed up query performance by allowing the database to quickly locate data, similar to a book's index.
  - Without indexes, MongoDB scans all documents, which is inefficient for large datasets.

- **Practical Example**:
  - Querying a recipe collection for a cook time of 10 minutes without an index requires scanning all documents.
  - With an index on the 'title' field, querying for "Tacos" reduces the number of documents scanned, significantly improving efficiency.

- **Managing Indexes**:
  - Use `getIndexes()` to inspect existing indexes.
  - Create an index with `createIndex()`, specifying the field (e.g., 'cook time') and direction (e.g., descending).
  - Drop an index using `dropIndex()`, specifying the index name.

- **Index Types**:
  - **Unique Indexes**: Prevent duplicate values in a field.
  - **Compound Indexes**: Created on multiple fields.
  - **Geospatial Indexes**: For spatial data.

- **Best Practices**:
  - Align index order with common query patterns.
  - Ensure proper indexing on frequently accessed fields for optimal performance.

#### MongoDB Collection Types

- **Capped Collections**:
  - Designed for scenarios like log data, where data order is crucial.
  - Automatically deletes older documents once a specified limit is reached (First-In-First-Out).
  - Created using `db.createCollection()` with `capped` set to true and defining a size or document limit.
  - Cannot be sharded and lack a default index, but can be useful for maintaining a fixed-size collection.

- **Time Series Collections**:
  - Introduced in MongoDB 5.0, optimized for data with fixed intervals (e.g., stock prices, sensor data).
  - Track parameters over time and store metadata for future queries.
  - Support automatic document deletion with a Time-to-Live (TTL) feature, similar to capped collections.
  - Ideal for applications like monitoring or sensor data, with built-in data optimization for queries.

### Development with MongoDB
#### MongoDB and Python
This section provides guidance on developing applications with MongoDB, focusing on using **Python** and **PyMongo** to interact with MongoDB databases. The same examples can be applied to other languages like JavaScript, PHP, or Go.

1. **PyMongo Installation**
- Install PyMongo using PIP: `pip install pymongo`.
- If running locally, ensure MongoDB is installed and running on `localhost` with the default port (`27017`).

2. **Connecting to MongoDB in Python**
- Import PyMongo in the Python shell.
- Set up the MongoDB client: `client = pymongo.MongoClient("localhost", 27017)`.
- Define a database: `db = client['cooker']`.
- Confirm the connection: `print(db.name)` should return `'cooker'`.

3. **Basic MongoDB Commands with Python**
- Retrieve a single document: `db.recipes.find_one()`.
- Retrieve multiple documents: `db.recipes.find()`.
- Use loops to process multiple documents, e.g., print the titles of all recipes.

4. **Advanced Commands**
- **Sorting**: Use `.sort()` to sort documents. For example, `db.recipes.find().sort("title", 1)` sorts by title in ascending order.
- **Limiting Results**: Use `.limit()` to restrict the number of documents returned, e.g., `db.recipes.find().limit(3)` returns three documents.

5. **Building a Simple Recipe Search**
- Import `pymongo` and `os`.
- Prompt the user for a recipe search term.
- Query the database and display the results (e.g., cook time, calories).

6. **Exploration and Experimentation**
- Modify the provided Python scripts to practice different MongoDB operations in your code space.
- Feel free to experiment in this learning environment to better understand how MongoDB integrates with Python.

#### MongoDB and Node.js

This section introduces developing applications with **MongoDB** using **Node.js**. MongoDB provides official drivers for various languages, and here we focus on Node.js integration.

1. **Setting Up MongoDB with Node.js**
- Use the official MongoDB Node.js driver, which can be installed via NPM: `npm install mongodb@4.10` (or the latest version).
- If installation issues occur, refer to the documentation or set an exact version.

2. **Connecting to MongoDB**
- In the provided code space, open the Node.js files and use the terminal to execute: `node one-test`.
- This script connects to the **Cooker** database and confirms a successful connection.

3. **Basic MongoDB Operations in Node.js**
- **Connecting to the database**: Create a Mongo client, set the connection string, and select the database.
- **Retrieving data**: Use `findOne()` to fetch a single document, and `find()` to list multiple documents from the "recipes" collection.

4. **Sorting and Limiting Results**
- Apply sorting with `.sort()` and limit the number of results with `.limit()`, as shown in example 4. For instance, sort recipes by title and return only the first three documents.

5. **Interactive Recipe Search**
- In file 5, the code prompts the user for a recipe search term.
- It then connects to the database, performs a case-insensitive search using a regular expression, and displays the results with cook time and calories per serving.

6. **Experimentation and Exploration**
- Review and modify the Node.js examples in the code space.
- If you're familiar with JavaScript, use this as a starting point to build custom MongoDB applications with Node.js.

### Server-side Administration with MongoDB
#### Server-side Administration with MongoDB

This section covers **server-side administration** of MongoDB, focusing on configuring MongoDB using **config files** for easier and more secure management of startup options.

1. **MongoDB Config Files**
- MongoDB configurations can be set via command-line options (e.g., `--dbpath`), but using **YAML configuration files** is more convenient and scalable.
- These config files allow for a wide range of settings, such as specifying the **data file location**, **log file management**, **network configurations**, and **security settings**.

2. **Example Config Files**
- The provided config files (`mongo-deep.conf` and `sample.conf`) demonstrate different setup options:
  - **Log file management**: Prevents log overflow by appending logs and specifying log file locations.
  - **Storage settings**: Configures the database path, eliminating the need for `--dbpath`.
  - **Network settings**: Controls bind IP, port, and other network-related options important for securing the database.

3. **Advanced Configuration Options**
- Advanced options in `sample.conf` include:
  - **Separating logs and databases** on different physical disks for better performance.
  - **Directory per database**: Organizes data files for each database in its directory.
  - **Process management**: Configures MongoDB to run in the background (forking), useful for production environments.
  - **Security settings**: Enables role-based authorization for enhanced security.
  - **Replication settings**: Configures the replica set name, which is essential for setting up replication.

4. **Using Config Files**
- To start MongoDB with a configuration file, use the `--config` option:
  ```bash
  mongod --config /path/to/config-file.conf
  ```
- On Windows, config files may use a three-letter extension like `.yaml`.

#### Replication

In production environments, using a standalone MongoDB instance is risky due to potential server crashes or downtime. To mitigate these risks, **replica sets** are recommended. A **replica set** consists of multiple database instances (nodes) that replicate data from a **primary node** to several **secondary nodes**. If the primary fails, one of the secondaries automatically takes over.

1. **Replica Set Setup**
- Replica sets involve a primary node and secondary nodes to ensure data redundancy and high availability.
- For demonstration, a replica set with three members is configured in Docker on a single host, each running on a different port. In production, the nodes should be distributed across different servers.

2. **Initiating and Configuring Replica Sets**
- Create directories for each replica member's data files and start MongoDB instances in separate terminals.
- Log into the primary node and configure the replica set using `rs.initiate()` with member details.
- Use `rs.status()` and `db.isMaster()` to check the replica set status and verify replication.

3. **Connecting to a Replica Set**
- When connecting to a replica set, use a connection string that specifies all members and the replica set name to ensure automatic connection to the primary node.

4. **Replication in MongoDB**
- Any changes made on the primary node automatically propagate to the secondary nodes, providing data redundancy and minimizing downtime.

#### Sharding

**Sharding** in MongoDB is a method for distributing data across multiple servers to improve performance and scalability. Instead of relying on increasingly larger servers as data grows, sharding enables **scaling out** by partitioning data across multiple servers.

1. **Sharding vs. Scaling Up**
- Traditional scaling involves using larger servers ("scale up"), while sharding allows distributing the data across many servers ("scale out"), providing flexibility and resource optimization.
- MongoDB automates sharding, reducing the complexity compared to manual partitioning in other databases.

2. **MongoDB Cluster and MongoS**
- A **MongoDB cluster** is the setup of servers in a sharded environment. Unlike replica sets that replicate data across all nodes, **sharding splits data** among servers.
- **MongoS** acts as a router, determining where data resides and fetching it from the correct shard based on a **shard key**.
- **Config servers** (preferably in a replica set) manage data locations, while other replica sets store the data itself.

3. **Shard Keys and Data Distribution**
- A **shard key** is a field that determines how data is partitioned across shards, and it must be indexed.
- MongoDB automatically adjusts the data distribution as it grows, balancing shards dynamically to prevent overload.

4. **Application Transparency**
- Sharding is transparent to the application, meaning the application connects to MongoS, and MongoDB handles routing and merging of data without requiring special handling or code changes.

#### Authentication and Authorization

Securing MongoDB requires implementing **authentication** and **authorization**. While network security measures like firewalls are helpful, it is crucial to enforce **role-based access control** to manage user privileges.

1. **Authentication**
- **Authentication** verifies a user's identity using usernames, passwords, or keys, similar to logging into an account.
- By default, MongoDB has no authentication enabled. You must set up user accounts to secure access.
- To set up, log into the MongoDB shell without access control, use the **admin database**, and create users with specified roles (e.g., read, write).
  
2. **Authorization**
- **Authorization** defines what authenticated users can do, assigning **roles** and **permissions**.
- MongoDB uses **role-based access control** (RBAC) to grant precise permissions, such as read-only access or administrative tasks.
- Roles can be customized further by restricting access to specific databases or operations (e.g., limiting the ability to create indexes).

3. **Enabling Access Control**
- After creating user accounts, restart the MongoDB server and edit the configuration file to enable **authorization**.
- Authentication can be performed during or after connection, specifying the admin database, username, and password.

#### Backups

Backing up your MongoDB databases is essential, and testing restore procedures is just as important. MongoDB offers two primary methods for backups: **file copying** and the **mongodump/mongorestore** utilities.

1. **Copying Data Files**
- This manual method involves copying the MongoDB data files directly.
- Before copying, use `DB.fsyncLock` to temporarily lock the database to prevent writes, copy the files, and then unlock with `DB.fsyncUnlock`. 
- Alternatively, you can stop MongoDB, copy the files, and restart the server. 
- If using a **replica set**, one member can be removed temporarily for backup to minimize downtime.
- To restore, stop MongoDB, replace the data files with the backup, and restart.

2. **mongodump/mongorestore**
- **mongodump** creates a backup in a dump folder with subfolders for each database and collection.
- You can back up specific databases, collections, or even partial documents using queries.
- **mongorestore** allows you to restore from the dump folder, either for entire databases or specific collections.

In both methods, regular backups and testing the restore process are crucial for maintaining database integrity and disaster recovery.