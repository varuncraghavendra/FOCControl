
# Thrust Bench Testing

These steps are to be followed for proper bench testing of a motor on the ST Motor Workbench and the thrust bench.


## 1. Motor Profiling

### ST MOTOR PROFILER

The ST motor-profiler software tool finds profiled information for custom motors.

The ST Motor Profiler runs on a PC system using Windows and requires a USB type-A connector.

The “Motor Profiler” algorithm determines the correct motor parameters needed to configure the STM32 PMSM FOC firmware library:
 * Stator resistance (Rs)
 * Stator inductance (Ls)
 * B-EMF constant
 * Inertia and friction values.

These quantities have to be known/measured accurately before running the profiler: 

<img src="https://user-images.githubusercontent.com/120045092/215274001-73c6c000-c4f6-4a3b-a794-dc93cf9f9840.png" 
        alt="Picture" 
        width="470" 
        height="300" 
        style="display: block; margin: 0 auto" />

* Number of pole pairs
* Maximum speed of the application
* Maximum peak current of the motor and optionally Bus Voltage.
* Select Surface Mounted PMSM

#### All quantities are referenced to choice of Motor at given battery voltage and propeller combination.

*Number of pole pairs* -

![image](https://user-images.githubusercontent.com/120045092/215273848-b308eeb2-77e9-4ce0-b989-1229489b06bb.png)

Pole pairs in the permanent magnet rotors. Found out from the motor datasheet under motor configuartion - eg. "18N22P" = 22/2 = 11 Pole Pairs.

*Maximum speed of the application* - Not advised to exceed the RPM specified at 100% throttle in the motor, for high KV rated motors, 10,000 can be taken as a safe limit but a lower number like 8000 can be sufficient. 

*Maximum peak current of the motor* -

Throttle% ------- Current

![image](https://user-images.githubusercontent.com/120045092/215273900-52b80e5a-1e33-4fc6-875b-4b0e539fbb65.png)

Take the lower quantity among : current draw at 100% throttle from motor datsheet and maximum sink current of the power board. 

#### _Startup_
* Click on “Select Boards” to list supported boards. Our MCU and Power board pair are - IHM08.
* Click the “Connect” button. If communication with the board is successful it will display such.
* Mount the motor with propellers carefully on the bench, if not using the bench (no load run without propellers), hold the 3 wires of the motor to reduce free vibrations.
* Connect the battery and wait for 2 seconds.
* Click the “Start Profile” button. The profiling algorithm starts with several sequences.
* After the test is over, take a note of the measured quantities for reference.

![image](https://user-images.githubusercontent.com/120045092/215273784-9184804d-9163-4df1-a8fd-c0e2cad1cb17.png)

## 2. Motor Control Workbench

### Selection of the example project

Choose the STEVAL-ESC0001V1 example project and note the build procedure.


![image](https://user-images.githubusercontent.com/120045092/215282619-5fd336ec-5f2a-43f2-8825-6c9e92189552.png)

#### Home Screen

### Motor Profile Entry

Click on the M icon on the right to proceed, the following dialouge box will open.

![image](https://user-images.githubusercontent.com/120045092/215282708-c209127c-9961-40c0-9249-2acb0a50c9bb.png)

In this section enter the values for each parameter from the data obtained in the motor profiling routine.


### Startup parameters of the motor:

![image](https://user-images.githubusercontent.com/120045092/215283240-14a26533-cea5-4f8e-9187-0f6ab2d809b8.png)

#### Go to firmware drive management under control unit and select startup parameters.

![image](https://user-images.githubusercontent.com/120045092/215283316-d4bb9989-54bc-4c96-80be-ff073776a1b7.png)


#### The first current selection parameter, "final current ramp value" is for the alignment routine and the second "current ramp final value" is during the startup-to-running under closed loop routine.

* Check the box “Include alignment before ramp-up”.
* Set the motor alignment “Duration” to 2000 ms. This will align the motor to a fixed position by double pole alignment.
* Set the motor alignment “Final current ramp value” to ½ of the nominal motor current (in A).
* Set the “Speed ramp duration” to 3000 ms.
* Set the “Speed ramp final value” to 30% of the maximal motor speed (in RPM);
* Set the “Current ramp final value” to ½ of the nominal motor current (in A).
* Set the “Minimum start-up output speed” to 15% of the maximal motor speed (in RPM).






