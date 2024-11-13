# Cruise Controller Assignment2

## Project OverView
The following assignment is to create a cruise controller system using Esterel. The purpose of this assignment was to have the ability to create a program which utilizes synchronous programming concepts. The code is split up into 1 main module and 3 submodules. The main module executes all 3 submodules in parallel to achieve our intended result.

## Constants Given
The following constants have been given
| Constant      | Value      |
|---------------|------------|
| SpeedMin      | 30.0km/h   |
| SpeedMax      | 150.0km/h  |
| SpeedInc      | 2.5km/h    |
| Kp            | 8.113      |
| Ki            | 0.5        |
| ThrottleSatMax| 45.0%      |
| PedalsMin     | 3.0%       |

## Inputs
The following inputs have been given
| Signal       | Type  | Description                               |
|--------------|-------|-------------------------------------------|
| On           | pure  | Enable the cruise control                 |
| Off          | pure  | Disable the cruise control                |
| Resume       | pure  | Resume the cruise control after braking   |
| Set          | pure  | Set the current speed as the new cruise speed |
| QuickDecel   | pure  | Decrease the cruise speed                 |
| QuickAccel   | pure  | Increase the cruise speed                 |
| Accel        | float | Accelerator pedal sensor                  |
| Brake        | float | Brake pedal sensor                        |
| Speed        | float | Car speed sensor                          |

## Outputs
The Following outputs have been given
| Signal        | Type         | Description                                                  |
|---------------|--------------|--------------------------------------------------------------|
| CruiseSpeed   | float        | Cruise speed value                                           |
| ThrottleCmd   | float        | Throttle command                                             |
| CruiseState   | enumeration  | State of the cruise control. It can be either OFF, ON, STDBY, or DISABLE |

## Main Module

In our main module, we will be running all three submodules in parallel and mapping all the inputs and outputs as described in the tables above with the ones in the submodules. This approach allows us to run and execute the code synchronously to produce correct results.

For reference, the signals and constants used are defined as follows:

- **Signals:**
  - **CruiseSpeed (float):** Cruise speed value.
  - **ThrottleCmd (float):** Throttle command.
  - **CruiseState (enumeration):** State of the cruise control. It can be either OFF, ON, STDBY, or DISABLE.
  - **On (pure):** Enable the cruise control.
  - **Off (pure):** Disable the cruise control.
  - **Resume (pure):** Resume the cruise control after braking.
  - **Set (pure):** Set the current speed as the new cruise speed.
  - **QuickDecel (pure):** Decrease the cruise speed.
  - **QuickAccel (pure):** Increase the cruise speed.
  - **Accel (float):** Accelerator pedal sensor.
  - **Brake (float):** Brake pedal sensor.
  - **Speed (float):** Car speed sensor.

- **Constants:**
  - **SpeedMin:** 30.0km/h
  - **SpeedMax:** 150.0km/h
  - **SpeedInc:** 2.5km/h
  - **Kp:** 8.113
  - **Ki:** 0.5
  - **ThrottleSatMax:** 45.0%
  - **PedalsMin:** 3.0%

By utilizing the structured approach of running submodules in parallel, we ensure that the cruise control system operates efficiently and effectively.

## FSM Module

The FSM (Finite State Machine) module controls the state transitions of the cruise control system based on various inputs. The states include OFF, ON, STDBY (standby), and DISABLE, with initial state set to OFF. The module continuously loops, emitting the current state at each tick and transitioning states based on input conditions.

### Constants
The following constants are used in the FSM module, defined in the header file:

- `PedalsMin : float`
- `SpeedMin : float`
- `SpeedMax : float`

### Inputs
| Name        | Type  | Description                         |
|-------------|-------|-------------------------------------|
| On_FSM      | pure  | Enable the cruise control           |
| Off_FSM     | pure  | Disable the cruise control          |
| Resume_FSM  | pure  | Resume the cruise control after braking |
| Accel_FSM   | float | Accelerator pedal sensor            |
| Brake_FSM   | float | Brake pedal sensor                  |
| Speed_FSM   | float | Car speed sensor                    |

