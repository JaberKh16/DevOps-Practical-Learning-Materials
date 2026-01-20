The Dockerfile format is ==a simple plain text file that uses a Domain-Specific Language (DSL) to define the instructions for building a Docker image==. It typically has no file extension and defaults to the name `Dockerfile`.

Basic Format
Each instruction in a Dockerfile is a single line composed of a command (instruction keyword) followed by arguments.

Syntax:
	INSTRUCTION argument [argument...]

By convention, instruction keywords are written in **uppercase** to distinguish them from their arguments, though the builder is case-insensitive. Comments are indicated by a `#` character at the beginning of a line.


Key Instructions:
Instructions are executed sequentially from top to bottom, with each one creating a new, read-only layer in the final image. A Dockerfile must begin with a `FROM` instruction, except for parser directives or comments. 

Common instructions include:

- **`FROM`**: Specifies the base image from which you are building (e.g., `FROM ubuntu:22.04` or `FROM python:3.11-slim`).
- **`RUN`**: Executes commands in a new layer during the build process, often used for installing packages or running scripts (e.g., `RUN apt-get update && apt-get install -y curl`).
- **`WORKDIR`**: Sets the working directory for any subsequent `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions.
- **`COPY`**: Copies files and directories from the host machine to the container image (e.g., `COPY . /app`).
- **`ADD`**: Similar to `COPY`, but also supports fetching remote URLs and automatic extraction of tar archives.
- **`ENV`**: Sets environment variables within the container (e.g., `ENV FLASK_APP=app.py`).
- **`EXPOSE`**: Documents the network ports the container will listen on at runtime (e.g., `EXPOSE 8080`).
- **`CMD`**: Provides defaults for an executing container. This is the command that runs when the container starts. Only the last `CMD` instruction in a Dockerfile will take effect.
- **`ENTRYPOINT`**: Configures a container to run as an executable. It is often used in conjunction with `CMD` to set default arguments for the executable.


For an in-depth, official guide to all instructions and best practices, refer to the [Dockerfile reference documentation](https://docs.docker.com/reference/dockerfile/) on the [Docker website](https://www.docker.com/).