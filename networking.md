## Basic 

[Udacity course](https://www.udacity.com/course/networking-for-web-developers--ud256)

## Tools

```bash
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install netcat-openbsd tcpdump traceroute mtr
```


## Serial Port Vs Network Port
### Serial Port (`/dev/ttyUSB0`)

- In the context of `/dev/ttyUSB0`, a serial port refers to a physical or virtual communication interface that allows serial communication between a computer and a device, such as a USB-to-serial converter or a serial device connected via USB.
- `/dev/ttyUSB0` is a device file that represents a specific serial port in the Linux operating system.
- Serial ports are used for serial communication protocols, such as RS-232, RS-485, or UART, which involve sending and receiving data bit by bit over a single wire or multiple wires.
- `/dev/ttyUSB0` is associated with the USB-to-serial device connected to the system and provides a way to read from and write to that device.

### Network Port

- In networking, a network port is a numbered endpoint that identifies a specific application or service running on a device within a network.
- Network ports are used in the TCP/IP protocol suite to allow multiple applications or services to share a single IP address on a networked device.
- Network ports are identified by port numbers ranging from 0 to 65535.
- Commonly used network ports are standardized, such as port 80 for HTTP, port 443 for HTTPS, and port 22 for SSH.
- Network ports facilitate communication between different devices on a network by directing network traffic to the appropriate application or service based on the port number.
