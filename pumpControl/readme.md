<h1>Cloud based control panel application for pump control</h1>

<h2>Demonstration</h2>

https://github.com/Seanyap90/IoTCloud/assets/34641712/a61084d2-1336-40a2-8309-f420b96ab983

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

![CloudArchitectureForIoT1](https://github.com/Seanyap90/IoTCloud/assets/34641712/f0b85f3a-7c2d-43d8-b2aa-5ffb8aa03b07)

<h3>System Design Details</h3>

<p>A bash application is launched on a raspberry pi to simulate a pump.  The simulated pump publishes operational status whil receving user driven commands after user toggles between buttons and add sampling input under manual mode.  The initiation of these actions are done via pub sub mechanisms.</p>

<h3>Cloud infrastructure High Level Details</h3>

- IoT Core
  - Pub/sub MQTT topics in form of pump/<device-id>*/<operation>
  - Operation refers to mode, change and count
  - Use AWS IoT Rules to route messages from pump/<device-id>*/# or specific topics
- Lambda functions (coded in nodejs)
  - 1 nodejs function to connect to Websockets from API gateway
  - 1 nodejs function for filtering between messages from IoT Core and updating database accordingly
  - 1 nodejs function for sending updates to client upon update of database
  - 1 nodejs function for receiving messages from client through Websockets and posting to MQTT topic subscribed by simulated device
- Database
  - 1 partition key used
  - It will store mode status.  Any change will trigger the lambda function to send updates to client
- Websocket configuration under API Gateway
  - Map $connect route to lambda function that enables connection to Websocket
  - Map $default to lambda function receiving messages from client, updating of database and posting to MQTT topic.  Ensure that the path is bidirectional
  - Map a custom route to lambda function enabling updates to database

<h2>Relevant applications</h2>

- Oil and gas
- Water quality monitoring, especially for taking contaminated samples
- Hydroponics
