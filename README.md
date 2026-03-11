# Autonomous-Warehouse-Robot-Hardware-

[cite_start]An autonomous mobile robot designed to identify, collect, and restock grocery items on various shelving units within a simulated grocery store environment[cite: 24]. [cite_start]This project was developed as part of the **EGB320 - Mechatronics Design II** course at the **Queensland University of Technology (QUT)**[cite: 1, 2].

![Image of Actual Robot implementation](image-url)
![Image of final CAD Robot](image-url)

---

## 🛠️ Subsystem Spotlight: Item Collection
[cite_start]I was responsible for the research, design, and testing of the **Item Collection Subsystem**, which is divided into lifting and grabbing mechanics[cite: 25, 27, 28].

### 1. Mechanical Design
* [cite_start]**Vertical Scissor Lift:** Selected for its vertical motion, which simplifies software calculations by keeping the robot at a constant distance from shelves regardless of height[cite: 56, 57, 63].
* [cite_start]**Lead Screw Actuation:** Converts the rotational motion of a DC motor into linear displacement[cite: 122]. [cite_start]The added friction acts as a lock, preventing the lift from falling without continuous power[cite: 128].
* [cite_start]**Parallel Rack-and-Pinion Gripper:** Chosen for its mechanical simplicity and ability to ensure even gripping forces on objects of varying shapes[cite: 71, 73].
* [cite_start]**3D Printed Components:** All lifting and gripping components were modeled in Autodesk Fusion 360 and produced via 3D printing through multiple iterations[cite: 176, 177].

### 2. Electronics & Control
* [cite_start]**Actuators:** Utilized **N20 Encoded Gear Motors** for both mechanisms to provide required torque and precise position feedback[cite: 84, 123, 149].
* [cite_start]**Power System:** Powered by a 7.4V nominal voltage battery[cite: 193, 201]. [cite_start]A buck converter regulates 5.1V for the **Raspberry Pi 5**, while an unregulated line supplies the motor driver (H-Bridge)[cite: 195, 202, 203, 206].
* [cite_start]**Communication:** Commands are sent via a serial interface from the Raspberry Pi to the motor controller to regulate motor speed, direction, and position[cite: 210, 212].

### 3. Software Architecture
[cite_start]The system utilizes Python-based functions to communicate with the motor controller via Serial[cite: 216, 217]:
* [cite_start]`lift_level(level)`: Uses positional control to raise the lift to ground level or three specific shelf heights[cite: 216, 358].
* [cite_start]`grip(job)`: Controls the gripper to open, close, or stop[cite: 217, 366].
* [cite_start]**Contact Detection:** For closing, the controller monitors encoder values and grabs the object when the velocity reaches a certain threshold[cite: 218].

---

## 📊 Performance & Validation
[cite_start]The subsystem was verified against functional requirements through experimental testing[cite: 262].

| Parameter | Specification | Result | Status |
| :--- | :--- | :--- | :--- |
| **Vertical Range** | [cite_start]250 mm [cite: 36] | [cite_start]254 mm [cite: 271, 277] | [cite_start]**PASS** [cite: 271]|
| **Payload Capacity** | [cite_start]0.5 kg [cite: 36] | [cite_start]0.15 kg [cite: 284] | [cite_start]**FAIL** [cite: 286]|
| **Angular Tilt** | [cite_start]$<7^{\circ}$ [cite: 36] | [cite_start]$5^{\circ}$ at Max Height [cite: 277] | [cite_start]**PASS** [cite: 316]|
| **Lifting Speed** | [cite_start]3.0 s [cite: 36] | [cite_start]6.13 s (at 0g payload) [cite: 284] | [cite_start]**FAIL** [cite: 287]|

[cite_start]**Key Finding:** Integration testing confirmed the robot maintains stability navigating ramps at Level 1, but loses its center of balance if the collection subsystem is raised higher than Level 1 during movement[cite: 304, 306].

---

## 🚀 Future Improvements
* [cite_start]**Durability:** Replacing 3D-printed joints with metal or ball-bearing pivots to improve precision and reduce friction[cite: 321, 323].
* [cite_start]**Structural Rigidity:** Using laser-cut acrylic for linkages to provide more rigidity than standard plastic[cite: 324].
* [cite_start]**Speed Optimization:** Increasing lifting speed by optimizing the lead screw pitch or using a higher-speed motor[cite: 325].

---

### 📂 Repository Structure
* [cite_start]`/CAD`: Fusion 360 models and linkage drawings[cite: 107, 147, 171].
* [cite_start]`/Code`: Python scripts for serial communication and level control[cite: 339, 393].
* [cite_start]`/Documentation`: Full technical report including power flow and logic diagrams[cite: 201, 244].
