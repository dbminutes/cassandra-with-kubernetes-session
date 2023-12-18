# Glossary - (Short Version)

1. **Cassandra:** A highly scalable, distributed NoSQL database designed to handle large amounts of data across many commodity servers.

2. **Column Family:** Basic data structure of Cassandra, similar to a table in relational databases, but more flexible.

3. **Keyspace:** The highest level of data container in Cassandra, similar to a schema in SQL databases.

4. **Partition Key:** A primary key component that determines data distribution across nodes.

5. **Replication Factor:** Determines how many copies of data are maintained.

6. **Consistency Level:** Controls how many replicas in a cluster must acknowledge read or write operations.

7. **SSTable (Sorted String Table):** File format used to store data in Cassandra.

8. **Gossip Protocol:** Communication process between nodes to share information about the cluster's topology and state.

9. **Snitch:** Component that helps determine the network topology to route requests efficiently.

10. **Hinted Handoff:** Temporary storage of data meant for a node that is down.

11. **CQL (Cassandra Query Language):** SQL-like language used for querying Cassandra.

12. **Bloom Filter:** A space-efficient probabilistic data structure used to test whether an element is in a set.

13. **Read Repair:** Mechanism for maintaining consistency by updating stale replicas during read operations.

14. **Write Ahead Log (WAL):** Used for ensuring data durability.

15. **Compaction:** Process of merging SSTables to improve read efficiency.

16. **Vnodes (Virtual Nodes):** Mechanism for distributing data more evenly across a cluster.

17. **Secondary Index:** Allows queries on non-primary key columns.

18. **Tunable Consistency:** Ability to balance consistency and availability.

19. **Lightweight Transactions:** Provides conditional updates ensuring atomicity.

20. **Data Center:** Physical or virtual container of nodes.

21. **Rack:** Logical grouping of nodes, usually based on physical location.

22. **Node:** A single machine in a Cassandra cluster.

23. **Commit Log:** Log for durability that records every write operation.

24. **Memtable:** In-memory data structure where data is written before being flushed to SSTables.

25. **Tombstone:** Marker for a deleted column or row.

26. **Seed Node:** Initial contact point for a node joining a cluster.

27. **Paxos:** Protocol used for achieving consensus in a network of unreliable nodes, used in lightweight transactions.

28. **Time-to-Live (TTL):** Mechanism to specify how long data should live before being deleted automatically.

29. **Read Path:** Process describing how data is read from Cassandra.

30. **Write Path:** Process describing how data is written into Cassandra.

31. **Anti-Entropy Repair:** Process of synchronizing data across replicas.

32. **JMX (Java Management Extensions):** Used for monitoring and managing Cassandra.

33. **Cassandra Stress:** Tool for benchmarking and load testing Cassandra.

34. **DataStax:** A popular distribution of Cassandra with additional features and enterprise support.

35. **Hint Store:** Place where hinted handoffs are stored temporarily.

36. **LWT (Lightweight Transactions):** Refers to Cassandra's lightweight transactions feature.

37. **SSTableLoader:** Tool for bulk loading data into a Cassandra cluster.

38. **Super Column:** Deprecated feature, was a special column that contained a map of sub-columns.

39. **Cassandra.yaml:** Configuration file for Cassandra nodes.

40. **Distributed Architecture:** Refers to Cassandra's distributed and decentralized design.

41. **Peer-to-Peer:** Describes Cassandra's node communication model.

42. **Eventual Consistency:** Consistency model where updates reach all nodes eventually.

43. **Batch Operations:** Feature to execute multiple DML (Data Manipulation Language) operations as a single atomic operation.

44. **Data Modeling:** Process of structuring data to fit Cassandra's architecture.

45. **Partitioner:** Determines the distribution of data across the cluster.

46. **Repair:** Process of synchronizing replicas in a cluster.

47. **Schema Migration:** Process of updating Cassandra's data model.

48. **Cassandra File System (CFS):** Cassandra's distributed file system.

49. **Nodetool:** Command line tool for managing Cassandra.

50. **Client Libraries:** Libraries in various programming languages for interacting with Cassandra.


