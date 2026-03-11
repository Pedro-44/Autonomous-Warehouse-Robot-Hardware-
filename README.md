# Autonomous Warehouse Restocking Robot (TRL 3 Prototype)

An autonomous mobile robot designed to identify, collect, and restock grocery items on various shelving units within a simulated grocery store environment. This project was developed as part of the **EGB320 - Mechatronics Design II** course at the **Queensland University of Technology (QUT)**.

<img src="https://github.com/Pedro-44/Autonomous-Warehouse-Robot-Hardware-/blob/66faf588fa44a66bec917b1ae86ca404fd2776f5/Screenshot%202026-03-11%20145050.png" width="50%" />
<img src="https://github.com/Pedro-44/Autonomous-Warehouse-Robot-Hardware-/blob/500a91816e0aaa42c58955c7f26537e390e303da/Screenshot%202025-10-28%20151323.png" width="50%" />
---

## 🛠️ Subsystem Spotlight: Item Collection
I was responsible for the research, design, and testing of the **Item Collection Subsystem**, which is divided into lifting and grabbing mechanics.

### 1. Mechanical Design
* **Vertical Scissor Lift:** Selected for its vertical motion, which simplifies software calculations by keeping the robot at a constant distance from shelves regardless of height.
* **Lead Screw Actuation:** Converts the rotational motion of a DC motor into linear displacement. The added friction acts as a lock, preventing the lift from falling without continuous power.
* **Parallel Rack-and-Pinion Gripper:** Chosen for its mechanical simplicity and ability to ensure even gripping forces on objects of varying shapes.
* **3D Printed Components:** All lifting and gripping components were modeled in Autodesk Fusion 360 and produced via 3D printing through multiple iterations.

<img src="https://github.com/Pedro-44/Autonomous-Warehouse-Robot-Hardware-/blob/500a91816e0aaa42c58955c7f26537e390e303da/Screenshot%202026-03-11%20145121.png" width="90%" />



### 2. Electronics & Control
* **Actuators:** Utilized **N20 Encoded Gear Motors** for both mechanisms to provide required torque and precise position feedback.
* **Power System:** Powered by a 7.4V nominal voltage battery. A buck converter regulates 5.1V for the **Raspberry Pi 5**, while an unregulated line supplies the motor driver (H-Bridge).
* **Communication:** Commands are sent via a serial interface from the Raspberry Pi to the motor controller to regulate motor speed, direction, and position.



### 3. Software Architecture
The system utilizes Python-based functions to communicate with the motor controller via Serial:
* `lift_level(level)`: Uses positional control to raise the lift to ground level or three specific shelf heights.
* `grip(job)`: Controls the gripper to open, close, or stop.
* **Contact Detection:** For closing, the controller monitors encoder values and grabs the object when the velocity reaches a certain threshold.

---

## 📊 Performance & Validation
The subsystem was verified against functional requirements through experimental testing.

| Parameter | Specification | Result | Status |
| :--- | :--- | :--- | :--- |
| **Vertical Range** | 250 mm | 254 mm | **PASS** |
| **Payload Capacity** | 0.5 kg | 0.15 kg | **FAIL** |
| **Angular Tilt** | < 7° | 5° at Max Height | **PASS** |
| **Lifting Speed** | 3.0 s | 6.13 s (at 0g payload) | **FAIL** |

**Key Finding:** Integration testing confirmed the robot maintains stability navigating ramps at Level 1, but loses its center of balance if the collection subsystem is raised higher than Level 1 during movement.

---

## 🚀 Future Improvements
* **Durability:** Replacing 3D-printed joints with metal or ball-bearing pivots to improve precision and reduce friction.
* **Structural Rigidity:** Using laser-cut acrylic for linkages to provide more rigidity than standard plastic.
* **Speed Optimization:** Increasing lifting speed by optimizing the lead screw pitch or using a higher-speed motor.

---

### 📂 Repository Structure
* `/CAD`: Fusion 360 models and linkage drawings.
* `/Code`: Python scripts for serial communication and level control.
* `/Documentation`: Full technical report including power flow and logic diagrams.
