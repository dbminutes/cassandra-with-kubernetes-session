`nodetool` is a command-line utility that comes with Apache Cassandra and is used for various administrative tasks related to cluster management. Here's a tutorial on some of the most commonly used `nodetool` commands, including examples:

### 1. **Adding a Node to the Cluster**

   - **Step 1:** Set up a new Cassandra node with the same configuration as the existing nodes in your cluster.
   - **Step 2:** Start the Cassandra service on the new node.
   - **Step 3:** The new node will automatically join the cluster if it's configured correctly.

   There is no specific `nodetool` command to add a node, as it joins the cluster automatically when you start the Cassandra service with the correct settings.

### 2. **Removing a Node from the Cluster**

   - **Command:** `nodetool decommission` (if the node is up) or `nodetool removenode` (if the node is down)
   - **Usage:**
     - To decommission a live node: 
       ```
       nodetool decommission
       ```
     - To remove a failed node:
       ```
       nodetool removenode <host ID>
       ```

### 3. **Checking Cluster Status**

   - **Command:** `nodetool status`
   - **Example:**
     ```
     nodetool status
     ```

   This command provides information about the nodes in your cluster, including their state (up/down), load, tokens, and more.

### 4. **Repairing a Node**

   - **Command:** `nodetool repair`
   - **Example:**
     ```
     nodetool repair
     ```

   Regular repairs are critical in Cassandra to ensure data consistency across the cluster.

### 5. **Flushing Data from Memory to Disk**

   - **Command:** `nodetool flush`
   - **Example:**
     ```
     nodetool flush
     ```

   This forces a flush of data from the memtables (in-memory data structures) to SSTables (on-disk files).

### 6. **Cleaning Up Nodes**

   - **Command:** `nodetool cleanup`
   - **Example:**
     ```
     nodetool cleanup
     ```

   Run this on a node after adding new nodes to the cluster. It removes data that no longer belongs to the node.

### 7. **Taking a Snapshot**

   - **Command:** `nodetool snapshot`
   - **Example:**
     ```
     nodetool snapshot
     ```

   This creates a snapshot (backup) of your data.

### 8. **Viewing Ring Information**

   - **Command:** `nodetool ring`
   - **Example:**
     ```
     nodetool ring
     ```

   Displays the token ring for the cluster.

### Best Practices:
- Regularly monitor and maintain your Cassandra cluster using these and other `nodetool` commands.
- Schedule regular repairs and backups.
- Monitor the status of your nodes frequently.

-------------------------

### Preparing a new node

### 1. **Install Cassandra**

   - Install the same version of Cassandra that is running on your existing cluster nodes.
  

### 2. **Configure Cassandra**

   After installation, you need to configure the new node. The main configuration file for Cassandra is `cassandra.yaml`, usually found in the `conf` directory of your Cassandra installation.

   - **Cluster Name:** Set the cluster name to "MyCluster" to match your existing cluster.
     ```yaml
     cluster_name: 'MyCluster'
     ```
   - **Listen Address:** Set the listen address to the IP address of the new node. This is the address the node uses to communicate with other nodes.
     ```yaml
     listen_address: <new_node_ip>
     ```
   - **Broadcast Address:** Often the same as the listen address unless you're doing advanced network configuration.
     ```yaml
     broadcast_address: <new_node_ip>
     ```
   - **RPC Address:** Set the RPC address, which is used for client connections. If your clients are all internal, this can be set to the internal IP.
     ```yaml
     rpc_address: <new_node_ip>
     ```
   - **Seed Nodes:** Add the IP addresses of one or more nodes from the existing cluster as seed nodes. Don't include the new node as a seed for itself.
     ```yaml
     seeds: "<seed_node_ip_1>,<seed_node_ip_2>"
     ```
   - **Data and Log Directories:** Configure the directories for storing data and logs.
     ```yaml
     data_file_directories: - /var/lib/cassandra/data
     commitlog_directory: /var/lib/cassandra/commitlog
     hints_directory: /var/lib/cassandra/hints
     saved_caches_directory: /var/lib/cassandra/saved_caches
     ```

### 3. **Configure JVM Options**

   - Edit `jvm.options` or `cassandra-env.sh` to configure JVM options based on your hardware specifications and performance requirements.

### 4. **Start Cassandra on the New Node**

   - Start the Cassandra service on the new node:
     ```
     sudo service cassandra start
     ```
     or
     ```
     sudo systemctl start cassandra
     ```

### 5. **Verify the Node Joins the Cluster**

   - Use `nodetool status` from an existing node to check if the new node has joined the cluster:
     ```
     nodetool status
     ```

### Additional Tips:

- Ensure the new node has network connectivity to all existing nodes in the cluster.
- Match the Cassandra configuration as closely as possible to the existing nodes, especially settings that impact cluster behavior.
- If you have any specific configurations like custom compaction strategies or user-defined types, ensure they are consistently configured across all nodes.
- Update firewall rules to allow traffic on Cassandra's ports, typically 7000 (for internode communication) and 9042 (for CQL clients).

Remember, the process may vary slightly depending on the specifics of your environment and the version of Cassandra. Always refer to the Cassandra documentation for the version you are using for the most accurate and detailed instructions.
