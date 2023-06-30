# Container Networking and Namespaces

This document covers the concepts of container networking and namespaces with a focus on Docker containers.

**Resources:**

- [Container networking is simple!](https://iximiuz.com/en/posts/container-networking-is-simple/)
- [Docker container run metrics](https://docs.docker.com/config/containers/runmetrics/)

## Namespaces

In Linux, each process belongs to one instance of several types of namespaces. These namespaces provide isolation for certain aspects of system resources. The types of namespaces include, but are not limited to, PID namespaces, network namespaces, and mount namespaces.

Each process belongs to one network namespace, one PID namespace, one mount namespace, etc., and those namespaces are materialized under `/proc/<pid>/ns/`. For example, the network namespace of PID 42 is materialized by the pseudo-file `/proc/42/ns/net`.

You can explore the available namespaces using the `nsenter` tool. Run `nsenter --help` to view the available namespaces.

## Namespaces in Docker Containers

Docker uses namespaces to provide the isolated workspace called a container. When you run a container, Docker creates a set of namespaces for that container.

You can inspect a Docker container's namespaces. Here's an example of how to do it:

1. **Find the container's process ID (PID):**

    Docker assigns a unique PID to each container. You can find the PID of a container with the `docker inspect` command:

    ```bash
    PID=$(docker inspect --format '{{.State.Pid}}' <container-id>)
    ```

    Replace `<container-id>` with the ID or name of your Docker container.

2. **Run a command in the container's namespace:**

    You can use the `nsenter` command to run a command in a particular namespace of a process. Here's an example of how to use `nsenter` to run a `netstat -i` command in the network namespace of a Docker container:

    ```bash
    nsenter -t $PID -n netstat -i
    ```

    In this command, the `-t` flag specifies the target process whose namespace is to be entered. The value following `-t` is the PID (process ID) of the process. The `-n` flag instructs `nsenter` to enter the network namespace of the target process. The command `netstat -i` is then executed in this network namespace, effectively giving the output as if it were run inside the Docker container's network namespace.

**NOTE:** Always ensure you understand the implications of running commands within a container's namespaces, as it can have effects on the isolation and security of the container.
