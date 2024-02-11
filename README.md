# Traffic Lights: Pedestrian Priority

*The problem:*

The traffic light positioned at the intersection of BR-110 and the UFERSA Campus exits in Mossoró is depicted in Figure 01. Sensors are strategically placed at exits A and B of the Campus and along lanes C and D of BR-110. The outputs of sensors A and B assume a low level (0) when there is no detection of a pedestrian and a high level (1) when a pedestrian is detected. The outputs of sensors C and D assume a low level (0) when there is no detection of a vehicle and a high level (1) when a vehicle is detected.

The logic for controlling the vehicle traffic light is as follows:

1. The traffic light in the North-South direction activates the green light if lanes C and D are occupied.
2. The traffic light in the North-South direction activates the green light if lanes C or D are occupied and outputs A and B are not occupied.
3. The traffic light in the East-West direction activates the green light if exits A and B are occupied and lanes C and D are not occupied.
4. The traffic light in the East-West direction activates the green light if exits A or B are occupied and lanes C and D are not occupied.
5. The traffic light in the East-West direction activates the green light if exits A and B and lanes C and D are not busy.

The design of the circuit should use the outputs of sensors A, B, C, and D as inputs to control the traffic light for vehicles. It is essential to ensure that the conditions prioritize safety and do not expose pedestrians to risky scenarios. The project should not deviate from these expectations, and any modifications should aim to enhance pedestrian crossings. The traffic light outputs must be high to activate a red light and low to activate a green light in each direction. The circuit should be simplified as much as possible.

*Resolution:*

Conditions:
A and B - Pedestrian Crossing:
  0 - No pedestrian - Vehicle signal red
  1 - With pedestrian

C and D - Vehicle Lane:
  0 - No vehicle - Pedestrian signal red
  1 - With vehicle

(P) Prioritize pedestrians

Green_NS:
- (1) The traffic light in the North-South direction must activate the green light if lanes C and D are occupied:
  
  (CD) = 1 - (C=1 D=1)

- (2) The traffic light in the North-South direction must activate the green light if lanes C or D are occupied, and exits A and B are not occupied:
  
  (C+D)(AB) = 1 - (C=1 D=1 A=0 B=0)

Green_EW (LO in PT-BR):
- (3) The traffic light in the East-West direction must activate the green light if exits A and B are occupied, and lanes C and D are not occupied:
  
  (AB)(CD) = 1 - (A=1 B=1 C=0 D=0)

- (4) The traffic light in the East-West direction must activate the green light if exits A or B are occupied, and lanes C and D are not occupied:
  
  (A+B)(CD) = 1 - (A=1 B=1 C=0 D=0)

- (5) The traffic light in the East-West direction must activate the green light if exits A and B, as well as lanes C and D, are not occupied:
  
  (AB)(CD) = 1 - (A=0 B=0 C=0 D=0)


*Truth Table*

| A | B | C | D | V_NS | V_EW |
|---|---|---|---|------|------|
| 0 | 0 | 0 | 0 |  0   |  1(5)|
| 0 | 0 | 0 | 1 |  1(2)|  0   |
| 0 | 0 | 1 | 0 |  1(2)|  0   |
| 0 | 0 | 1 | 1 |  1(1)|  0   |
| 0 | 1 | 0 | 0 |  0   |  1(4)|
| 0 | 1 | 0 | 1 |  0   |  1(P)|
| 0 | 1 | 1 | 0 |  0   |  1(P)|
| 0 | 1 | 1 | 1 |  0   |  1(P)|
| 1 | 0 | 0 | 0 |  0   |  1(4)|
| 1 | 0 | 0 | 1 |  0   |  1(P)|
| 1 | 0 | 1 | 0 |  0   |  1(P)|
| 1 | 0 | 1 | 1 |  0   |  1(P)|
| 1 | 1 | 0 | 0 |  0   |  1(3)|
| 1 | 1 | 0 | 1 |  0   |  1(P)|
| 1 | 1 | 1 | 0 |  0   |  1(P)|
| 1 | 1 | 1 | 1 |  0   |  1(P)|

*Consider*:

1, 2, 3, 4, and 5 - Conditions

P - Pedestrian Priority

1 - Green signal for the respective lane

0 - Red signal for the respective lane

*Equations:*

V_NS: (A'B'C'D)+(A'B'CD')+(A'B'CD)

![image](https://github.com/lucasvinasl/traffic_lights_pedestrian_vehicles/assets/74206824/f31499dc-af38-4435-8a31-54f2c9c5b307)


V_EW: (A'B'C'D')+(A'BC'D')+(A'BC'D)+(A'BCD')+(A'BCD)+(AB'C'D')+(AB'C'D)+(AB'CD')+(AB'CD)+(ABC'D')+(ABC'D)+(ABCD')+(ABCD)

![image](https://github.com/lucasvinasl/traffic_lights_pedestrian_vehicles/assets/74206824/280b7311-5cc9-40b3-b7dc-641beebe9a03)

*Circuit Simulation in ThinkerCad*

Avaiable in:

https://www.tinkercad.com/things/duorzueiRSZ-semaforoufersa

![image](https://github.com/lucasvinasl/traffic_lights_pedestrian_vehicles/assets/74206824/b70e2964-92f1-486a-8c41-7b9a3e06c8b0)
