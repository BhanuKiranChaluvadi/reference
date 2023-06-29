
---
# Adding a Device to a Running Docker Container

**NOTE: This guide is applicable only when using cgroups v1. Docker may not fully support this method if you're using cgroups v2.**

This guide describes how to add a device to a running Docker container using Docker, `nsenter`, and cgroups.

## Step 1: Identify the Container's cgroup

First, you need to identify the cgroup of the running Docker container where you want to insert the device. Use `docker inspect` to find information about the container:

```bash
docker inspect <container_id>
```

In the output, the "CgroupParent" field will tell you where the cgroup for the container is.

## Step 2: Identify Major and Minor Device Numbers

Identify the major and minor device numbers of the device you want to add. Replace `<device_name>` with the name of your device (e.g., `ttyUSB0`):

```bash
ls -l /dev/<device_name>
```

The command will output a line like this:

```bash
crw-rw---- 1 root dialout 188, 0 Jun 5 12:49 /dev/<device_name>
```

In this line, `188, 0` are the major and minor numbers, respectively.

## Step 3: Add the Device to the cgroup

Once you have the major and minor device numbers, you can add the device to the cgroup of the Docker container. Replace `<container_id>`, `<major>`, and `<minor>` with your container's ID and the device's major and minor numbers respectively:

```bash
echo "c <major>:<minor> rwm" > /sys/fs/cgroup/devices/docker/<container_id>/devices.allow
```

## Step 4: Identify the Container's PID

Next, identify the PID of the Docker container where you want to insert the device:

```bash
docker inspect --format '{{.State.Pid}}' <container_id>
```

## Step 5: Create Device Node Inside the Container

Use the `nsenter` command to create a new device node inside the container. Replace `<pid>`, `<device_name>`, `<major>`, and `<minor>` with the appropriate values:

```bash
nsenter -t <pid> -m mknod /dev/<device_name> c <major> <minor>
```

## Step 6: Set Appropriate Permissions

Lastly, set the appropriate permissions for the device node:

```bash
nsenter -t <pid> -m chmod 666 /dev/<device_name>
```

This command will give all users read and write access to the device. If you want to restrict access, you may want to use different permissions.

---

**Please note:** These operations require root access and can have security implications. Make sure to understand what each step is doing and consider these implications before using these commands.



Sure, here's a markdown document for the process described by your script.








---
# Adding a Device to a Running Docker Container

**NOTE: This guide is applicable only when using cgroups v1. Docker may not fully support this method if you're using cgroups v2.**

This guide explains how to add a device to a running Docker container by enabling access through cgroups, and then creating the device within the container.

## Step 1: Identify Major and Minor Device Numbers

Identify the major and minor device numbers of the device you want to add. Replace `device_name` with the name of your device (e.g., `ttyUSB0`):

```bash
ls -l /dev/device_name | grep device_name | awk '{print $5, $6}'
```

This command outputs the major and minor numbers of the specified device.

## Step 2: Get the ID of the Running Container

Replace `CONTAINER_NAME` with the name of your Docker container:

```bash
container_id=$(docker ps --quiet --all --no-trunc --filter "name=^${CONTAINER_NAME}$")
```

This command sets the `container_id` variable to the ID of the running Docker container with the specified name.

## Step 3: Allow Container's cgroup Access to the Device

Replace `DEVICE_MAJOR` and `DEVICE_MINOR` with the major and minor numbers of your device, and `container_id` with the ID of your Docker container:

```bash
echo "c ${DEVICE_MAJOR}:${DEVICE_MINOR} rwm" | sudo tee /sys/fs/cgroup/devices/docker/${container_id}/devices.allow
```

This command allows the Docker container's cgroup to access the specified device.

## Step 4: Create Device Directory Inside the Container

Replace `DEVICE_FOLDER_IN_CONTAINER` with the directory path inside the container where you want to create the device, and `CONTAINER_NAME` with the name of your Docker container:

```bash
docker exec ${CONTAINER_NAME} mkdir -p -m777 ${DEVICE_FOLDER_IN_CONTAINER}
```

This command creates the specified directory inside the Docker container, if it does not already exist.

## Step 5: Create Device Node Inside the Container

Replace `DEVICE_PATH_IN_CONTAINER` with the device path inside the container, `DEVICE_MAJOR` and `DEVICE_MINOR` with the major and minor numbers of your device, and `CONTAINER_NAME` with the name of your Docker container:

```bash
docker exec ${CONTAINER_NAME} mknod -m 666 ${DEVICE_PATH_IN_CONTAINER} c ${DEVICE_MAJOR} ${DEVICE_MINOR}
```

This command creates a new device node inside the Docker container.

---

**Please note:** These operations require root access and can have security implications. Make sure to understand what each step is doing and consider these implications before using these commands.
