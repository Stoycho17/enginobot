---
weight: 3
title: Line Following
---

# Line Following

## Introducing Line Following

Line following robots are autonomous vehicles designed to navigate along a predefined path or track by detecting and following a line. These robots utilize various sensors, such as infrared or reflective sensors, to detect the line on the surface and make decisions on how to navigate based on the sensor readings.

The primary objective of a line following robot is to maintain its position relative to the line, ensuring accurate tracking and smooth movement. By interpreting the sensor data, the robot can make real-time adjustments to its steering or motor control, allowing it to stay centered on the line.

Line following robots find applications in diverse fields, ranging from industrial automation to educational projects. They are commonly used in tasks such as warehouse logistics, automated guided vehicles (AGVs), and even in competitions like line following robot races.

To implement line following functionality, a line sensor module is typically used. This module consists of multiple sensors arranged in a line, enabling the robot to detect deviations from the desired path. By analyzing the sensor readings, the robot can adjust its movement, such as turning left or right or maintaining a straight trajectory, to stay on the line.

In this project, we will explore the development of a line following robot using an Arduino board and a line sensor module. By combining the power of microcontrollers, sensor integration, and motor control, we can create an intelligent robot capable of autonomously following a line.



## Implementing Line Following

```haskell
#include <ginobot.h>
```
```arduino
int Right = 0;
int Left = 0;
int Move_Speed = 70;
int Turn_Speed = 55;

Ginobot gbot;


void setup()
{
  Wire.begin();
  delay(1000); 
}

void loop()
{

  Right = gbot.get_bottom_right();
  Left = gbot.get_bottom_left();

  if (Right == 0 && Left == 0 )
  {
    gbot.move_forward(Move_Speed);
  }
  if(Right == 1 && Left == 0)
  {
    gbot.rotate_left(Turn_Speed);
  }
  else if(Left == 1 && Right == 0)
  {
    gbot.rotate_right(Turn_Speed);
  }
  else if (Right == 1 && Left == 1)
  {
    gbot.move_backward(Move_Speed);
  }
}

```

The code begins by including the ginobot.h library, indicating that it provides the necessary functions and definitions for controlling the robot.

Next, some variables are declared: Right, Left, Move_Speed, and Turn_Speed. These variables are used to store sensor readings and control the movement speeds of the robot.

An instance of the Ginobot class, named gbot, is created.

In the setup() function, the code initializes the Wire library, and includes a delay of 1 second.

The loop() function is where the main behavior of the robot is implemented.

The Right and Left variables are updated by calling the get_bottom_right() and get_bottom_left() functions of the Ginobot object gbot, respectively. These functions retrieve sensor readings from the robot's bottom-right and bottom-left IR sensors.

The code then uses a series of conditional statements (if and else if) to determine the appropriate action based on the sensor readings:

If both Right and Left are 0, indicating that the robot is on the line, the code calls the move_forward() function of gbot to move the robot forward at the specified Move_Speed.

If only Right is 1 and Left is 0, the code assumes that the robot is deviating to the right of the line, and it calls the rotate_left() function of gbot to rotate the robot left at the specified Turn_Speed.

If only Left is 1 and Right is 0, the code assumes that the robot is deviating to the left of the line, and it calls the rotate_right() function of gbot to rotate the robot right at the specified Turn_Speed.

If both Right and Left are 1, the code assumes that the robot has lost the line and calls the move_backward() function of gbot to move the robot backward at the specified Move_Speed.

![line-folowing](/line.gif)

