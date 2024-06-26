
## Color Coding
### PLC
When configuring your EtherCAT terminals, follow this path: **Devices > EtherCAT > Term X > Term Y > Drop Down Menu**. Here, you will encounter various colored boxes, each representing a different type of information:

- **Yellow:** Represents **inputs**. This color indicates data traveling from the terminal to the PLC (Programmable Logic Controller).
- **Red:** Signifies **outputs**. It shows when the output to PLC is written back to the terminal, denoting data movement from the PLC to the terminal.
- **Green:** Indicates **status** information about the terminal or connection. And it is Acyclic.

### HMI
This explaing the color schema of various variable the you encounter in Beckhoff HMI
- **S Blue:** S repesents the server symbol. These are linked symbols (read/write) to PLC code.
- **C Green** C stands for HMI controls. We are using a property of the HMI Controls from the beckoff. Control interface properties like button background color etc.
- **P yellow** P Stands for parameters. These are the input and ouput params for a function.

## Arrow Navigation

To delve into the details of a terminal variable, navigate through the interface until you reach the desired terminal variable. If the variable is linked to another variable, you'll notice a **diagonal pointing arrow** at the bottom left corner of the variable color box.

- To explore this link further, **right-click** on the arrow and select **"Go To Link Variable"**. This action will direct you to the associated variable for more detailed examination.

## F2 Button

The F2 button serves as a shortcut to view and manage variables within your code efficiently:

1. Press **F2** to open a navigation pane.
2. Navigate through **Categories > Instance Calls** and select the desired **Block**.

This process organizes all input and output arguments of the block instance, allowing you to easily fill in the required values.

## Enable Smart Coding

To enhance your coding efficiency with Smart Coding features, follow these steps:

1. Go to **Debug > Options > TwinCAT > PLC Environment > Smart Coding**.
2. **Enable** most (if not all) of the available options to leverage advanced coding functionalities and assistive features.

By activating Smart Coding, you can streamline your development process, reduce errors, and improve the overall quality of your code.
