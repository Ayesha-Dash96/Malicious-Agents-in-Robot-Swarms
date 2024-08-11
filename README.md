# Malicious-Agents-in-Robot-Swarms
This project explores the world of swarm robotics system, concentrating on the possible dangers and vulnerabilities that they may be susceptible to. Swarm robotics is an expanding field and offers numerous opportunities for its implementation in many industries. Nevertheless, as these frameworks become more sophisticated, their vulnerability to malicious misuse increases. This project seeks to identify and analyse the hostile behaviour in robot swarms and come up with measures to protect them from potential threats.

## Motivation
The motivation behind this project comes from the dynamic relationship between innovation and security. Adapting innovation without implementing the necessary security measures makes an inefficient system. It is fascinating to realise that the technology that gives rise to more and more complex and advanced systems, is also the reason for the ongoing threats in them. In addition to the technical aspects, this study aims to emphasise the moral, financial, and societal factors linked to harmful individuals in groups of robots. In order to develop a defence strategy, it is important to first analyse how the swarm robots behave and how it can be misused. It is essential to realise the impact of such threats on the performance of the individual members in the swarm. The reason behind this project is to state the potential of swarm robots and to address the security issues that threaten to compromise the potential of such systems.

## Project Details
**Technologies Used**: The system consists of swarm robots, a web camera, a central server and a client system. These components are explained in detail below-
  - _Swarm robots_- This experiment uses 10 swarm robots which are Mona robots, made of ESP 32 microcontrollers. The MONA robot platform, a structure built on open-source and open hardware principles, is crafted specifically for swarm robotics analyses. It's designed to tackle research areas that include infinite swarms, multi-agent coordination as well as the interaction or handling between human beings and an entire fleet of robotic structures (23). MONA robots are small and circular in size. They are 80mm in diameter and consist of 2 wheels that help them in movement if needed. It is built with two DC motors as well as 5 IR transmitter receivers that are placed in the front section of the robot. These robots are equipped with type
  2 charging port that facilitates its charging using any type 2 cables. It has the ability to connect with wifi and communicate in the network. The battery life of this robot is 2-8 hours. The MONA robots used for this experiment have ESP32 embedded in it. ESP 32 is always in energy saving mode and needs to be woken up in regular intervals. This helps in minimising the energy consumption of ESP32. 
  - _Arena_- The experiment is done in a well-defined arena measuring 1.92m x1.08m in dimensions. The arena serves as a physical space in which swarm robots do their tasks. This dimension is carefully chosen to create a controlled environment in which the experiments can be conducted. This confined space reduces the risk of swarm robots going beyond the observation area and reduces minor accidents and unnecessary interactions with the external factors. Also, it sets a boundary for the swarm, helping them to interact with each other if needed effectively within a small zone.
  - _ArUco tags_- ArUco marker is a synthetic square marker that has been designed with a distinct pattern which helps it get recognised by the web camera. They are used for location and tracking of objects. They are placed in precise positions in the arena for the camera to detect the dimension of the arena. It is also used on top of all the swarm robots for the camera to detect them. The placement of the ArUco tags in the arena helps in calculating the area of the whole arena.
  - _Web camera_- For this experiment, webcams are placed at the top of the arena to get a clear view of the swarm robots as well as the area of the experiment. This webcam has a resolution of 1080p and can cover the entire area of the arena. It acts as an essential detector for capturing and analysing data from the swarm robots. The web camera used is Brio which has excellent video quality. The resolution of the web camera is 4K Ultra HD and the video mode delivered is 1080p. This matches with the size of the arena. The web camera is mounted on top of the frame of the arena and is stationary.
  - _Client system_- In this experiment, the client system plays an important role in forming a bridge between the operator and the robot swarms. The client system acts as a command interface which allows the operator to interact with the swarm robots by sending the desired commands. It also receives feedback from the robots and keeps a log of the essential data. Client system is primarily responsible for implementing the control logic of the colour change. After it receives values from server and robot, it implements the algorithm and sends the updated values back to the server system Server system- The central server is one of the main components of the system as it aggregates all the data received from the sensors, web camera
  as well as the client systems to execute a set of actions. It either updates the user interface or sends the requested data back to the client system. In this way, it acts as a communication hub of the swarm system.
  - _Json packets_-JSON packets are structured data formats that are used to send information to different parts of a system. In this experiment JSON packets have been used as a part of communication between robots and the client and between the client and the server system.

