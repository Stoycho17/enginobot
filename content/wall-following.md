---
weight: 5
title: Wall Following
---

# Wall Following

## Introducing Wall Following

Wall following is a common technique used in robotics to navigate a mobile robot along the contours of a wall or obstacle. By employing sensors and intelligent algorithms, the robot can detect and maintain a specific distance or alignment with the wall, allowing it to navigate through complex environments while avoiding collisions.

In this project, we will explore the concept of wall following and develop a robot capable of autonomously traversing along walls. The robot will be equipped with sensors, such as ultrasonic, to detect the presence of walls or obstacles in its surroundings. By analyzing the sensor data and implementing control algorithms, the robot will be able to adjust its movements to stay parallel to the wall or maintain a desired distance from it.

The objective of the wall following system is to provide a reliable and efficient means for a robot to explore and navigate indoor environments with the presence of walls. Wall following algorithms find applications in various fields, including robotics research, automated guided vehicles (AGVs), home cleaning robots, and industrial automation.

The implementation of a wall following system typically involves integrating sensor data processing, control algorithms, and motor control to achieve the desired behavior. The robot uses sensor readings to estimate the distance to the wall and calculates the appropriate steering or motor commands to maintain the desired position relative to the wall.

By building a robot capable of following walls, you will unlock various possibilities for applications such as exploration, mapping, surveillance, or even assistance in tasks like room cleaning. With the advancement of sensor technologies and intelligent algorithms, wall following techniques continue to evolve, providing more robust and versatile navigation capabilities to mobile robots.

## Implementing Wall Following

```haskell
#include <NewPing.h>
#include <ginobot.h>

#define TRIGGER_PIN 9    
#define ECHO_PIN 10      

#define MAX_DISTANCE 200      
#define RIGHT_DISTANCE 10 
```

```arduino
NewPing rightSensor(TRIGGER_PIN, ECHO_PIN, MAX_DISTANCE);
Ginobot gbot;

int FRONT_DISTANCE = 150; 
int Move_Speed = 75;
int Turn_Speed = 70;


void setup() {
  Wire.begin();
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  delay(1000);
  
}

void loop() {
  int rightDistance = rightSensor.ping_cm();   
  int frontDistance = gbot.get_distance_front_mm();  

  if (rightDistance <= RIGHT_DISTANCE) {
    turnLeft();
    moveForward();
    turnRight();
  }else if(frontDistance <= FRONT_DISTANCE ){
        turnLeft();
  }else {
    moveForward();
  }
}

void moveForward() {
  gbot.move_forward(Move_Speed);
  delay(500);
}

void turnLeft() {
    gbot.rotate_left(Turn_Speed);
    delay(500);
}

void turnRight(){
    gbot.rotate_right(Turn_Speed);
    delay(500);
}
```

The code begins by including the necessary libraries, which are NewPing for ultrasonic sensor functionality and ginobot for controlling the robot.

Constants are defined to specify the trigger pin (TRIGGER_PIN) and echo pin (ECHO_PIN) connected to the ultrasonic sensor. MAX_DISTANCE represents the maximum distance to measure, and RIGHT_DISTANCE determines the distance threshold for the right side object detection.

An instance of the NewPing class named rightSensor is created, which utilizes the trigger and echo pins defined earlier to control the right-side ultrasonic sensor.

An instance of the Ginobot class named gbot is also created to control the robot.

In the setup() function, Wire communication is initiated, and the trigger pin is set as an output, while the echo pin is set as an input. A delay of 1 second is included.

The main behavior of the robot is implemented in the loop() function.

Inside the loop, the rightDistance variable stores the distance measured by the right ultrasonic sensor using the ping_cm() function provided by the NewPing library. The frontDistance variable stores the distance measured by the front ultrasonic sensor using the get_distance_front_mm() function from the ginobot library.

The code then utilizes conditional statements to determine the appropriate action based on the distance readings:

If an object is detected on the right side (rightDistance is less than or equal to RIGHT_DISTANCE), the robot performs the following sequence: turn left (using the turnLeft() function), move forward (using the moveForward() function), and turn right (using the turnRight() function). These functions control the robot's movements with specified delays between actions.

If an object is detected in front of the robot (frontDistance is less than or equal to FRONT_DISTANCE), the robot turns left (using the turnLeft() function) to avoid the obstacle.

If no obstacles are detected, the robot moves forward (using the moveForward() function).

![wall-folowing](/wall.gif)
