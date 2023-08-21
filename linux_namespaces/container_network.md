# Finding Network Namespace in a Docker Container

Docker utilizes namespaces to provide isolated workspaces for containers. One of the namespaces created by Docker is the network namespace, which gives the container its own network stack. 

This guide will show you how to find the network namespace of a Docker container.

First you find the interface name with 
```bash
ip link show
```

## Step 1: Inspect the Docker Container

Use the `docker inspect` command with the `--format` option to retrieve the network namespace of a specific container. Replace `<container_id>` with the ID or name of your Docker container:

```bash
docker inspect --format '{{ .NetworkSettings.SandboxKey }}' <container_id>
```

This command returns the file path of the network namespace associated with the given container. An example output might look like this:

```
/var/run/docker/netns/3e8f2cb8e3c4
```

Note: This file path is not directly accessible because Docker places these namespaces in a special mount namespace for security reasons.

## Step 2: Enter the Network Namespace (Optional)

If you need to enter the network namespace for debugging or other purposes, you will need to use a tool like `nsenter`. 

First, retrieve the process ID (PID) of the Docker container:

```bash
docker inspect --format '{{ .State.Pid }}' <container_id>
```

Then, use `nsenter` to run a command in the network namespace:

```bash
nsenter -t <PID> -n <command>
```

In this command, `<PID>` is the PID of the Docker container, and `<command>` is the command you wish to execute in the container's network namespace. The `-n` option instructs `nsenter` to enter the network namespace of the container.

Please note that if your Docker version uses a private mount namespace or your system does not support `nsenter`, you might need to use Docker's own commands, such as `docker exec`, to interact with the container's network namespace.

As always, please be aware of the implications of entering a container's namespaces, as it can potentially impact the isolation and security of the container.



##############################################

Here is the commands to move a socket interface into a container

First you find the interface name with 

```bash
ip link show
```
 

Secondly you find your container network namespace name with the command

```bash
docker inspect $(docker ps -aq) -f '{{.Name}} ns  {{.NetworkSettings.SandboxKey}}'
```
 

Next you move the interface to the new namespace

```bash
ip link set eth1 netns /var/run/docker/netns/35847b8440f8
```
 

Then you can verify from the host with the command

```bash
nsenter --net=/var/run/docker/netns/35847b8440f8 ip link show
```
 

If you kill the container and thereby also the namespace the interface does come back to the host

Alternatively you can run the command

```bash
nsenter --net=/var/run/docker/netns/35847b8440f8 ip link set eth1 netns /proc/1/ns/net
```

# Way 2:
```bash
Here is the commands to move a socket interface into a container

First you find the interface name with 

ip link show

 

Secondly you find your container network namespace name with the command

docker inspect $(docker ps -aq) -f '{{.Name}} ns  {{.NetworkSettings.SandboxKey}}'

 

Next you move the interface to the new namespace

ip link set eth1 netns /var/run/docker/netns/35847b8440f8

 

Then you can verify from the host with the command

nsenter --net=/var/run/docker/netns/35847b8440f8 ip link show

 

If you kill the container and thereby also the namespace the interface does come back to the host

Alternatively you can run the command

nsenter --net=/var/run/docker/netns/35847b8440f8 ip link set eth1 netns /proc/1/ns/net


This should get you going with eth1 inside the container

```

This should get you going with eth1 inside the container
