# Malicious Agents in Robot Swarms
## Project Summary
Swarm robotics represents a rapidly growing field of study that leverages the collective behavior of multiple robots to achieve complex tasks that would be difficult or impossible for a single robot to accomplish. While the potential applications of swarm robotics are vast and transformative, from industrial automation to search-and-rescue operations, the increasing complexity of these systems also introduces new vulnerabilities. This project, titled "Malicious Agents in Robot Swarms," delves into the critical security challenges that arise when dealing with robot swarms, specifically focusing on the identification, analysis, and mitigation of malicious behaviors within these systems.

## Table of Contents
1. [Motivation](#motivation)
2. [Project Details](#project-details)
   - [Technologies Used](#technologies-used)
   - [Behaviour Algorithms](#behaviour-algorithms)
3. [Limitations](#limitations)
4. [Future Scope](#future-scope)
5. [Conclusion](#conclusion)

## Motivation
The motivation for this project stems from the inherent tension between technological innovation and security. As we push the boundaries of what is possible with swarm robotics, we must also anticipate and address the potential risks that come with these advancements. Without proper security measures, even the most sophisticated systems can become vulnerable to exploitation, leading to inefficiencies, system failures, or worse, malicious takeovers.

### Technological Impact
Swarm robotics has the potential to revolutionize numerous industries by offering scalable, adaptable, and resilient solutions. However, the same complexity that allows these systems to function autonomously also makes them susceptible to security threats. Understanding and mitigating these risks is not just a technical challenge but a moral and societal imperative, as the misuse of robotic swarms could have far-reaching consequences.

### Ethical Considerations
In addition to the technical challenges, this project also addresses the ethical implications of deploying swarm robotics in environments where they might interact with humans. The potential for malicious agents to disrupt or corrupt the behavior of a swarm poses significant ethical concerns, particularly when these systems are used in critical applications such as healthcare, defense, or disaster response.

### The Need for Security
As with any advanced technology, the security of swarm robotics cannot be an afterthought. This project seeks to emphasize the importance of building security into the core of swarm robotic systems, ensuring that they are robust enough to withstand potential threats. By analyzing how these systems can be compromised, this project aims to develop strategies that will protect them from malicious actors, thereby safeguarding their potential to contribute positively to society.

## Project Details
### Technologies Used
The experimental setup for this project includes several key components that work together to simulate and analyze the behavior of robot swarms in a controlled environment. Below is a detailed description of each component:

- **Swarm Robots:**
This project uses 10 MONA robots, which are specifically designed for swarm robotics research. Each MONA robot is built on an ESP 32 microcontroller platform and adheres to open-source and open-hardware principles. These robots are small, circular devices with a diameter of 80mm, equipped with two wheels for movement, powered by DC motors. They feature 5 IR transmitter-receivers on their front side, enabling them to detect their surroundings and interact with other robots in the swarm.

Key features of the MONA robots include:

Type 2 Charging Port: Facilitates easy charging using standard Type 2 cables.<br />
Wi-Fi Connectivity: Allows robots to communicate wirelessly within the network.<br />
Battery Life: Each robot has a battery life ranging from 2 to 8 hours, depending on usage.<br />
Energy Efficiency: The ESP32 microcontroller is designed to operate in energy-saving mode, waking up at regular intervals to minimize power consumption.

- **Arena:**
The experiment is conducted within a well-defined arena, measuring 1.92m x 1.08m. This confined space is carefully selected to create a controlled environment where the robots can perform their tasks without external interference. The arena's dimensions are chosen to ensure that the robots remain within the observation area, reducing the risk of accidents and unnecessary interactions with external factors.

- **ArUco Tags:**
ArUco markers are synthetic square markers with unique patterns that allow them to be recognized by cameras. In this experiment, ArUco tags are strategically placed in the arena to assist with the localization and tracking of robots. Each robot is equipped with an ArUco tag on top, enabling the camera to identify and track their positions within the arena.

- **Web Camera:**
A Brio webcam with 1080p resolution is mounted above the arena to capture a comprehensive view of the robots and their interactions. This camera is critical for monitoring the experiment and collecting data. The Brio webcam is capable of recording in 4K Ultra HD, providing high-quality video that is essential for accurate analysis.

- **Client System:**
The client system serves as the command interface, allowing the operator to interact with the swarm. It sends commands to the robots and receives feedback, which is then logged for further analysis. The client system is responsible for implementing the control logic that governs the robots' behavior, particularly their color-changing behavior, which is central to this experiment.

- **Server System:**
The central server acts as the communication hub for the swarm. It aggregates data from the robots, the webcam, and the client system, executing commands as needed. The server is responsible for updating the user interface and relaying information between the client system and the swarm, ensuring smooth and coordinated operation.

- **JSON Packets:**
JSON (JavaScript Object Notation) packets are used to structure the data exchanged between different components of the system. These packets facilitate communication between the robots, the client system, and the server, ensuring that commands and data are transmitted in a standardized format.

### Behaviour Algorithms
The behavior of the robots in this experiment is governed by two primary algorithms: one for normal behavior and another for malicious behavior. These algorithms dictate how the robots interact with each other and respond to different conditions within the swarm.

- **Normal Behaviour:**
Initialization: The sendCommands function is initiated, setting robot.redCount and robot.blueCount to 0, along with initializing neighRed and neighBlue.<br />
Neighbor Interaction: For each neighboring robot, the algorithm checks its color and updates the robot's red and blue counts accordingly.<br />
Time-Based Decision Making: The algorithm checks if the current time minus the robot's last color change time exceeds a threshold. If so, it updates the robot's color based on the cumulative red and blue counts.<br />
Data Logging: The robot's data, including its new color, is saved to a CSV file for analysis.<br />
Command Execution: The robot's LED color and motor speeds are updated based on the new color, and a command message is sent to the robot.

- **Malicious Behaviour:**
Initialization: Variables are initialized, including a list of potentially malicious robot IDs (mal_robot) and a victim ID.<br />
Neighbor Interaction: The algorithm checks the colors of neighboring robots and identifies potential victims if their IDs are in the malicious list.<br />
Victim Manipulation: If the robot is identified as a victim, its red and blue counts are set to 0.<br />
Color Change Logic: The algorithm decides whether to change the robot's color based on elapsed time. If the robot is a victim, the color change logic is reversed, leading to potentially disruptive behavior in the swarm.<br />
Data Logging and Command Execution: Similar to the normal behavior algorithm, the robot's data is saved, and its LED color and motor speeds are updated based on the new color.

### Limitations
While this project provides valuable insights into the behavior of robot swarms and the impact of malicious agents, there are several limitations to the current experimental setup:

- **Lack of Advanced Security Measures**
One of the primary limitations is the absence of advanced security protocols, such as encryption, authentication, and authorization. In real-world applications, these measures are essential to prevent unauthorized access and ensure the integrity of the swarm. The experiment is conducted in a local network with basic security, which does not fully represent the challenges faced in more complex environments.

- **Limited Network Security**
The network used in this experiment has a basic layer of security, which is not sufficient to protect against sophisticated cyber-attacks. In real-world deployments, multiple layers of security are typically employed to safeguard the network and prevent malicious intrusions.

- **No Access Control Mechanisms**
The experiment lacks access control mechanisms, such as password checks or credential verification, which are commonly used in real-world systems to restrict participation in the swarm to authenticated robots. This presents a potential vulnerability, as it allows any robot to join the swarm without verification.

### Future Scope
The study of malicious agents in robot swarms opens up numerous avenues for future research and development. Below are some potential directions in which this work can be extended:

- **Enhanced Malicious Detection Algorithms**
Developing more sophisticated algorithms for detecting malicious behavior within a swarm is crucial. Machine learning techniques could be employed to analyze patterns of normal and abnormal behavior, enabling the system to identify potential threats more accurately and swiftly. These algorithms could be designed to adapt over time, learning from new threats and improving their detection capabilities.

- **Autonomous Defense Mechanisms**
Future work could explore the development of autonomous defense mechanisms that allow the swarm to detect, isolate, and neutralize malicious agents in real time. This could involve creating self-healing systems where robots can reconfigure themselves to maintain overall swarm functionality, even when some members are compromised.

- **Scalability and Large-Scale Swarm Systems**
As swarm robotics moves from research labs to real-world applications, the ability to scale up these systems will become increasingly important. Future research could focus on managing larger swarms effectively, ensuring that the algorithms and security measures developed in this project can be applied to swarms of hundreds or thousands of robots.

- **Cross-Swarm Interaction and Secure Communication**
In the future, multiple swarms may need to interact and cooperate on complex tasks. Ensuring secure communication between different swarms will be a critical area of research. This could involve developing protocols that allow swarms to exchange information securely, verify the authenticity of other swarms, and collaborate on tasks while safeguarding against potential threats.

### Conclusion
This project represents a foundational step in understanding and addressing the security challenges associated with swarm robotics. By investigating the behavior of malicious agents within a swarm, we have gained valuable insights into the potential vulnerabilities of these systems and the steps that can be taken to mitigate these risks. While the current work is primarily exploratory, it sets the stage for future research and development aimed at creating robust, secure, and scalable swarm robotic systems that can be deployed in a wide range of real-world applications.
