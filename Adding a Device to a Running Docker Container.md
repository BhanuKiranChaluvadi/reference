
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
