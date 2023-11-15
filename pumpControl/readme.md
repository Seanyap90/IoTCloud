<h1>Cloud based control panel application for pump control</h1>

<h2>Demonstration</h2>

https://github.com/Seanyap90/IoTCloud/assets/34641712/24fc0a9d-244b-48d3-9cc9-0e0cd21322bc

This demo simulates an industrial sampling operation where a tank is used to take liquid samples, so pumps are utilised to assist in the extraction of samples from main operational tanks.  Sampling operations can either be left automated or be conducted by a user on his own.

<h2>Use Cases and Constraints</h2>

<h3>Use cases</h3>

- User can control the pump through toggling a series of buttons
   - User can leave the pump operating automatically by pressing "Auto"
   - User can stop the pump operation by pressing "Stop"
   - User can decide how long the pump operates for by entering an integer after pressing "manual".  During the operation (sampling count), the user is not allowed to toggle
   - Once the intended manual operation is over, the user has to press "manual" if he decides to operate the pump on his own again
- User can view the real time volume of the tank
- Service extracts user actions and accordingly dispatches commands to start or stop the pump

<h3>Constraints and assumptions</h3>

<p>Assumptions</p>

- Infrequent usage
- User access purpose is usually to view tank levels and operation status
- Remote access
- (future) Control of multiple pumps at multiple sites

<h2>High level System Design</h2>

![CloudArchitectureForIoT1](https://github.com/Seanyap90/IoTCloud/assets/34641712/7447e16a-78da-4359-a8e4-6f82c170c83d)

<h2>Relevant applications</h2>

- Oil and gas
- Water quality monitoring, especially for taking contaminated samples
- Hydroponics
