---
weight: 4
title: Object Avoidance
---

# Object Avoidance

## Introducing Object Avoidance

Object avoidance is a fundamental aspect of robotics that enables autonomous robots to navigate in dynamic environments without colliding with obstacles. By integrating sensors, algorithms, and intelligent decision-making, robots can detect and respond to objects in their surroundings, ensuring safe and efficient movement.

In this project, we will explore the development of an object avoidance system using a single front ultrasonic sensor. The ultrasonic sensor emits high-frequency sound waves and measures the time it takes for the waves to bounce back after hitting an object. By analyzing this data, the robot can determine the distance to the object in its path.

The objective of the object avoidance system is to detect objects within a certain range and take appropriate actions to avoid them. When an object is detected, the robot can perform maneuvers such as stopping, changing direction, or slowing down to ensure a safe and obstacle-free path.

The implementation of the object avoidance system involves integrating the ultrasonic sensor into the robot's control system. The sensor readings are processed and analyzed to make decisions about the robot's movement. Advanced algorithms, such as obstacle mapping or path planning, can be employed to optimize the avoidance behavior and enable efficient navigation in complex environments.

Object avoidance finds applications in various fields, including robotics research, autonomous vehicles, and industrial automation. It plays a crucial role in tasks such as mobile robot navigation, robotic exploration, and collision avoidance in dynamic environments. By building an object avoidance system, you will gain valuable insights into sensor integration, data processing, and decision-making algorithms, contributing to your understanding of robotics and autonomous systems.

## Implementing Object Avoidance


```haskell
#include <ginobot.h>
```

```arduino
Ginobot gbot;

int distance;
int Move_Speed = 75;
int Turn_Speed = 75;

void setup()
{
  Wire.begin();
  delay(1000);
}

void loop(){
  gbot.set_front_lights(0, 255, 0);
  gbot.set_back_lights(0, 0, 0);   
  distance = gbot.get_distance_front_mm(); 
  gbot.move_forward(Move_Speed);
  delay(500);

  if (distance <= 200){
    gbot.set_front_lights(0, 0, 255);
    gbot.set_back_lights(0, 0, 255);
    
    gbot.stop();
    gbot.rotate_right(Turn_Speed);
    delay(1000);
	  
  }
  if(gbot.get_wheel_left_speed() == 0){
    gbot.set_front_lights(255, 0, 0);
    gbot.set_back_lights(0, 255, 0);
    
    gbot.stop();
    gbot.move_backward(Move_Speed);
    delay(500);
    gbot.rotate_right(Turn_Speed);
    delay(1000);
    gbot.move_forward(Move_Speed);

  }
}
```

The code starts by including the ginobot.h library, indicating that it provides the necessary functions and definitions for controlling the robot.

An instance of the Ginobot class, named gbot, is created.

The distance variable is declared to store the distance measurement from the front sensor.

In the setup() function, the code initializes the Wire library and includes a delay of 1 second.

The loop() function is where the main behavior of the robot is implemented.

The code starts by setting the front lights of the robot to green and the back lights to off using the set_front_lights() and set_back_lights() functions of gbot, respectively.

The code then retrieves the distance from the front sensor in millimeters using the get_distance_front_mm() function and stores it in the distance variable.

Next, the code commands the robot to move forward at the specified Move_Speed using the move_forward() function of gbot.

After a delay of 500 milliseconds, the code checks if the distance is less than or equal to 200 (indicating an obstacle in front of the robot).

If an obstacle is detected, the front lights are set to blue, and the back lights are also set to blue using the set_front_lights() and set_back_lights() functions.

The robot is then commanded to stop using the stop() function of gbot.

After a delay of 1 second, the robot rotates to the right using the rotate_right() function with the specified Turn_Speed.

The code continues with an if statement to check if the left wheel speed is zero, which could indicate the robot is stuck.

If the left wheel speed is zero, the front lights are set to red, and the back lights are set to green.

The robot is stopped using the stop() function.

The robot then moves backward at the specified Move_Speed using the move_backward() function.

After a delay of 500 milliseconds, the robot rotates to the right using the rotate_right() function.

Finally, after a delay of 1 second, the robot moves forward again at the specified Move_Speed using the move_forward() function.
![object-avoidance](/object.gif)
