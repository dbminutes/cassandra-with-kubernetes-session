Time-to-Live (TTL) in Apache Cassandra is a feature that determines how long data should be stored in the database before it is automatically deleted. Here's an overview of how TTL can be used in Cassandra, along with examples of the different types of TTL options available:

### 1. Default TTL for a Table
You can set a default TTL for all data in a table. This means that any data inserted into the table will be automatically deleted after the specified time period.

**Example:**
```cql
CREATE TABLE users (
    user_id int PRIMARY KEY,
    name text,
    email text
) WITH default_time_to_live = 86400;  -- Sets a default TTL of 24 hours
```

### 2. TTL for Individual Columns
You can also set a TTL for specific columns in a row when inserting or updating data. This is useful if you want some data to persist longer than others.

**Example:**
```cql
INSERT INTO users (user_id, name, email) VALUES (123, 'John Doe', 'john@example.com') USING TTL 3600;  -- TTL of 1 hour for this row
```

### 3. Updating TTL
You can update the TTL of existing data. This will reset the TTL timer for the specified data.

**Example:**
```cql
UPDATE users USING TTL 7200 SET email = 'john@newexample.com' WHERE user_id = 123;  -- Update TTL to 2 hours for this row
```

### 4. Checking TTL
Cassandra allows you to check the remaining TTL of a specific column in a row. This can help in understanding when the data will expire.

**Example:**
```cql
SELECT TTL(email) FROM users WHERE user_id = 123;
```

### 5. Removing TTL
You can remove the TTL from a column, making it persistent indefinitely unless manually deleted.

**Example:**
```cql
UPDATE users USING TTL 0 SET email = 'john@permanentemail.com' WHERE user_id = 123; -- Removes TTL from the email column
```

### Important Notes:
- TTL values are specified in seconds.
- If a row or column has a TTL, it will be automatically removed from the database after the TTL expires.
- Default TTL for a table can be altered later using the `ALTER TABLE` command.
- TTL is not set by default; it needs to be explicitly specified.

Using TTL in Cassandra is particularly useful for managing data that needs to be automatically purged after a certain period, like session data, cache data, or temporary records.