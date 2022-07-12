
# Installation


Today we are going to show you how to interface your Arduino with LabVIEW.Before we get started, we require the following items.
- An Arduino UNO, MEGA or etc.
- LabVIEW 2011 or greater.
- The latest NI VISA drivers for your version of LabVIEW.
- The JKI VI packager manager.
- The LINX add-on.
- Arduino drivers and IDE.

Firstly, lets open the VI package manager.Which is a nice utility for downloading various LabVIEW add-ons.
![vipakage](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/vipackage.png)
Next we want to go to the search bar and type in "Arduino".Once our results have appeared, we want to select and install the LINX add-on.Notice however, there is also a LIFA add-on. This is no longer supported by NI and has been superseded by LINX.Now let's install the LINX add-on.Once the package loads, you want to click on the install button for your version of LabVIEW.Now let's confirm the Arduino and PC are communicating properly. To do this, lets open NI MAX.
![Nimax](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/ni%20max.png)
First lets confirm if we have the latest NI VISA driver installed.Click and expand Software and go down and select your NI VISA driver and confirm its the latest version for your version of LabVIEW.Next we want to go into Devices and Interfaces up here and expand.Now select the COM port your Arduino is currently connected to.For my PC it's COM port 21.If you look under the port description, you can see that the Arduino UNO is listed.

You can also see and adjust various other port settings, such as the Baud Rate which may be important to you depending on your application. Now a quick way to test if your VISA session is active is to use the VISA test panel.If you open that here, you will get a nice test panel. Which will show you again, your serial port settings.Select Input and Output and do a quick write. If you get no error on return, it means your Arduino is communicating correctly.
![nimax2](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/nimax2.png)
An additional method to confirm your Arduino is communicating with your PC is to open the Arduino IDE.Once loaded, you will have a basic sketch open. Go to Tools and select Port, again you can see COM port 21 confirms the Arduino is present.You can also select Board Info which confirms you are able to communicate with your Arduino.As if you couldn't an error would occur once selected.Now that communication is confirmed. 

Lets open LabVIEW to load the LINX firmware onto the Arduino.
- Go to "Tools", select "MakerHub" > "LINX" > "LINX Firmware Wizard".
![LINX firmware](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/linx%201.png)
- Once loaded, select the "Device Family" > "Arduino". "Device Type" > "UNO" 
![LINX firmware](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/linx2.png)
- The "Firmware Method"> "USB", click next.
- Select the COM port. COM21 in my case.
![LINX firmware](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/linx3.png)
- Then confirm the "Firmware Version" and " Upload Type" then select next.

Now we wait for the firmware to upload to the Arduino.
![LINX firmware](https://github.com/jineshkjose/LabViewArduino/blob/main/imgs/linx4.png)

Now that the firmware has been uploaded, we can begin programming the Arduino in LabVIEW.
