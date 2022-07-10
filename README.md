# Installation


0:00
Hi Everyone, Sin here.
0:01
Today we are going to do some engineering and stuff.
0:03
And I'm going to show you how to interface your Arduino with LabVIEW.
0:07
Before we get started, we require the following items.
0:10
An Arduino UNO, MEGA or etc.
0:13
LabVIEW 2011 or greater.
0:15
The latest NI VISA drivers for your version of LabVIEW.
0:18
The JKI VI packager manager.
0:21
The LINX add-on.
0:22
And lastly, the Arduino drivers and IDE.
0:25
Firstly, lets open the VI package manager.
0:28
Which is a nice utility for downloading various LabVIEW add-ons.
0:32
Next we want to go to the search bar and type in "Arduino".
0:36
Once our results have appeared, we want to select and install the LINX add-on.
0:41
Notice however, there is also a LIFA add-on. This is no longer supported by NI and has been superseded by LINX.
0:49
Now let's install the LINX add-on.
0:52
Once the package loads, you want to click on the install button for your version of LabVIEW.
0:57
As you can see, I've pre-installed these so we can move on to the next step.
1:00
Now let's confirm the Arduino and PC are communicating properly. To do this, lets open NI MAX.
1:07
First lets confirm if we have the latest NI VISA driver installed.
1:11
Click and expand Software and go down and select your NI VISA driver and confirm its the latest version for your version of LabVIEW.
1:18
Next we want to go into Devices and Interfaces up here and expand.
1:22
Now select the COM port your Arduino is currently connected to.
1:26
For my PC it's COM port 6.
1:29
If you look under the port description, you can see that the Arduino UNO is listed.
1:33
You can also see and adjust various other port settings, such as the Baud Rate which may be important to you depending on your application.
1:40
You can also see these details in your PC's Device Manager, which I will not cover here.
1:45
Now a quick way to test if your VISA session is active is to use the VISA test panel.
1:50
If you open that here, you will get a nice test panel. Which will show you again, your serial port settings.
1:56
Select Input and Output and do a quick write. If you get no error on return, it means your Arduino is communicating correctly.
2:03
An additional method to confirm your Arduino is communicating with your PC is to open the Arduino IDE.
2:09
Once loaded, you will have a basic sketch open. Go to Tools and select Port, again you can see COM port 6 confirms the Arduino is present.
2:19
You can also select Board Info which confirms you are able to communicate with your Arduino.
2:24
As if you couldn't an error would occur once selected.
2:27
Now that communication is confirmed. Lets open LabVIEW to load the LINX firmware onto the Arduino.
2:32
Go to "Tools", select "MakerHub" > "LINX" > "LINX Firmware Wizard".
2:39
Once loaded, select the "Device Family" > "Arduino". "Device Type" > "UNO" in my case.
2:46
The "Firmware Method"> "USB", click next.
2:49
Select the COM port. COM6 in my case.
2:53
And then confirm the "Firmware Version" and " Upload Type" then select next.
2:59
Now we wait for the firmware to upload to the Arduino.
3:02
Now that the firmware has been uploaded, we can begin programming the Arduino in LabVIEW.
3:06
Let's begin!
3:07
Alright, now that we have loaded the firmware onto the Arduino.
3:10
A good place to start,
3:12
with hardware I find is to build off an existing example.
3:14
Generally when you purchase hardware, it will come with an example.
3:18
Whether it's in C, Python or MATLAB etc.
3:21
A good starting point is to replicate those examples.
3:24
In LabVIEW to confirm that you have the same functionality.
3:26
All I'm going to do is demonstrate how I built off the blink sketch example from the Arduino IDE on the left.
3:32
And develop this functionality in LabVIEW with the LINX functions.
3:35
On the right, you can see the VI front panel I've prepared.
3:38
Which show's the indicator's and circuit schematic for the LED connected to the Arduino.
3:42
In short, what are we doing? We are turning on and off the LED at a frequency of 1Hz.
3:47
In the sketch code, we can see we are writing to the digital input and output pin 13 a HIGH or a LOW value ever second.
3:54
What does this do?
3:55
When HIGH, 5V is output on pin 13 and the LED turns ON.
4:00
When LOW, 0V is output on pin 13 and the LED turns OFF.
4:04
In LabVIEW we are replicating this function by writing to pin 13.
4:07
On the Arduino, at a frequency we select on the slider control here.
4:12
Ok, now that we have a basic theory of operation.
4:14
Let's look at the block diagram to understand how we are programming the Arduino.
4:18
The first place we are going to start when we create a new VI.
4:21
Is to actually locate the LINX functions.
4:24
Under the menu, "MakerHub"> "LINX"
4:26
Let's pin this so we can see it at all times.
4:29
As you can see here there are a few basic and essential functions.
4:32
Open and Close, you need to open your VISA session.
4:36
To your hardware, whether it's an Arduino or Raspberry Pi or anything else supported by the LINX toolkit.
4:41
And then you need to close that session, to exit it properly.
4:44
If we look at the left of the block diagram, here, we are opening a VISA session to the Arduino.
4:49
Allocating the resources in memory and configuring any serial parameters.
4:52
In this case, we are only specifying the serial address, which is COM6.
4:56
As we determined previously.
4:57
All other configuration settings are set to there default values, such as the baud rate for example.
5:03
As we can see this is a polymorphic VI.
5:06
Which allows different configurations of communications protocols.
5:09
Let's leave this as automatic.
5:11
Once we have configured the Open VI.
5:13
Let's read its output terminal to confirm we're communicating with the Arduino.
5:17
Successfully in LabVIEW.
5:19
This will be the third method and final method, confirming we are talking to the Arduino.
5:24
It's always a good idea to do a bit of due diligence.
5:27
If we select the Open VI and look at the Context Help, we can see an output listed as "Device Name".
5:32
This will show a string confirming what model Arduino is connected.
5:36
Now let's place a break point here to stop the code and look at the output by placing a probe.
5:41
We can now examine the output as the code runs and should see the string output in the probe display.
5:46
And the string indicator on the front panel.
5:49
So let's run the code, wait for it to upload to the Arduino.
5:52
Once we reach the breakpoint, the code will pause.
5:55
Now we can see we have successfully read the device name in both the probe display and string indicator.
6:01
Now that we know the code is running, lets abort it and see what happens when you don't close a VISA session properly.
6:06
A common error most people make, when interfacing with hardware.
6:10
So we abort, we remove the breakpoint, by breakpoint, clear.
6:14
Let's leave this probe open to see what happens.
6:18
Now let's run this VI.
6:20
And as we can see, it failed to connect to the Arduino.
6:23
The reason being, we did not appropriately close the resource allocated to COM port 6.
6:28
Now if we continue, this will be flushed from memory and we can run the code successfully, again.
6:32
Let's run, and now we can see we're connected to the Arduino.
6:37
As we've now free'd up that resource.
6:39
With a quick stop, the resource will close and we will not have that error issue again.
6:44
Again, we run the code.
6:46
And we have a blinking LED, so let's stop the code.
6:49
So let's remember, it's always important to close your resources appropriately,
6:54
and not to prematurely abort them.
6:56
You always want to handle this using the appropriate error handling methods in your VI.
7:00
The way we're handling errors in this VI, is very simple.
7:04
Once the loop stops, by either having an error occur or the stop button returning TRUE.
7:11
We exit the loop, the close function then frees any resources and closes the session to the hardware, in this case the Arduino.
7:18
Then any resulting errors are handled by this error function.
7:21
If we go to context help, by clicking this question mark here.
7:24
We can see a short description of what this VI does.
7:27
The Simple Error Handler VI will just return,
7:30
a description of the error once it occurs,
7:32
this is very handy when you're developing your VIs,
7:35
and you just need a simple error return.
7:36
You can access the Simple Error Handler VI, by simply right clicking the block diagram.
7:41
Going to "Dialog and User Interface" and finding the Simple Error Handler.
7:46
Additionally, you can press "CTRL+Spacebar" to bring up the quick drop menu.
7:52
Type in "Simple Error Handler".
7:55
Double click, and the Error Handler VI will appear.
7:59
Now that we know how to open and close the sessions properly to our hardware.
8:03
Let's look at the meat of the code, to see how we're actually writing to pin 13.
8:08
Flashing the LED and handling the frequency.
8:11
First let's organise our workspace, so we have a clearer picture.
8:13
Close the probe.
8:15
Yes.
8:17
Now essentially there are four sections to our while loop.
8:20
The first being, the frequency control which determines the loop speed.
8:24
The second being, a simple piece of logic to determine if the LED will be on or off.
8:28
The third, actually writing the boolean value to the appropriate pin. Which is pin 13.
8:34
And the fourth, is the loop condition for determining when to stop the while loop.
8:37
Let's start by examining the frequency control section of the while loop.
8:42
First, we're taking an integer value and taking its reciprocal,
8:45
we're multiplying this value by 1000 to convert it to milliseconds.
8:49
We are then, converting it to an unsigned 32 bit integer.
8:53
And then feeding this value into Wait ms function.
8:56
Which will hold the loop for the specified amount of ms. Before iterating, to the next loop.
9:01
This way, we are able to control the frequency of while loop and hence, the frequency of the LED flashing,
9:07
on the Arduino.
9:08
You may notice on the front panel the frequency control is a horizontal slider.
9:13
You can access this horizontal slider, by right clicking the front panel.
9:16
Go into "Numeric" and then horizontal pointer slide.
9:19
Notice, the values are only from 1 to 10.
9:24
This has been done by right clicking the control.
9:26
"Properties" > "Data Entry"
9:30
Minimum value set to 1.
9:32
Maximum value set to 10.
9:35
And the increment set to 1.
9:37
Notice that the properties are coerce to nearest.
9:39
This allows you to increment in integer values.
9:43
If we go back to the frequency section of the code.
9:46
You may of been asking yourself why did I convert a double value of the frequency into an unsigned integer?
9:52
The reason is, it's generally good practice to convert different data representations,
9:58
when you have two different types between functions.
10:01
This is to avoid coercion dots, which I will not go into detail here.
10:04
Now let's look at the Digital Write function from the LINX library.
10:07
This is quite a simple function.
10:09
It simply allows you to select an input channel and write boolean value to that digital channel.
10:14
In this case, we're only writing to a single channel.
10:16
As you can see this is again a polymorphic VI.
10:19
And we have selected one channel.
10:21
You are able to also select N-channels, or automatic.
10:24
If you select N-channels, it will accept an array as an input.
10:28
Which specify the range of channels you want to write to.
10:31
It will also require an array of boolean inputs.
10:34
Let's go back to automatic.
10:35
As you can see, it has gone back to single channel.
10:38
Channel 13 and we are writing the boolean value.
10:42
Which we determine here.
10:43
Now it's easy to manually control the LED by simply placing a boolean control.
10:48
Which can turn on and off.
10:49
But in our case, I want to completely replicate the example blink sketch.
10:53
By having this LED turn on and off with the frequency of the while loop.
10:57
To handle this in this VI, all I'm doing is implementing a case structure,
11:01
Which will write a true value or a false value.
11:05
Depending on if the loop counter is odd or even.
11:09
How is this done, I take the loop counter value.
11:12
Divide it by 2 and check if the remainder is 0 or not.
11:15
If the remainder is 0, we have an even value and we write TRUE (1).
11:21
If the remainder is not 0, we have an odd value and we write FALSE(0)
11:25
This will illuminate the LED and write to the digital output pin of the Arduino.
11:30
Lastly, what's the loop condition of the while loop.
11:32
It's if an error occurs or we press the stop button.
11:36
It then simply exits, closes the session, handles any errors.
11:41
Now that we have a basic understanding of how we're blinking the LED at a frequency of 1Hz.
11:46
Or at a rate we select.
11:47
Let's see how this works in real-time with the Arduino.
11:52
The code is now running and as we can see the LED on the VI and in our circuit are blinking in sync.
11:59
As we adjust the slider between 1Hz and 10Hz, we see the LED flashing with the appropriate frequency.
12:06
Thank you for watching my video, please subscribe, share and comment if you enjoyed or didn't below.
12:12
See you ne xt time!
