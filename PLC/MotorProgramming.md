
1. Scan for the beckhoff terminals

2. Check for the linked variables. In our case EL7332 for controlling/Drive the motor and encoder EL5131 are different. They should be matched with the NC-Task axes

Only Drive EL7332 variables are auto connected
NC-Drive option in Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Drive --> NC-Drive --> Link To variable

Manually link the encoder variables
NC-Drive option in Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Enc --> NC-Encoder --> Link To variable
3. 
