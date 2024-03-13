# Industrial Communication Compatibility Matrix

Understanding the nuances of industrial communication can be overwhelming, especially when distinguishing between communication protocols (like Modbus) and the interfaces or mediums through which they operate (like RS485). A relatable analogy might offer clarity.

## An Analogy: Letters in a Town

Imagine you're in a town where people communicate by sending handwritten letters to each other.

1. **Modbus** can be likened to the specific language and style of writing that the townspeople have agreed upon. For instance, everyone begins their letters with "Dear [Name]," and concludes with "Regards." By adhering to this structure, it guarantees each recipient grasps the intended message when they peruse their letters.

2. **RS485**, in contrast, mirrors the town's postal service. It's the system responsible for delivering these letters from sender to receiver. The postal service itself has its own set of regulations: every letter must be contained within an envelope, a stamp needs to be affixed at the top right corner, among other stipulations.

Yet, the townspeople have alternative means of relaying messages too, such as employing pigeons or perhaps shouting across lanes. Analogously, Modbus (the letter-writing style) can be relayed using channels other than RS485 (akin to the postal service).

In essence:
- **Modbus** = The standardized format or style of the message.
- **RS485** = One of many avenues to dispatch that message.

---

## Compatibility Table

|                     | RS485 | RS232 | Ethernet | CAN   | USB    |
|---------------------|:-----:|:-----:|:--------:|:-----:|:------:|
| **Modbus**          | ✓     | ✓     | ✓        |       |        |
| **Profibus**        | ✓     |       |          |       |        |
| **Profinet**        |       |       | ✓        |       |        |
| **EtherCAT**        |       |       | ✓        |       |        |
| **DeviceNet**       |       |       |          | ✓     |        |
| **CANopen**         |       |       |          | ✓     |        |
| **BACnet**          | ✓     | ✓     | ✓        |       |        |
| **FOUNDATION Fieldbus** | ✓ |       |          |       |        |
| **OPC UA**          | ✓     | ✓     | ✓        |       | ✓      |
| **Ethernet/IP**     |       |       | ✓        |       |        |
| **CC-Link**         | ✓     |       | ✓        |       |        |

---

## Articles
### Modbus

- [By National Instruments](https://www.ni.com/en/shop/seamlessly-connect-to-third-party-devices-and-supervisory-system/the-modbus-protocol-in-depth.html)

### serial communication

- [rs485-vs-rs232-vs-rs422](https://allmeteo.com/rs485-vs-rs232-vs-rs422)

## Notes

- The matrix above signifies typical or standard pairings. Non-standard configurations might exist in specialized settings or with the help of additional equipment or software.
- Protocols like CANopen and DeviceNet are intrinsically tied to a particular interface (in this case, CAN). Relaying them through a different medium, like RS485, typically necessitates a specialized gateway or bridge.
- Some protocols, such as OPC UA, are versatile and adaptable to numerous mediums. However, some implementations might be more prevalent than others.

It's paramount to consult with technical documentation or industry experts before establishing any communication systems based on this matrix.

## Modbus vs. RS485: Breaking Down the Difference

Modbus and RS485 are terms often thrown around interchangeably, but they stand for distinct concepts. Let's delve deeper:

### **Nature:**

- **Modbus**: 
  - A communication protocol.
  - Dictates how data is structured and how devices converse to send and receive this data.
  - Originally created by Modicon (now Schneider Electric) in 1979 for PLCs.
  - Today, it's a standard communication protocol in the industrial domain.
  
- **RS485**:
  - Also known as TIA-485(-A) or EIA-485.
  - An electrical specification for multi-point communication.
  - Sets the electrical characteristics of drivers and receivers, usually used in differential mode.

### **Purpose:**

- **Modbus**: 
  - Ensures devices communicate data in a structured manner.
  - Variants include Modbus RTU, Modbus ASCII, and Modbus TCP/IP.
  
- **RS485**:
  - Specifies electrical characteristics for long-range, multi-point data transfer.

### **Usage:**

- **Modbus**: 
  - Implemented over various layers, including RS485, RS232, and TCP/IP.
  
- **RS485**:
  - Acts as the physical layer for several protocols, with Modbus RTU being a prominent example.

### **Components:**

- **Modbus**: 
  - Comprises defined function codes, response structures, and error-handling methods.
  
- **RS485**:
  - Involves details about voltage levels, maximum transmission lengths, and number of devices on a line.

### **Illustrative Comparison:**

Imagine sending a letter. The language and structure (e.g., English, date format, greetings) is like Modbus. The delivery mechanism, say a postal system with its own rules about weight, size, and stamping, is RS485. Put simply, Modbus is the content, RS485 is the delivery method.



