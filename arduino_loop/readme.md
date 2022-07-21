## Aim
To perform blinking of leds by interfacing with Arduino
## Required Material
Arduino Uno R3 board, Red led, Blue led, 2 Resistor(150ohm), Breadboard, wires
## Circuit
![Super Juttuli](https://user-images.githubusercontent.com/109128832/180256414-e1ad5ec4-b20b-4b6c-9ab3-0195c2171c35.png)

## Procedure
### Step 1:
Build the circuit.
### Step 2:
 
Connect the Arduino board to your computer with the USB cable and start sketching the following program, 
 
### Step 3:
Programming
~~~
int red=13;//set red led pin =13;
int blue=12;//set Blue led pin= 12;
int r_time=500;//RED LED DELAY TIME =1/2 SCEUND
int b_time=500;//BLUE LED DELAY TIME =1/2 SECUND
int NUM_R=2;
int NUM_B=5;

void setup() {

  //SET PIN MODE

 pinMode(red,OUTPUT);
 pinMode(blue,OUTPUT);

// SET INIATAILY AT OFF

 digitalWrite(blue,LOW);
 digitalWrite(red,LOW);

}


void loop() {


for(int a=1;a<=NUM_R;a++)

{

  digitalWrite(red,HIGH);//RED LED ON
  delay(r_time);//WAIT
  digitalWrite(red,LOW);//RED LED OFF
  delay(r_time);//WAIT

}

for(int b=1;b<=NUM_B;b++)

{

  digitalWrite(blue,HIGH);//Blue LED ON
  delay(b_time);//WAIT
  digitalWrite(blue,LOW);//BLUE LED OFF
  delay(b_time);//WAIT 

}
}
~~~
## Result
Blue led blinks two times and red led blinks 5 times.



