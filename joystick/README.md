# Joystick Control for Vehicle

## About This Project
This is the earlier design of the robot vehicle project using wired joystick control. This project can be served as a guide for controlling other mechanical system such as robot arms.

Please see [here](https://github.com/YiChiMa/robot-car) for more details.


## Components

**Arduino Uno**

**Joystick**
 * For communication and control

## Schematics
![optional caption text](scheme/joystick.jpg)

## Design Analysis
![Figure 1](scheme/joystickdiagram.jpg)
The raw output value for both axis is ranged from 0 - 1024. I use map function to map the value to a range of 0 - 255 for driving the motors.


## Code
This is the arduino code with extension .ino.
This code is integrated with the vehicle design. Please see [here](https://github.com/YiChiMa/robot-car).

```
const int xPin = A0;
const int yPin = A1;
int x = 0;
int y = 0;
int v = 0;
int d = 0;


void setup() {
  Serial.begin(9600);
}

void loop() {
  delay(100);
  x = analogRead(xPin);
  delay(100);
  y = analogRead(yPin);
  delay(100);

  Serial.print("X value: ");
  Serial.println(x);

  Serial.print("Y value: ");
  Serial.println(y);

  if (x <= 500){
    x = 499-x;
    v = map(x, 0, 499, 0, 255);
    Serial.print("+ Speed: ");
    Serial.println(v);
    delay(50);
    analogWrite(3,v);
    analogWrite(6,0);
    analogWrite(9,v);
    analogWrite(10,0);
  }

  else if (x>=525){
    v = map(x, 525, 1023, 0, 255);
    Serial.print("- Speed: ");
    Serial.println(v);
    delay(50);
    analogWrite(3,0);
    analogWrite(6,v);
    analogWrite(9,0);
    analogWrite(10,v);
  }

else if (y <= 250){
    y = 249-y;
    v = map(y, 0, 249, 0, 255);
    Serial.print("+ Speed: ");
    Serial.println(v);
    delay(50);
    analogWrite(3,v);
    analogWrite(6,0);
    analogWrite(9,0);
    analogWrite(10,v);
  }

  else if (y>776){
    v = map(y, 776, 1023, 0, 255);
    Serial.print("- Speed: ");
    Serial.println(v);
    delay(50);
    analogWrite(3,0);
    analogWrite(6,v);
    analogWrite(9,v);
    analogWrite(10,0);
  }

  else {
    analogWrite(3,0);
    analogWrite(6,0);      
    analogWrite(9,0);
    analogWrite(10,0);       
  }
}
```
