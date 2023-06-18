---
weight: 2
title: Lesson 2
---

# Lesson 2

## Using the Ginobot Library

```go
// Assigning Object for Library
Ginobot gbot;
```

### Set up the GinoBot

```arduino
void setup()
{
  Wire.begin();
  // Give some time to the GinoBot to initialize
  delay(1000);             
}
```

In the setup() function, initialize the GinoBot by calling Wire.begin() to join the I2C bus. This step is required for communication with the GinoBot. Additionally, you can perform any necessary setup steps specific to your project.



## Control the GinoBot

In the loop() function, you can use various library commands to control the GinoBot based on sensor readings or other conditions. 

### Commands allowing you to retrieve data from the Ginobot

```arduino
void loop() {
  // Read the distance from the front ultrasonic sensor
  int distance = gbot.get_distance_front_mm();

  // If an obstacle is detected within 200mm, stop and rotate left
  if (distance <= 200) {
    gbot.stop();
    gbot.set_front_lights(255, 0, 0); // Set front lights to red
    gbot.set_back_lights(255, 0, 0);  // Set back lights to red

    // Rotate left for 1 second
    gbot.rotate_left(75);
    delay(1000);
  } else {
    // No obstacle detected, continue moving forward
    gbot.move_forward(75);
  }

  // Delay for a short period between each loop iteration
  delay(100);
}
```

| Command                      | Description                                                                          |
| ---------------------------- | ------------------------------------------------------------------------------------ |
|   get_distance_front_mm()    | Returns the ultrasonic distance in mm. Requires ultrasound sensor present on Ginobot |
|   get_IR_FL_analog()         | Returns the Front Left IR sensor analog value (0-100)                                |
|   get_IR_FR_analog()         | Returns the Front Right IR sensor analog value (0-100)                               |
|   get_IR_Back_analog()       | Returns the Back IR sensor analog value (0-100)                                      |
|   get_IR_FL                  | Returns the Front Left IR sensor digital value (1 or 0)                              |
|   get_IR_FR                  | Returns the Front Right IR sensor digital value (1 or 0)                             |
|   get_IR_Back                | Returns the Back IR sensor digital value (1 or 0)                                    |
|   get_bottom_left            | Returns the Bottom Left IR sensor digital value (1 or 0)                             |
|   get_bottom_left_white()    | Returns the Bottom Left color sensor white intensity (0-255)                         |
|   get_bottom_left_red()      | Returns the Bottom Left color sensor red intensity (0-255)                           |
|   get_bottom_left_green()    | Returns the Bottom Left color sensor green intensity (0-255)                         |
|   get_bottom_left blue()     | Returns the Bottom Left color sensor blue intensity (0-255)                          |
|   get_bottom_right()         | Returns the Bottom Right IR sensor digital value (1 or 0)                            |
|   get_bottom_right_white()   | Returns the Bottom Right color sensor white intensity (0-255)                        |
|   get_bottom_right_red()     | Returns the Bottom Right color sensor red intensity (0-255)                          |
|   get_bottom_right_green()   | Returns the Bottom Right color sensor green intensity (0-255)                        |
|   get_bottom_right_blue()    | Returns the Bottom Right color sensor blue intensity (0-255)                         |
|   get_wheel_right_speed()    | Returns the current speed of the right wheel (0-100)                                 |
|   get_wheel_right_position() | Returns the current position of the right wheel in clicks (0 – 65535)                |
|   get_wheel_left_speed()     | Returns the current speed of the left wheel (0-100)                                  |
|   get_wheel_left_position()  | Returns the current position of the left wheel in clicks (0 – 65535)                 |
|   get_battery_level()        | Returns the current battery level (0 – 4)                                            |


### Commands allow you to control the GinoBot

```arduino
void loop() {
  // Read the digital values of the left and right line sensors
  int leftSensor = gbot.get_IR_FL();
  int rightSensor = gbot.get_IR_FR();

  // If both line sensors detect the line, move forward
  if (leftSensor == 1 && rightSensor == 1) {
    gbot.move_forward(50);
  }
  // If only the left sensor detects the line, turn left
  else if (leftSensor == 1 && rightSensor == 0) {
    gbot.rotate_left(50);
  }
  // If only the right sensor detects the line, turn right
  else if (leftSensor == 0 && rightSensor == 1) {
    gbot.rotate_right(50);
  }
  // If neither sensor detects the line, stop
  else if (leftSensor == 0 && rightSensor == 0) {
    gbot.stop();
  }

  // Delay for a short period between each loop iteration
  delay(100);
}
```

