**Resources:**

- [how-to-access-serial-devices-in-docker](https://www.losant.com/blog/how-to-access-serial-devices-in-docker)
- [docker-a-way-to-give-access-to-a-host-usb-or-serial-device)](https://stackoverflow.com/questions/24225647/docker-a-way-to-give-access-to-a-host-usb-or-serial-device)

Sure, here is the previous information formatted in markdown:

---

# Setting udev Rules for ttyUSB Devices

The following steps will guide you through creating a udev rule for a `ttyUSB` device, such as a virtual serial port created with socat:

## Step 1: Create a New udev Rule File

Open a new udev rules file in a text editor (e.g., nano). This file should be in the `/etc/udev/rules.d/` directory and have a .rules extension. Here, we'll create a file named `99-ttyUSB.rules`:

```bash
sudo nano /etc/udev/rules.d/99-ttyUSB.rules
```

## Step 2: Write the Rule

In the new file, write a rule that matches `ttyUSB` devices and sets their permissions and ownership as needed. Here's an example:

```bash
KERNEL=="ttyUSB*", MODE="0666", OWNER="yourusername", GROUP="dialout"
```

This rule matches any device whose kernel name is `ttyUSBn`, where `n` is a number. The `MODE="0666"` part sets permissions so all users can read from and write to the device. The `OWNER` and `GROUP` parts set device ownership to a specific user and group. Be sure to replace `"yourusername"` with your actual username.

## Step 3: Save and Close the File

After writing the rule, save and close the file.

## Step 4: Reload the udev Rules

Finally, use the following commands to reload the udev rules:

```bash
sudo udevadm control --reload-rules
sudo udevadm trigger
```

Now, when you plug in or create `ttyUSB` devices, they should be accessible to all users, thanks to your new udev rules.

> **Note:** Always be careful when changing device permissions, as unrestricted access can pose a security risk. Only grant necessary access to the users who need it.

---
