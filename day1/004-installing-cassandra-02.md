Installing Apache Cassandra using Docker simplifies the process and ensures you have a clean, isolated environment for Cassandra. Here's a step-by-step guide to installing Cassandra using Docker:

### 1. Install Docker
If you don't have Docker installed on your Linux system, install it first. The commands may vary depending on your Linux distribution. For Debian-based systems like Ubuntu, use:

```bash
sudo apt update
sudo apt install docker.io
```

After installation, start and enable Docker:

```bash
sudo systemctl start docker
sudo systemctl enable docker
```

### 2. Pull the Cassandra Docker Image
You can pull the official Cassandra image from Docker Hub. To get the latest version, use:

```bash
sudo docker pull cassandra
```

If you need a specific version of Cassandra, specify the tag. For example, for Cassandra 3.11:

```bash
sudo docker pull cassandra:3.11
```

### 3. Run Cassandra Container
To run Cassandra in a Docker container, use:

```bash
sudo docker run --name cassandra -d cassandra
```

This command will start a new container named `cassandra` using the Cassandra image. The `-d` flag runs the container in detached mode (in the background).

### 4. Verify Cassandra is Running
To ensure Cassandra is running correctly in the container, use:

```bash
sudo docker exec -it cassandra nodetool status
```

### 5. Access Cassandra
To interact with Cassandra, use `cqlsh` within the container:

```bash
sudo docker exec -it cassandra cqlsh
```

### 6. Customizing Cassandra Configuration (Optional)
If you need to customize the Cassandra configuration, you can create a custom `cassandra.yaml` file and mount it to the Docker container. For example:

```bash
sudo docker run --name cassandra -v /path/to/custom/cassandra.yaml:/etc/cassandra/cassandra.yaml -d cassandra
```

Replace `/path/to/custom/cassandra.yaml` with the path to your custom configuration file.

### 7. Data Persistence (Optional)
To persist data, you should mount a directory from the host to store Cassandra data:

```bash
sudo docker run --name cassandra -v /path/to/cassandra/data:/var/lib/cassandra -d cassandra
```

Replace `/path/to/cassandra/data` with the path to your desired host directory.

### 8. Using Docker Compose (Optional)
For more complex setups, like clustering, Docker Compose is recommended. You'll need to create a `docker-compose.yml` file with the necessary configurations.

### Notes
- Make sure your Docker service is running before executing these commands.
- Adjust the commands according to your requirements and Linux distribution.
- Always check the [official Docker Hub page for Cassandra](https://hub.docker.com/_/cassandra) for more detailed information and configuration options.

Using Docker for Cassandra can significantly simplify deployment and configuration, especially when scaling or creating isolated environments for development and testing.