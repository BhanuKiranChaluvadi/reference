# Adding a Network Interface to a Running Docker Container

**NOTE: This guide involves advanced system administration tasks that can affect network behavior. Be sure to understand the implications of each step and consider security and connectivity impacts before using these commands.**

This guide explains how to add a network interface (e.g., `eth1`) to a running Docker container using Docker and `nsenter`.

## Step 1: Identify the Container's PID

First, you need to identify the PID of the running Docker container where you want to add the network interface. Replace `CONTAINER_ID` with the ID of your Docker container:

```bash
docker inspect --format '{{.State.Pid}}' CONTAINER_ID
```

This command outputs the PID of the specified Docker container.

## Step 2: Add the Network Interface to the Container

Replace `NETWORK_NAMESPACE_PATH` with the path of the network namespace file (e.g., `/var/run/docker/netns/35847b8440f8`), `INTERFACE_NAME` with the name of your network interface (e.g., `eth1`), and `CONTAINER_PID` with the PID of your Docker container:

```bash
sudo nsenter --net=NETWORK_NAMESPACE_PATH ip link set INTERFACE_NAME netns /proc/CONTAINER_PID/ns/net
```

This command moves the specified network interface into the network namespace of the Docker container.

---

**Please note:** These operations require root access and can have security implications. Make sure to understand what each step is doing and consider these implications before using these commands. It's also worth noting that this change won't persist if the container is restarted. If you need a persistent change, consider adding the network interface when starting the container or using Docker's networking options.


---

# Adding a Network Interface to a Running Docker Container

**NOTE: This guide involves advanced system administration tasks that can affect network behavior. Be sure to understand the implications of each step and consider security and connectivity impacts before using these commands.**

This guide explains how to add a network interface (e.g., `eth1`) to a running Docker container using Docker and `nsenter`.

## Step 1: Identify the Interface Name

First, identify the name of the network interface that you want to add to the Docker container:

```bash
ip link show
```

This command lists all network interfaces available on your system.

## Step 2: Find the Container's Network Namespace Name

Next, find the network namespace name of the Docker container. 

```bash
docker inspect $(docker ps -aq) -f '{{.Name}} ns  {{.NetworkSettings.SandboxKey}}'
```

This command displays the names and network namespace paths of all Docker containers currently running on your system.

## Step 3: Move the Network Interface to the Container's Namespace

Replace `INTERFACE_NAME` with the name of your network interface (e.g., `eth1`), and `NAMESPACE_PATH` with the network namespace path of your Docker container:

```bash
ip link set INTERFACE_NAME netns NAMESPACE_PATH
```

This command moves the specified network interface into the network namespace of the Docker container.

## Step 4: Verify the Network Interface Inside the Container's Namespace

Next, verify that the network interface is now inside the Docker container's network namespace. Replace `NAMESPACE_PATH` with the network namespace path of your Docker container:

```bash
nsenter --net=NAMESPACE_PATH ip link show
```

This command lists all network interfaces available in the Docker container's network namespace.

## Step 5: Move the Network Interface Back to the Host's Namespace

If you want to move the network interface back to the host's namespace, you can do so with the following command. Replace `INTERFACE_NAME` with the name of your network interface:

```bash
nsenter --net=NAMESPACE_PATH ip link set INTERFACE_NAME netns /proc/1/ns/net
```

This command moves the network interface from the Docker container's network namespace back to the host's network namespace.

---

**Please note:** These operations require root access and can have security implications. Make sure to understand what each step is doing and consider these implications before using these commands. Also, be aware that these changes will not persist if the Docker container is restarted. If you need a persistent change, consider adding the network interface when starting the Docker container or using Docker's networking options.
