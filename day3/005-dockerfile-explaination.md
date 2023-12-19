### Docckerfile Parameters.

In a Dockerfile, `CMD` and `RUN` are both instructions, but they serve different purposes and are used in different contexts.

1. **RUN**:
   - **Purpose**: The `RUN` instruction is used to execute commands during the build phase of the Docker image. It is primarily used for installing software, libraries, and doing other setup and configuration tasks that should happen when the image is being created.
   - **Behavior**: Each `RUN` command creates a new layer in the Docker image. After the command is executed, the results are committed to the image, and the next instruction in the Dockerfile is processed. 
   - **Example**: `RUN apt-get update && apt-get install -y python3`.

2. **CMD**:
   - **Purpose**: The `CMD` instruction is used to set the default command that will be executed when a container is started from the image. It is used to define what the container should do by default when it starts up. 
   - **Behavior**: Unlike `RUN`, `CMD` does not execute anything at build time. It specifies the command that will be executed at runtime, when the container is started. Only the last `CMD` instruction in the Dockerfile will have an effect. If you start a container with an alternative command, it will override the `CMD` instruction.
   - **Example**: `CMD ["python3", "-u", "myscript.py"]`.

In summary, `RUN` is for building the Docker image (things you do before the container starts), and `CMD` is for running the container (what happens when you start the container).

--------------------


Including a `CMD` instruction in your Dockerfile is not strictly necessary for keeping a container in a running state, but it is often essential for defining the primary task the container should perform when it starts. The role of `CMD` is to specify the default command that should be executed when the container is run.

However, whether or not the container remains in a running state depends on the nature of the command specified in `CMD` (or in the `docker run` command if it overrides `CMD`):

1. **Long-Running Processes**: If the `CMD` specifies a long-running process, like a web server, database, or any other service that runs indefinitely, the container will stay running as long as that process is active.

2. **One-Time Tasks**: If the `CMD` specifies a command that completes its task and exits, such as a script that performs a calculation and then finishes, the container will stop once the command completes.

To ensure that your container stays running, you might consider the following:

- **Use a Service**: If the purpose of your container is to run a service (like a web server), ensure that the `CMD` starts that service in the foreground.

- **Keep-Alive Techniques**: For containers that don't inherently run a long-term process, you might use techniques to keep them alive. This can include running a command that doesn't exit, like `tail -f /dev/null` or starting a shell.

- **No `CMD`**: If you don't include a `CMD`, Docker will use the default command defined in the base image specified by the `FROM` instruction. If this default command is a long-running process, the container will remain running.

In summary, whether or not you need a `CMD` in your Dockerfile to keep the container running depends on what the container is meant to do. For most practical applications where the container is meant to provide a continuously running service, a `CMD` that initiates a long-running process is indeed necessary.

----------------


If you have multiple `CMD` instructions in a Dockerfile, only the last `CMD` will take effect. Dockerfiles can contain multiple `CMD` instructions, but unlike `RUN` instructions, where each one adds a new layer to the image and all of them are executed in sequence, only the final `CMD` in the Dockerfile will be executed when a container is run from the image.

Here's a breakdown:

- **During Image Build**: When the Docker image is being built, Docker reads and processes each instruction in the Dockerfile sequentially. However, for `CMD` instructions, Docker doesn't execute them during the build; it merely notes them.

- **Final `CMD` Instruction**: The last `CMD` instruction in the Dockerfile is the one that Docker will use as the default command to run when a container is started from the built image.

- **Overriding `CMD`**: When you run a container, you can override the `CMD` specified in the Dockerfile by providing a command at the end of the `docker run` command. This is a common practice when you want to run different processes or tasks using the same image.

For example, in a Dockerfile like this:

```Dockerfile
CMD ["echo", "First Command"]
CMD ["echo", "Second Command"]
CMD ["echo", "Final Command"]
```

Only the `Final Command` will be executed when a container is run from this image. The other `CMD` instructions are effectively ignored.

-------------

A Dockerfile supports several instructions, each serving a specific purpose in the process of building a Docker image. Here are the key instructions along with examples of their usage:

1. **FROM**: Specifies the base image to start with.
   - Example: `FROM ubuntu:20.04`

2. **RUN**: Executes commands in a new layer on top of the current image and commits the results.
   - Example: `RUN apt-get update && apt-get install -y python3`

3. **CMD**: Provides the default command to be executed when a container starts.
   - Example: `CMD ["python3", "-u", "app.py"]`

4. **LABEL**: Adds metadata to an image as a key-value pair.
   - Example: `LABEL maintainer="name@example.com"`

5. **EXPOSE**: Informs Docker that the container listens on the specified network ports at runtime.
   - Example: `EXPOSE 80`

6. **ENV**: Sets environment variables.
   - Example: `ENV API_KEY=123456`

7. **ADD**: Copies new files, directories, or remote file URLs and adds them to the filesystem of the container.
   - Example: `ADD https://example.com/big.tar.xz /usr/src/things/`

8. **COPY**: Copies new files or directories and adds them to the filesystem of the container.
   - Example: `COPY ./app /usr/src/app`

9. **ENTRYPOINT**: Allows you to configure a container that will run as an executable.
   - Example: `ENTRYPOINT ["python3", "-u", "app.py"]`

10. **VOLUME**: Creates a mount point with the specified name and marks it as holding externally mounted volumes from the native host or other containers.
    - Example: `VOLUME /data`

11. **USER**: Sets the username or UID to use when running the image and for any `RUN`, `CMD`, and `ENTRYPOINT` instructions that follow it.
    - Example: `USER nobody`

12. **WORKDIR**: Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it.
    - Example: `WORKDIR /usr/src/app`

13. **ARG**: Defines a variable that users can pass at build time to the builder with the docker build command.
    - Example: `ARG VERSION=1.0`

14. **ONBUILD**: Adds a trigger instruction that will be executed at a later time, when the built image is used as the base for another build.
    - Example: `ONBUILD RUN echo "Triggered on build"`

15. **STOPSIGNAL**: Sets the system call signal that will be sent to the container to exit.
    - Example: `STOPSIGNAL SIGTERM`

16. **HEALTHCHECK**: Tells Docker how to test a container to check that it is still working.
    - Example: `HEALTHCHECK CMD curl --fail http://localhost:80/ || exit 1`

17. **SHELL**: Allows the default shell used for the shell form of commands to be overridden.
    - Example: `SHELL ["powershell", "-command"]`

These instructions provide a comprehensive toolkit for creating Docker images that are customizable, maintainable, and efficient for various applications.



