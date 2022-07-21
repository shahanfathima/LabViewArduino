## Aim
To print "Hello World" on LCD screen.
## Required Material
Arduino Uno R3 board, lcd 16 x 2 module, Breadboard, Wires
## Circuit
![Super Juttuli](https://user-images.githubusercontent.com/109128832/180261288-afa90db0-c0a5-41ea-9ef9-d1fbd57991a6.png)

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

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  lcd.print("hello, world!");
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.setCursor(0, 1);
  // print the number of seconds since reset:
  lcd.print(millis() / 1000);
}
~~~
## Result
"Hello World" displayed on LCD screen.

