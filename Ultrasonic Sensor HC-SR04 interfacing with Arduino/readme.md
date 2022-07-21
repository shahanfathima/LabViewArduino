## Aim
To measure and display distance of an object from ultrasonic sensor interfaced with Arduino.
## Required Material
Arduino Uno R3 board, lcd 16 x 2 module, ultrasonic distance sensor , Breadboard, Wires
## Circuit
![Super Juttuli (1)](https://user-images.githubusercontent.com/109128832/180267962-fef63289-e5c7-4de5-8ef5-616a8fcefdca.png)

## Procedure
### Step 1:
Build the circuit.
 The circuit:
 * LCD RS pin to digital pin 12
 * LCD Enable pin to digital pin 11
 * LCD D4 pin to digital pin 5
 * LCD D5 pin to digital pin 4
 * LCD D6 pin to digital pin 3
 * LCD D7 pin to digital pin 2
 * LCD R/W pin to ground
 * LCD VSS pin to ground
 * LCD VCC pin to 5V
 * 10K resistor:
 * ends to +5V and ground
 * wiper to LCD VO pin (pin 3)
 * Pin1 (Vcc): This pin provides a +5V power supply to the sensor.
 * Pin2 (Trigger): This is an input pin, used to initialize measurement by transmitting ultrasonic waves by keeping this pin high for 10us.
 * Pin3 (Echo): This is an output pin, which goes high for a specific time period and it will be equivalent to the duration of the time for the wave to return back to    the sensor.
 * Pin4 (Ground): This is a GND pin used to connect to the GND of the system.
### Step 2:
 
Connect the Arduino board to your computer with the USB cable and start sketching the following program, 
 
### #Step 3:
Programming
~~~
#include <LiquidCrystal.h>

// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
// defining the pins
const int trigPin = 9;
const int echoPin = 10;
// defining variables
long duration;
int distance;
void setup() {
pinMode(trigPin, OUTPUT); // Sets the trigPin as an Output
pinMode(echoPin, INPUT); // Sets the echoPin as an Input
Serial.begin(9600); // Starts the serial communication
lcd.begin(16, 2);
   
}
void loop() {
// Clears the trigPin
digitalWrite(trigPin, LOW);
delayMicroseconds(2);
// Sets the trigPin on HIGH state for 10 micro seconds
digitalWrite(trigPin, HIGH);
delayMicroseconds(10);
digitalWrite(trigPin, LOW);
// Reads the echoPin, returns the sound wave travel time in microseconds
duration = pulseIn(echoPin, HIGH);
// Calculating the distance
distance= duration*0.034/2;
// Prints the distance on the Serial Monitor
Serial.print("Distance: ");
Serial.println(distance);
lcd.clear();
lcd.setCursor(0, 1);
  lcd.print("Distance:");
  lcd.println(distance);
  delay(1000);

}
~~~
## Result
Distance of object from ultrasonic sensor measured and displayed on LCD screen.

