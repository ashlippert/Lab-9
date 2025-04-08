# Lab 8: Take Control - The PID Feedback Controller

**Authors:**

Ashlyn Lippert and Seth Daniel

**Date:**

April 8th, 2025

## Introduction
   In this lab, we implemented a PID (Proportional-Integral-Derivative) feedback control system on an Arduino-based robot to maintain a fixed distance from a wall using an ultrasonic distance sensor. The PID controller continuously calculates the error between a manually defined setpoint and the actual measured distance, and adjusts the robot’s motor output to minimize that error. By tuning the proportional, integral, and derivative gains, we aimed to achieve stable and responsive control of the robot's position. This exercise demonstrated the fundamental principles of feedback control systems, which are widely used in modern engineering applications, and provided hands-on experience with implementing a PID algorithm using the PID_v2 library in Arduino.

## Materials
1. A computer running Arduino IDE and Chrome Browser
2. RedBoard
3. Ultrasonic sensor
4. Two motors
5. Motor driver
6. Battery pack
7. Additional wires

## Assembly Methods
**Objective 1: PID Use**

  To begin the lab, connect the RedBoard to your computer. Mount the ultrasonic sensor on the front of the robot chassis, ensuring it faces forward. Wire the sensor so that VCC is connected to 5V, GND to ground, the TRIG pin to a digital output, and the ECHO pin to a digital input on the Arduino. 
  Next, mount the two DC motors onto the robot chassis and connect them to the outputs of the motor driver. The motor driver inputs should be connected to appropriate digital pins on the RedBoard, and the driver should be powered using the battery pack, with correct connections to power and ground. This circuit is the same as what was used in Lab 6, and the schematic for assembling the motor circuit is provided in Figure 1 below.

  <div align= "center">
