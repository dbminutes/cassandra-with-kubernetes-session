Enabling logging in Cassandra involves configuring the logging settings in its configuration files. The primary configuration files for logging are `logback.xml` and `cassandra.yaml`. 


### 1. Locate Configuration Files
- The `logback.xml` and `cassandra.yaml` files are usually located in the `conf` directory of your Cassandra installation.
  
### 2. Configure `logback.xml` for General Logging
- `logback.xml` is used for configuring the general logging settings.

**Example:**
To change the log level to DEBUG for more detailed logs, find and modify the `<logger>` tag:
```xml
<logger name="org.apache.cassandra" level="DEBUG"/>
```

### 3. Enable Query Logging
- For logging CQL queries, you need to modify the `cassandra.yaml` file.

**Example:**
To enable query logging, add or update the following lines in `cassandra.yaml`:
```yaml
# Full query logging options
full_query_logging_options:
    log_dir: /path/to/log/dir
    roll_cycle: HOURLY
    block: true
    max_queue_weight: 268435456 # 256 MiB
    max_log_size: 17179869184 # 16 GiB
```
- Set the `log_dir` to a directory where you want the logs to be stored.
- Adjust other parameters as per your requirements.

### 4. Enable Audit Logging (Optional)
- Cassandra also supports audit logging, which can be configured in the `cassandra.yaml` file.

**Example:**
```yaml
audit_logging_options:
    enabled: true
    logger: SLF4JAuditWriter 
    included_categories: QUERY, DML, DDL
    excluded_keyspaces: "system, system_schema, system_virtual_schema"
    included_keyspaces: ""
    excluded_categories: ""
    excluded_users: ""
```
- Here, `included_categories` specifies the type of operations to log.
- Adjust `excluded_keyspaces`, `included_keyspaces`, and other parameters according to your needs.

### 5. Restart Cassandra
- After making changes to the configuration files, restart your Cassandra node for the changes to take effect.

### 6. Monitor the Logs
- Check the specified log directory for logs.
- If you enabled full query logging, you'd find logs in the specified `log_dir`.
- General logs will be found in the directory configured for logback (usually `logs` directory in the Cassandra installation).

### Notes
- Always backup configuration files before making changes.
- Be aware of the performance implications of extensive logging, especially in a production environment.
- Secure your logs, especially if they contain sensitive information.
