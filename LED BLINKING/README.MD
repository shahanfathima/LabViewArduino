## Aim
To perform blinking of led by interfacing with Arduino
## Required Material
Arduino Uno board, Led,resistor(220ohm), Breadboard
wires
## Circuit
![led blinking png](https://user-images.githubusercontent.com/109128832/180232823-3f527b67-8281-4d2e-b020-0acf9ac4288c.png)
## Step 1:
Build the circuit.
## Step 2:
 
Connect the Arduino board to your computer with the USB cable and start sketching the following program, 
 
## Step 3: Programming
~~~
int ledpin=13;
int on_time=1000;
int off_time=1000;

void setup(){

  pinMode(ledpin,OUTPUT);

}


void loop() {

  digitalWrite(ledpin,HIGH);
  delay(on_time);
  digitalWrite(ledpin,LOW);
  delay(off_time);

}
~~~
## Result
Led blinks