**Behaviour algorithms:**
Normal behaviour 
      1. Start the `sendCommands` function.
      2. Initialize `robot.redCount` and `robot.blueCount` to 0, and also initialise `neighRed` and `neighBlue` to 0.
      3. For each neighbour in the robot's list of neighbours, do the following:
          - If the neighbour's ID is not equal to the robot's ID, do the following:
          - If the neighbour's colour is "red," increment `robot.redCount` by 1 and add the neighbour's `redCount` to `neighRed`.
          - If the neighbour's colour is "blue," increment `robot.blueCount` by 1 and add the neighbour's `blueCount` to `neighBlue`.
      4. Check if the difference between the current time and `robot.colourTime` is greater than 3 plus a random number.
      5. If the condition in step 4 is true, update `robot.colourTime` with the current time.
      6. Determine the robot's new colour based on the following rules:
          - If the sum of `robot.redCount` and `neighRed` is equal to the sum of `robot.blueCount` and `neighBlue`, keep the robot's current colour.
          - If the sum of `robot.redCount` and `neighRed` is greater than the sum of `robot.blueCount` and `neighBlue`, set the robot's colour to "red."
          - Otherwise, set the robot's colour to "blue."
      7. Save the robot's data to a CSV file.
      9. Set the LED colour of the robot to its new colour (`robot.colour`).
      11. Send a command message to the robot's connection with the LED colour and motor speeds which is 0.
      12. End the function.
  Malicious behaviour
      1. Initialize Variables:
          - `mal_robot`: List of robot IDs considered potentially malicious.
          - `victim`: ID of a robot that may become a victim.
      2. For Each neighbouring Robot:
          - Check if it's not the current robot.
          - If the neighbour is red, increment the count of red neighbours.
          - If the neighbour is blue, increment the count of blue neighbours.
          - If the neighbour's ID is in the `mal_robot` list, set it as the `victim`.
      3. If the robot's ID is that of victim, set its blue count and red count to 0
      4. Check for colour Change:
          - Determine if it's time to change the robot's colour based on elapsed time since last change.
          - If it's time for a colour change:
              - If the robot is not the victim and not in the malicious list:
                  i. If the counts of red and blue neighbours are equal, keep the current colour.
                  ii. If there are more red neighbours than blue, switch the robot's colour to red.
                  iii. Otherwise, switch the robot's colour to blue.
              - If the robot is the victim:
                  i. Follow the same logic as above but reverse the colours.
      4. Save Data: Save the robot's data (including its colour and relevant information) to a CSV file.
      5. Report neighbour Counts: Print the current counts of red and blue neighbours for monitoring.
      6. Prepare Command Message: Create a message specifying the robot's LED colour and motor speeds based on the updated colour.
      7. Send Command: Send the command message to the robot to adjust its LED colour and motor speeds accordingly.
      8. Handle Errors: If any exceptions occur during execution, handle them and print error messages for troubleshooting.
  
- **Limitations:**
Below are the various limitations that are observed in the current Swarm hack model used for the experiment-
  a) One prominent limitation is that it lacks any advanced security measures which is commonly found in real-world applications. In practice, the swarm systems are deployed in target locations along with all the necessary security protocols to avoid any disruptions. Some of these security measures are encryption of messages, authentication, authorisation, password checks to prevent any malicious intrusions.
  b) The experiment is conducted in local network with a basic layer of network security which is not the case in real world as there are multiple layers of security placed in the network to avoid any sort of cyber-attack.
  c) Maintaining password checks and access control mechanisms enhance the security of the systems so that only authenticated robots with correct credentials are allowed to take part in the swarm activities. This presents any malicious robot to enter the system.

- **Future Scope **
The project on malicious agents in robot swarms opens up various avenues for future research and development. Below are some potential directions in which this work can be extended:

_Enhanced Malicious Detection Algorithms:_ Developing sophisticated algorithms for detecting malicious behavior within a swarm is crucial. Machine learning techniques could be employed to analyze patterns of normal and abnormal behavior in the swarm, helping to identify potential threats more accurately and swiftly. These algorithms could be designed to adapt over time, learning from new threats and improving their detection capabilities.
_Autonomous Defense Mechanisms:_Future work could explore the development of autonomous defense mechanisms that allow the swarm to detect, isolate, and neutralize malicious agents in real-time. This could involve creating self-healing systems where robots can reconfigure themselves to maintain overall swarm functionality even when some members are compromised.
_Scalability and Large-Scale Swarm Systems:_ Expanding the system to manage larger swarms is a significant future direction. Research can focus on the scalability of both the security measures and the swarm algorithms to ensure they remain effective as the number of robots in the swarm increases. This also involves optimizing the communication protocols and network infrastructure to support large-scale operations.
_Cross-Swarm Interaction and Coordination:_ Investigating how different swarms can interact and coordinate with each other, especially in scenarios where multiple swarms with different objectives operate in the same environment, presents a challenging and interesting research direction. Ensuring secure and efficient cross-swarm communication while preventing malicious interference is key.
