# FC_NumConv Function Documentation

## Overview
The `FC_NumConv` function facilitates the conversion of values between various data types in a Beckhoff PLC environment. It handles different bit-length whole numbers as well as floating-point types.

## Inputs
1. **`Iany_Input`**: This variable holds the value you wish to convert. It can be of any whole number or float type.
2. **`Iany_Output`**: Provide a variable of the desired output type. The function uses this variable to determine the target type for conversion. The memory content of this variable will be overwritten with the converted value.

## Operation
The function evaluates the data type of `Iany_Input` and `Iany_Output` and then executes the appropriate conversion based on this evaluation. The actual data of the `Iany_Output` is then overwritten with the converted value.

## Usage
To use the function:
1. Provide the value you wish to convert in `Iany_Input`.
2. Provide a dummy/reference variable of the desired output type in `Iany_Output`.
3. Call the function. Post execution, the `Iany_Output` variable's memory will be overwritten with the converted value.

## Diagram Representation

```lua

    +-------------------+
    |   FC_NumConv      |
    |                   |
    |   +-----------+   |
    |   | Iany_Input|<----------[Conversion Logic]
    |   +-----------+   |
    |                   |
<----->| Iany_Output|   |
    |   +-----------+   |
    +-------------------+


```

## Key Points
- The function uses pointers and the `MEMMOVE` command to perform memory operations, ensuring efficient and fast conversions.
- For unsupported or unrecognized types, the function will simply return without making any changes to the `Iany_Output` variable.
- Ensure that the `Iany_Output` variable provided is of the correct data type to avoid unintended type conversions.

## Examples
1. **Convert BYTE to INT**:
    - Set a BYTE value in `Iany_Input`.
    - Provide an INT variable in `Iany_Output`.
    - Call `FC_NumConv`. Post execution, the INT variable will hold the converted value.

2. **Convert INT to REAL**:
    - Set an INT value in `Iany_Input`.
    - Provide a REAL variable in `Iany_Output`.
    - Call `FC_NumConv`. Post execution, the REAL variable will hold the converted value.

## Notes
- Be cautious about memory usage and ensure that the `Iany_Output` variable provided is initialized and of a valid type to prevent undefined behavior.

