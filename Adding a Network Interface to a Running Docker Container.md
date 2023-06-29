---

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
