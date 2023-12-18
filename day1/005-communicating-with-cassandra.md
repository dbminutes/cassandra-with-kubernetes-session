### Communicating with Cassandra

- **Apache Cassandra** is a distributed NoSQL database designed to handle large amounts of data across many commodity servers.
- To communicate with Cassandra, you typically use CQL (Cassandra Query Language), a query language similar to SQL.

### Using CQLSH

- **CQLSH** is a command-line shell for interacting with Cassandra through CQL.
- To start CQLSH, open your terminal and type `cqlsh` followed by Enter. This assumes Cassandra is running on your local machine with default settings.

### Creating a Database

- In Cassandra, databases are often referred to as "keyspaces".
- To create a keyspace, use the command: 
  ```sql
  CREATE KEYSPACE mykeyspace WITH replication = {'class': 'SimpleStrategy', 'replication_factor': 3};
  ```

### Defining a Keyspace

- A keyspace in Cassandra is a namespace that defines data replication on nodes.
- The replication factor defines how many copies of the data exist.

### Deleting a Keyspace

- To delete a keyspace:
  ```sql
  DROP KEYSPACE mykeyspace;
  ```

### Creating a Table

- To create a table within a keyspace:
  ```sql
  CREATE TABLE mykeyspace.mytable (id int PRIMARY KEY, name text, age int);
  ```

### Defining Columns and Datatypes

- Cassandra tables contain columns, each with a specific datatype like int, text, blob, etc.
- Example:
  ```sql
  CREATE TABLE mykeyspace.employee (id int, name text, salary varint, PRIMARY KEY (id));
  ```

### Defining Primary Key

- The primary key uniquely identifies a record in a table.
- It can be simple (a single column) or composite (multiple columns).

### Recognizing a Partition Key

- The first part of the primary key is the partition key, which determines the distribution of data across the system.

### Specifying a Descending Cluster Order

- To order data in descending order within a partition, use the `CLUSTERING ORDER BY` clause:
  ```sql
  CREATE TABLE mykeyspace.sales (year int, month int, revenue int, PRIMARY KEY (year, month)) WITH CLUSTERING ORDER BY (month DESC);
  ```

### Understanding Ways to Write Data

- Data can be written into Cassandra using CQL commands like INSERT, UPDATE, or using bulk load tools.

### Using INSERT INTO Command

- To insert data:
  ```sql
  INSERT INTO mykeyspace.employee (id, name, salary) VALUES (123, 'John', 70000);
  ```

### Using COPY Command

- The COPY command is used for bulk loading data from a CSV file.
- Example:
  ```sql
  COPY mykeyspace.employee (id, name, salary) FROM 'employees.csv';
  ```

### Understanding How Data is Stored in Cassandra

- Data in Cassandra is distributed across nodes in the cluster.
- Each row is uniquely identified by a primary key, and the partition key part of the primary key determines which node stores the data.

### Understanding How Data is Stored on Disk

- Cassandra stores data on disk in SSTables (Sorted String Tables).
- Data is written to a commit log for durability and then to a memtable. Once the memtable is full, it is flushed to disk as an SSTable.
