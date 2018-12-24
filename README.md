# Bluetooth-Controlled Robot Vehicle

## About This Project
This project can be served as a basic guideline for building robots of any kind because it is simple to build and easy to make further improvement. I designed this vehicle from the scratch.


## Components
**Car Chassis**

**4 Motors**

**Bread Board**
  * For connecting and organizing all the wires

**Arduino Uno**
**H-Bridge**
  * For this project, L298N Motor Drive Controller Board DC Dual H-Bridge was used
  * For controlling the motors

**9 V Batteries**
  * Power supply for both Arduino and motor system

**Bluetooth Module**
 * For communication and control

## Schematics
![optional caption text](scheme/bluetooth.jpg)

## Design Analysis
![Figure 1](scheme/mechanics1.jpg)
The idea for driving the vehicle forward and backward is very simple and straightforward as shown in the figure.
![](scheme/mechanics2.jpg)
The general idea for change the direction of the movement is to make motors spin in different directions. One side wheels spin in a direction while the wheels on the other side spin in an opposite direction. Thus, it produces a rotation on the chassis.

## Further Improvement

## Code
This is the arduino code with extension .ino
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

## Previous Design Using Joystick
