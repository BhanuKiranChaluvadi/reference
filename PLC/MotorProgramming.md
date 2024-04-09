
1. Scan for the beckhoff terminals

2. Check for the linked variables. In our case EL7332 for controlling/Drive the motor and encoder EL5131 are different. They should be matched with the NC-Task axes

Only Drive EL7332 variables are auto connected
NC-Drive option in Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Drive --> NC-Drive --> Link To variable

Manually link the encoder variables
NC-Drive option in Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Enc --> NC-Encoder --> Link To variable


3. Add "Startup" task for the each terminal. In our case all the Drive(EL7332) terminals. Do not use CoE-online as they are flashed directly into the terminal and problem will arise if the terminal goes bad and values are not present in the version control.
  I/O --> Devices --> Device N (Ethercat) --> Tern N (EK1100) --> Term N (EL7332) --> Startup --> New --> Navigate to section 8020:0
Added
  1. Maximum current --> 210
  2. Nominal current --> 150
  3. Nominal Voltage  --> 24000
  4. Motor coil resistance --> 5460
  5. Reduced current (positive) --> 100
  6. Reduce current (negative) --> 100

5. Modify the NC-Task Axis Specific parameters

  You can see which PLC terminal this Axis is connected
   Motion --> NC-Task 1 SAF --> Axes --> Axis N --> settings 

   Adjust Paramters 
  Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Parameters

  Maximum Dynamics:
    Reference Velocity (1.0)
    Maximum Velocity (1.0)
    Maximum Acceleration(1.0)
    Maximum Deceleration (1.0)
Default Dynamicd:
  Default Acceleration (4.0)
  Default Deceleration (4.0)
Manual Motion and Homing
  Homing Velocity (towards plc cam) (1.0)
  Homing Velocity (off plc cam) (1.0)
  Manual Velocity (Fast) (1.0)
  Manual Velocity (Slow) (1.0)
Monitoring
  Position Lag Monitoring (FALSE)

  
6. Modify the Nc-Task Encoder specific parameters

  Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Enc --> parameter
  Encoer Evaluation
    Invert Encoder Counting Direction ? (True)
    scaling Factor Numerator (mm/INC) (1.0)
    Scale Factor Numerator (mm/INC) (135168.0)
  
7. Modify the Nc-Task Drive specific parameters
  Motion --> NC-Task 1 SAF --> Axes --> Axis N --> Drive --> parameter
  Output Settings:
    Invert Motor Polarity : TRUE
   

9. Save all changes --> Activate Configuration 

10. Enable Motor
  Motion --> NC-Task 1 SAF --> Axes --> Axis N --> double click --> online  --> Enabling --> set --> select all --> OK

11. Try and run in Functions
   Motion --> NC-Task 1 SAF --> Axes --> Axis N --> double click --> Functions --> Raw rive output
    Output Mode: Velocity
    Output Value: 1 mm/s
    CLick on Start. and the motor should move in some [positive] direction.
    
 