<img src= "https://github.com/user-attachments/assets/4b8a9e11-0ed9-4751-8eaf-1036c17608a1" alt "Schematic 1" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 1: Motor circuit schematic from Lab 6. Obtained from (https://learn.sparkfun.com/tutorials/sparkfun-inventors-kit-experiment-guide---
v40/circuit-5b-remote-controlled-robot
 </figcaption>
</div>

<br>

  Once assembled, the RedBoard circuit created using schematic 1 should resemble what is shown in Figure 2 below. The wheels were attached on the underside of the RedBoard with velcro once circuit assembly was complete.

<div align= "center">
<img src="https://github.com/user-attachments/assets/78ab9299-aa88-4f64-b743-5c406f12c0c3"
alt "Motor Circuit" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 2: Constructed motor circuit from Schematic 1. </figcaption>
</div>
<br>

Next, open the Arduino IDE on your computer. Navigate to the Library Manager under Tools > Manage Libraries, search for “PID_v2” by Brett Beauregard, and install the latest version. After installing the library, modify your existing Arduino sketch. First, include the library at the top of your code using #include <PID_v2.h>. 
Then, define the setpoint, measurement, output, and the PID constants Kp, Ki, and Kd as type double. Before the setup() function, create a PID object using the syntax: PID myPID(&measurement, &output, &setpoint, Kp, Ki, Kd, DIRECT);. Inside the setup() function, initialize the PID controller by calling myPID.SetTunings(Kp, Ki, Kd); followed by myPID.SetMode(AUTOMATIC);.

   The code used in Arduino IDE to move the robot can be described in the following Figures 3-6.
   
   <div align= "center">
<img src="https://github.com/user-attachments/assets/5432bbf2-a9d4-493f-873d-907d849bd30d"
alt "Motor Circuit Code 1" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 3: Code to move motor robot (1/4). </figcaption>
</div>
<br>

 <div align= "center">
<img src="https://github.com/user-attachments/assets/7841a3e2-c867-4b7f-969a-fc5d75370728"
alt "Motor Circuit Code 2" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 4: Code to move motor robot (2/4). </figcaption>
</div>
<br>

 <div align= "center">
<img src= "https://github.com/user-attachments/assets/ae639d44-72af-4bbb-b657-c7bf7253dab6"
alt "Motor Circuit Code 3" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 5: Code to move motor robot (3/4). </figcaption>
</div>
<br>

 <div align= "center">
<img src= "https://github.com/user-attachments/assets/1bb0dac8-0711-4df9-8930-344ebeb79c99"
alt "Motor Circuit Code 4" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 6: Code to move motor robot (4/4). </figcaption>
</div>
<br>

**Objective 2: Keep Your Distance**

   To extend your project to full robot control, you will need to integrate the PID output into a motor movement function. Create a function that reads the PID output and maps it to a motor speed using Arduino’s map() function. Apply the resulting speed to the motors using PWM outputs connected through the motor driver.

   Once this mapping is in place, finalize the feedback control loop inside the Arduino loop() function. In each iteration, the robot should read the distance using the ultrasonic sensor, assign this value to the measurement variable, and then call myPID.Compute() to calculate the new motor output. The motor speed and direction are then adjusted based on this output, allowing the robot to actively maintain the desired distance from a wall. For our code, a setpoint distance of 20 cm was used.

<br/>

<div align="center">
<img src="https://github.com/user-attachments/assets/199b9e42-0694-4df0-a40a-2e5e48b77d77" alt="Code 1" width="400">
<br/>
<figcaption style="font-size: 16px; text-align: center;"> Figure 7: Distance mapping code (1/4). </figcaption>
</div> 

<br/>

<div align="center">
<img src="https://github.com/user-attachments/assets/ae54393a-99a1-47d8-9815-6bc306884395" alt="Code 2" width="400">
<br/>
<figcaption style="font-size: 16px; text-align: center;"> Figure 8: Distance mapping code (2/4). </figcaption>
</div> 

<br/>

<div align="center">
<img src="https://github.com/user-attachments/assets/922534c3-29c3-401c-b593-59d313499666" alt="Code 3" width="400">
<br/>
<figcaption style="font-size: 16px; text-align: center;"> Figure 9: Distance mapping code (3/4). </figcaption>
</div> 

<br/>

<div align="center">
<img src="https://github.com/user-attachments/assets/5d798a3b-1c8c-48b0-a1b7-82146c9f7343" alt="Code 4" width="400">
<br/>
<figcaption style="font-size: 16px; text-align: center;"> Figure 9: Distance mapping code (4/4). </figcaption>
</div> 

<br/>

## Test Equipment

1. Computer with Arduino IDE and MIT App Inventor 2
   
## Test Procedures

**Part 1: PID Use**
   
   After uploading the sketch to the Arduino, open the Serial Monitor to verify that the ultrasonic sensor is reading distances correctly. Confirm that the setpoint, measurement, and output values are displayed and responding to changes in distance as expected. As you move an object toward or away from the sensor, observe how the output changes. A larger error should produce a larger output, in line with PID behavior.
   
<br/>
<div align="center">
  <img src="https://github.com/user-attachments/assets/77c86507-5b4c-45c3-88dd-55a6bd3763ff" alt="Serial Monitor" width="400">
      <br/>
  <figcaption style="font-size: 16px; text-align: center;"> Figure 9: Serial monitor output in Arduino IDE for motor movement code. </figcaption>
</div>

<br/>


**Part 2: Keep Your Distance**

   Begin testing your complete system by selecting a target distance and placing the robot in front of a wall. Power on the robot and observe its behavior as it attempts to maintain the set distance. The robot should move forward if it is too far from the wall and backward if it is too close.

Once basic movement is confirmed, start tuning the PID parameters. Begin with a small proportional gain (Kp) and gradually increase it until the robot starts to respond meaningfully to distance changes. Then introduce a small integral gain (Ki) to reduce steady-state error. Finally, add derivative gain (Kd) to dampen oscillations and improve system stability. After each change, observe how the robot’s movement adjusts and record the behavior. The final modified code values are shown in the Test Results Section Below.
On top of modifying the Ki, Kp, and Kd values, the minimum and maximum speeds were adjusted. It was noted that the motor car performed better at lower speeds.

## Test Results:

**Table 1: Testing Different Ki, Kp, and Kd Values**

|  Ki  |  Kp  |  Kd  |       Comments     |
|------|------|------|--------------------|
| 0.5  | 1    | 0.1  | Starting values    |
| 0.5  | 2    | 0.1  | More stopping?     |
| 0.5  | 0.5  | 0.1  | Scooted backwards  |
| 1    | 1    | 0.1  | Skipping movements |
| 1    | 2    | 0.1  | Less randomized?   |
| 1    | 2    | 0.5  | Better             |
| 4    | 0.1  | 0.3  | Best               |

**Modified Code for Kp Ki, and Kd Adjustments**

 <div align= "center">
<img src="https://github.com/user-attachments/assets/ed213957-0b12-46f5-b496-b394eb1cf92c"
alt "Modified Code" width="400"/>
<br>
<figcaption style="font-size: 16px; text-align: center;"> Figure 10: Modified code from Part 2 with adjusted Kp, Ki, and Kd. </figcaption>
</div>
<br>


## Discussion:



## Conclusion:
