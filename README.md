# Simple-Virtual-Motor-Simulation
A simulation of a simple motor programmed in PLC Siemens through UDTs (User Defined Data Types) that can be exposed and viewed 'online' in OPC UA.

This project can only be viewed via TIA Portal Siemens V20 and it is configured for the PLC Siemens S7-1214C. 
In the following images i will show the primitive variables i used for testing the project, the structure for the Motor UDT, Motor UDT variables and other configurations.

## Project Screenshots

### PLC Tags

Here is a screenshot of the variables used for the basic raw inputs utilized. This means switches, LEDs and a simple potentiometer that was scaled to fit in the range of 0 to 100. 

<img width="907" height="388" alt="Screenshot 2026-01-09 133218" src="https://github.com/user-attachments/assets/6d1c2ccf-90fd-4a61-97c2-088278a1af1e" />

### UDT

Here is a screenshot of the variables that are used inside of an UDT instance. It has basic breakdowns simulations, variables for the speed of the motor that can be set through the potentiometer, and a few states for the motor to toggle through.

<img width="848" height="317" alt="Screenshot 2026-01-09 133230" src="https://github.com/user-attachments/assets/f550f237-28be-4ae9-8939-406a0fd03905" />

Next picture shows the instances of the UDT, that can be used for multiple motors at the same time. My project has been made with only one in mind, but can be extended to multiple motors through this UDT. 

<img width="930" height="396" alt="Screenshot 2026-01-09 133243" src="https://github.com/user-attachments/assets/fe3bf473-df1f-4ac2-8c33-e0d10a40be0c" />

### Implementation in Networks

The next series of images show the code implemented in LADDER in the first network, and the rest of the code written in Structured Text in the second network. The simulation consists of:
* A switch that represents the 'start / stop' button of the motor. When the switch is toggled to 'off', none of the motor's functionalities work.
* Raw inputs from a potentiometer, that have been scaled to a range from 0 to 100, that represent the speed that the motor can be set to. When the potentiometer is set to 0, the motor is 'idle' and when it is set to 100, the motor is set to full speed.
* Two switches that simulate the activation of a certain breakdown, one for exceeding limits for temperature and one for exceeding limits for drawn current.
* Activation of multiple LED's to indicate the current state of the motor or the presence of any breakdowns.

Here are pictures of the code implemented in LADDER.

<img width="1342" height="844" alt="Screenshot 2026-01-09 133403" src="https://github.com/user-attachments/assets/4d1de6b3-419e-45a7-a7e8-2afeaf3d8d2d" />
<img width="899" height="608" alt="Screenshot 2026-01-09 133417" src="https://github.com/user-attachments/assets/b5a1ad6a-ade3-4e20-bd83-76138142b275" />

And finally the next picture shows the piece of code written in Structured Text, in which i programmed 3 LED's to activate when the motor is set to the speed of their corresponding state: one between the values of 50 to 75, one for values between 75 and 98 and one for max speed when the values are between 98 and 100. When the motor is switched off or when a breakdown appears, none of the LEDs light up. The code for the breakdowns is also implemented here, which consist of the binary variables 'words', that are used to determine the general variable 'Avarie' (breakdown) through a simple binary equation: 1 | (1 << 2). This way there are formed 3 more states for the motor, when there are 1, 2, or no breakdowns. The corresponding LEDs also light up for each breakdown.

<img width="1097" height="369" alt="Screenshot 2026-01-09 133425" src="https://github.com/user-attachments/assets/5b2cf899-3e91-4527-82fe-eb79a1d4af99" />

