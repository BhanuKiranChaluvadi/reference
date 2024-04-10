
# Beckhoff Terminal Configuration Guide

This guide provides step-by-step instructions for configuring Beckhoff terminals, specifically focusing on the EL7332 and EL5131 models for motor and encoder control, respectively.

## 1. Terminal Scanning

Scan for the Beckhoff terminals to identify the available devices.

## 2. Variable Linking

Check and link variables for the control system:

- For EL7332 (Drive), auto-connected variables are used for motor control.
- For EL5131 (Encoder), variables must be manually linked.

### Drive Variables Linking

1. Go to `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N` -> `Drive` -> `NC-Drive`.
2. Click on `Link To variable`.

### Encoder Variables Linking

1. Navigate to `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N` -> `Enc` -> `NC-Encoder`.
2. Select `Link To variable`.

## 3. Startup Task Configuration

For each terminal, particularly Drive (EL7332), add a "Startup" task:

1. Navigate to `I/O` -> `Devices` -> `Device N (Ethercat)` -> `Term N (EK1100)` -> `Term N (EL7332)` -> `Startup`.
2. Click on `New` and navigate to section `8020:0`.

Enter the following parameters:

- Maximum current: `210`
- Nominal current: `150`
- Nominal Voltage: `24000`
- Motor coil resistance: `5460`
- Reduced current (positive): `100`
- Reduced current (negative): `100`

Avoid using CoE-online as it permanently writes values to the terminal, posing a risk if the terminal fails.

## 4. NC-Task Axis Configuration

Modify the NC-Task axis specific parameters by navigating to:

- `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N` -> `settings`.

### Adjust Parameters

- Go to `Parameters` under the same menu.
- Set `Maximum Dynamics` and `Default Dynamics` as needed.
- Configure `Manual Motion and Homing` and `Monitoring` settings.

## 5. Encoder Parameters Modification

For NC-Task Encoder specific parameters, navigate to:

- `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N` -> `Enc` -> `parameter`.

Configure the encoder evaluation settings, such as the inversion of counting direction and scaling factors.

## 6. Drive Parameters Modification

Adjust the Drive specific parameters at:

- `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N` -> `Drive` -> `parameter`.

Ensure settings like `Invert Motor Polarity` are correctly set.

## 7. Saving and Activation

Save all changes and activate the configuration to apply the settings.

## 8. Motor Enabling

To enable the motor:

1. Navigate to `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N`.
2. Double-click, go online, and enable the motor.

## 9. Testing Motor Function

Under `Functions`, test the motor operation with specified output modes and values.

## 10. Program Compilation and Linking

To control the motor via a program:

1. Write and compile the program including necessary library references.
2. Link the generated variables to the NC-Task.

```xml
PROGRAM MAIN
VAR
    nAlive: UDINT;    
END_VAR

nAlive:= nAlive +1;

P_Motion();
```
```xml
PROGRAM P_Motion
VAR
	bEnable: BOOL;
	bReset: BOOL;
	bStart: BOOL;
	bStop: BOOL;
	fPosition: LREAL;
	fVelocity: LREAL:= 0.5;

	bPositiveEndstop AT %I*: BOOL;
	bNegativeEndstop AT %I*: BOOL;
	
	stAxis: Tc2_MC2.AXIS_REF;
	fbPower: Tc2_MC2.MC_Power; 
	fbReset: Tc2_MC2.MC_Reset;
	fbHalt: Tc2_MC2.MC_Halt;
	fbMoveAbsolute: Tc2_MC2.MC_MoveAbsolute;
END_VAR

fbPower(
	Axis:= stAxis, 
	Enable:= bEnable, 
	Enable_Positive:= TRUE, 
	Enable_Negative:= TRUE, 
	Override:= , 
	BufferMode:= , 
	Options:= , 
	Status=> , 
	Busy=> , 
	Active=> , 
	Error=> , 
	ErrorID=> );
	
fbReset(
	Axis:= stAxis, 
	Execute:= bReset, 
	Done=> , 
	Busy=> , 
	Error=> , 
	ErrorID=> );	

fbHalt(
	Axis:= stAxis, 
	Execute:= bStop, 
	Deceleration:= , 
	Jerk:= , 
	BufferMode:= , 
	Options:= , 
	Done=> , 
	Busy=> , 
	Active=> , 
	CommandAborted=> , 
	Error=> , 
	ErrorID=> );	
	
fbMoveAbsolute(
	Axis:= stAxis, 
	Execute:= bStart, 
	Position:= fPosition, 
	Velocity:= fVelocity, 
	Acceleration:= , 
	Deceleration:= , 
	Jerk:= , 
	BufferMode:= , 
	Options:= , 
	Done=> , 
	Busy=> , 
	Active=> , 
	CommandAborted=> , 
	Error=> , 
	ErrorID=> );
```

## 11. Linking PLC Varaibles
Link the axis to `Tc2_MC2.AXIS_REF` in the NC-Task settings, and associate the endstop variables accordingly.

1. Navigate to `Motion` -> `NC-Task 1 SAF` -> `Axes` -> `Axis N`.
2. `Double Click` -> `setting tab` -> `Link To PLC` -> ` Link the correspoinding varaible from the program

1. Navigate to `I/O` -> `Devices` -> `Device N (Ethercat)` -> `Term N (EK1100)` -> `Term N (EL7332)`
It is a 4 channel digital input. You can use "Link to" double click for the program variables to appear.

## 12. Final Setup and Verification

Complete the setup by linking all necessary variables and inputs in the configuration, and verify the system's operational status.
