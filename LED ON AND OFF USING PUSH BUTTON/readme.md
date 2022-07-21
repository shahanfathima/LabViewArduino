## Aim
To perform blinking of led by interfacing with Arduino
## Required Material
Arduino Uno board

Push-button

Led

Breadboard

Hook up wires

USB cable
## Circuit
![Daring Crift-Kup (1)](https://user-images.githubusercontent.com/109128832/180274885-87902a76-9297-4a93-9434-221f1315b5cd.png)

## Procedure
### Step 1:
The first pin the push button is connected to a 5 volt supply.

The second pin the push button is connected to gnd and to digital pin 02.

The LED has a positive and a negative point.

The positive point of LED is connected to a digital pin 12.

The negative points connected to a gnd.
### Step 2:
 
Connect the Arduino board to your computer with the USB cable and start sketching the following program, 
 
### #Step 3:
Programming
~~~
int led = 12;  
int Button = 2;  
void setup()  
{  
    pinMode(Button, INPUT);  
    pinMode(led, OUTPUT);  
  digitalWrite(led, LOW);
}  
void loop()  
{  
   
    if (digitalRead(Button)==LOW)  
    {  
        digitalWrite(led, HIGH); // Turn on led  
    }  
    else  
    {  
        digitalWrite(led, LOW); //Turn off led  
    }  
   
}  
~~~
## Result
Led on and off pressing push button.