### Outputs
| Name        | Type    | Description                       |
|-------------|---------|-----------------------------------|
| State_FSM   | integer | State of the cruise control       |

## carDrivingControl Module

The `carDrivingControl` module regulates the throttle of the car based on the current state of the cruise control system. It uses inputs such as accelerator pedal position, cruise speed, current state, and car speed to determine the appropriate throttle output.

### Inputs
| Name               | Type    | Description                       |
|--------------------|---------|-----------------------------------|
| Accel_drive        | float   | Accelerator pedal position        |
| CruiseSpeed_drive  | float   | Desired cruise speed              |
| State_drive        | integer | Current state of the cruise control system |
| Speed_drive        | float   | Current speed of the car          |

### Outputs
| Name               | Type    | Description                       |
|--------------------|---------|-----------------------------------|
| Throttle_drive     | float   | Throttle command                  |

### Function
The module uses a function `regulateThrottle` which is defined in the C file to handle cruise control regulation.
- float regulateThrottle(bool isGoingOn, float cruiseSpeed, float vehicleSpeed)
where isGoingOn defers whether the system is transitioning to the on state, the cruiseSpeed is the current cruiseSpeed of the system and the vehicleSpeed is the current vehicleSpeed

## cruiseSpeedManage Module

The `cruiseSpeedManage` module handles the management of the cruise speed based on inputs such as set, quick acceleration, quick deceleration, current state, and current speed. It ensures the cruise speed is within specified limits and adjusts it accordingly.

### Constants
The following constants are used in the `cruiseSpeedManage` module:

- `SpeedMin : float`
- `SpeedMax : float`
- `SpeedInc : float`

### Inputs
| Name           | Type    | Description                       |
|----------------|---------|-----------------------------------|
| Set_c          | pure    | Set the current speed as the new cruise speed |
| QuickAccel_c   | pure    | Increase the cruise speed         |
| QuickDecel_c   | pure    | Decrease the cruise speed         |
| State_current  | integer | Current state of the cruise control system |
| Speed_current  | float   | Current speed of the car          |

### Outputs
| Name           | Type    | Description                       |
|----------------|---------|-----------------------------------|
| currentSpeed   | float   | Current cruise speed value        |



## How to Run

### If Running on a System with a Linux Extension with UOA

1. First, download the ZIP folder named `group_8.zip` to a directory where you can access it in the future.
2. Once extracted to a location, go to the internet and search [FlexIT](https://flexit.auckland.ac.nz/) and sign in using your university credentials.
3. Open the app **7-Zip**.
4. In 7-Zip, press `F9` to ensure that another panel is open (2 file explorers).
5. Open the **Z** drive on the left-hand side, which corresponds to your computer's disk hard drive, and on the second panel, open the **H** drive, which corresponds to the university's hard drive system.
6. On the left panel, navigate to where you extracted the ZIP file.
7. On the right panel, navigate to a place where you want to extract the contents. I recommend extracting it to the **Documents** folder.
8. Extract the ZIP file to your chosen location.
9. Now open **Ubuntu Linux 20.04**.
10. Once open, click **Files**.
11. Click **Home**, then **Shares**, then **MyHome**, and navigate to the directory where you extracted the ZIP file.
12. Drag and drop the folder into the Linux desktop or **Documents**.
13. Once done, open a new terminal and navigate to the directory using:
    ```bash
    cd "./PATH_TO_YOUR_EXTRACTED_ZIP/Group_8/files"
    ```
14. Once there, type the following commands to run and execute the program in order:
    ```bash
    make cruisecontrol.xes
    ./cruisecontrol.xes
    ```

### If Running on a Linux System

1. First, download the ZIP folder named `group_8.zip` to a directory where you can access it in the future.
2. Open a new terminal and navigate to the path directory using:
    ```bash
    cd "./PATH_TO_YOUR_EXTRACTED_ZIP/Group_8/files"
    ```
3. Once there, type the following commands to run and execute the program in order:
    ```bash
    make cruisecontrol.xes
    ./cruisecontrol.xes
    ```

