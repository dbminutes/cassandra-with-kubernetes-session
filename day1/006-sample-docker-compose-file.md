This configuration will allow you to persist data in a directory on your host machine, ensuring that the data is retained even if the container is removed or updated.

Here's a basic example of what your `docker-compose.yml` file could look like:

```yaml
version: '3'

services:
  cassandra:
    image: cassandra:latest
    container_name: cassandra
    ports:
      - "9042:9042" # CQL
      - "9160:9160" # Thrift
    volumes:
      - /path/to/your/local/folder:/var/lib/cassandra
    environment:
      - CASSANDRA_CLUSTER_NAME=MyCluster
      - CASSANDRA_DC=DataCenter1
      - CASSANDRA_RACK=Rack1
    restart: always
```

### Explanation of the Configuration:
- **version**: Specifies the version of the Docker Compose file format. Version 3 is widely used.
- **services**: Defines the services (containers) to run. In this case, only one service for Cassandra.
- **image**: Specifies the Cassandra Docker image. You can use a specific version instead of `latest` if needed.
- **container_name**: Sets a custom name for your container.
- **ports**: Maps ports from the container to the host. Port `9042` is for CQL (Cassandra Query Language) and `9160` for Thrift (an older Cassandra client protocol).
- **volumes**: Maps a directory from the host (`/path/to/your/local/folder`) to the container’s data directory (`/var/lib/cassandra`). Replace `/path/to/your/local/folder` with the actual path on your host where you want to store Cassandra data.
- **environment**: Sets environment variables for Cassandra configuration. You can customize the cluster name, datacenter name, and rack name as needed.
- **restart**: Configures the restart policy for the container. `always` ensures that the container restarts automatically if it crashes or the Docker daemon is restarted.

### How to Use:
1. Replace `/path/to/your/local/folder` with the actual path on your host.
2. Save this configuration to a file named `docker-compose.yml`.
3. Run `docker-compose up -d` in the directory where your `docker-compose.yml` file is located to start Cassandra.

This setup will get you started with a basic Cassandra instance using Docker Compose. For more advanced configurations, such as setting up a Cassandra cluster with multiple nodes, you'll need to extend and modify this file accordingly.