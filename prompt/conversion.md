# Convert TwinCAT TcPOU XML to Structured Text (.st)

## Objective

Convert a valid XML file in the standard TwinCAT TcPOU format into a clean, human-readable Structured Text (.st) file.

## Requirements

### 1. Extract PLC Logic Only

* Remove all TwinCAT-specific XML tags, metadata, and attributes.
* Ignore declarations or elements not directly related to code logic or method bodies.

### 2. Output Format

* Generate a valid Structured Text file compliant with IEC 61131-3.
* Preserve all **logic**, **inline comments**, and **code structure**.
* Maintain consistent **indentation** and **line spacing** for readability.
* For each method:

  * Use `END_METHOD` after the implementation.
  * Provide tab-indented method bodies.

### 3. Output Constraints

* Output is intended for **manual editing** in IEC 61131-3 environments.
* Do **not** include any XML, wrapper objects, or annotations.

### 4. Error Handling

* If any part of the XML cannot be unambiguously converted:

  * Insert a clearly marked comment at the relevant location:

    ```st
    (* Conversion Warning: description of issue *)
    ```

## Output

Return only the converted Structured Text code.
