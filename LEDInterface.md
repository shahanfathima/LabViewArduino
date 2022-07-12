[We have loaded the firmware onto the Arduino.](https://github.com/jineshkjose/LabViewArduino/blob/main/Installation.md)

Here I'm going to do is demonstrate how I built off the blink sketch example from the Arduino IDE on the left.And develop this functionality in LabVIEW with the LINX functions.On the right, you can see the VI front panel I've prepared. Which show's the indicator's and circuit schematic for the LED connected to the Arduino. In the sketch code, we can see we are writing to the digital input and output pin 13 a HIGH or a LOW value ever second. When HIGH, 5V is output on pin 13 and the LED turns ON. When LOW, 0V is output on pin 13 and the LED turns OFF.In LabVIEW we are replicating this function by writing to pin 13.

The first place we are going to start when we create a new VI.Is to actually locate the LINX functions.
- Under the menu, "MakerHub"> "LINX"
Let's pin this so we can see it at all times.As you can see here there are a few basic and essential functions. To open and close , you need to open your VISA session.To your hardware, whether it's an Arduino or Raspberry Pi or anything else supported by the LINX toolkit.And then you need to close that session, to exit it properly.

If we look at the left of the block diagram, here, we are opening a VISA session to the Arduino.Allocating the resources in memory and configuring any serial parameters.In this case, we are only specifying the serial address, which is COM21.Let's read its output terminal to confirm we're communicating with the Arduino. If we select the Open VI and look at the Context Help, we can see an output listed as "Device Name".
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