| Command                      | Description                                                                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| move(x)                      | Commands the Ginobot to move with speed x (-100 – 100). Moves forward if x is a positive value; moves backwards if x is a negative value |
| move_forward(x)              | Commands the Ginobot to move forward with speed x (0 - 100)                                                                              |
| move_backward(x)             | Commands the Ginobot to move backward with speed x (0 - 100)                                                                             |
| rotate(x)                    | Commands the Ginobot to rotate with speed x (0-100). Rotates right if x is a positive value; rotates left if x is a negative value       |
| rotate_right(x)              | Commands the Ginobot to rotate right with speed x (0-100)                                                                                |
| rotate_left(x)               | Commands the Ginobot to rotate left with speed x (0 -100)                                                                                |
| stop()                       | Commands the Ginobot to stop moving.                                                                                                     |
| wheel_left_spin(x)           | Commands the Ginobot to turn the left wheel with speed x (0-100)                                                                         |
| wheel_right_spin(x)          | Commands the Ginobot to turn the right with speed x (0 -100)
| move_distance_mm(x, y, z)    | Commands the Ginobot to move a specific distance in mm, where x is the distance, y is the wheel diameter in mm and z is the speed (0 – 100). A positive x value will cause the Ginobot to move forward; a negative x value will cause the Ginobot to move backward |
| rotate_clicks(x, y)          | Commands the Ginobot to rotate for a specific amount of clicks, where x is the number of clicks and y is the speed (0 – 100). A positive x value will cause the Ginobot to rotate right; a negative x value causes the Ginobot to rotate left |
| wheel_left_turn(x, y)        | Commands the Ginobot to rotate the left wheel for a specific number of clicks, where x is the number of clicks and y is the speed (0 – 100). A positive x value causes the wheel to rotate clockwise; a negative x value causes the wheel to spin anticlockwise |
| wheel_right_turn(x, y)       | Commands the Ginobot to rotate the right wheel for a specific number of clicks, where x is the number of clicks and y is the speed (0 – 100). A positive x value causes the wheel to rotate clockwise; a negative x value causes the wheel to spin anticlockwise |
| set_IR_FL_threshold(x)       | Sets the threshold value of the Front Left IR sensor (0-100). When the sensor's analog value is below this then the sensor's digital value turns to 0, when it is higher than this, its digital value turns to 1 |
| set_IR_FR_threshold(x)       | Sets the threshold value of the Front Right IR sensor (0-100). When the sensor's analog value is below this then the sensor's digital value turns to 0, when it is higher than this, its digital value turns to 1 |
| set_IR_Back_threshold(x)     | Sets the threshold value of the back IR sensor (0-100). When the sensor's analog value is below this then the sensor's digital value turns to 0, when it is higher than this, its digital value turns to 1 |
| set_IR_bot_L_threshold(x)    | Sets the threshold value of the bottom left IR sensor (0-100). When the sensor's analog value is below this then the sensor's digital value turns to 0, when it is higher than this, its digital value turns to 1 |
| set_IR_bot_R_threshold(x)    | Sets the threshold value of the bottom right IR sensor (0-100). When the sensor's analog value is below this then the sensor's digital value turns to 0, when it is higher than this, its digital value turns to 1 |
| set_front_lights(r,g,b)      | Sets the Ginobot front RGB red LED with intensity r (0-255), green LED with intensity g (0-255) and blue LED with intensity b (0-255)     |
| set_back_lights(r,g,b)       | Sets the Ginobot back RGB red LED with intensity x (0-255), green LED with intensity y (0-255) and blue LED with intensity z (0-255)      |
| set_buzzer_frequency(f)      | Sets the Ginobot buzzer frequency in Hz to f (0-65535). Setting to 0 turns the buzzer off                                                 |
| servo1_position(x)           | Sets the position for servo1 in degrees to x (0-180)                                                                                      |
