mDjiController
===============
 - Connect your DJI Remote Controller to your PC and use it to play simulators.
 - Currently confirmed working controllers: DJI Phantom 2
-----------------------------------------------------------------------------


This is a program that connects to your DJI Phantom Remote Controller (RC),
reads the stick positions and tells Windows that position. A simplified, wannabe driver.

In use:
![](https://raw.githubusercontent.com/Matsemann/mDjiController/master/in_use.png)

Here I'm flying a DJI Phantom in HELI-X5 using mDjiController. Open up the image in big version to see the controller configuration.

Installation
------------

In order for it to work, the original drivers from DJI must be installed, and something called vJoy.

* Download mDjiController.zip from above ( https://github.com/Matsemann/mDjiController/blob/master/mDjiController.zip?raw=true )
* Download DJI WIN Driver Installer from here: http://www.dji.com/product/phantom-2/download
* Download vJoy from here: http://vjoystick.sourceforge.net/site/index.php/download-a-install/72-download

* Install both.
* Then connect your RC to your computer via USB and turn it on.

* Run mDjiController.exe, and select the correct COM port. By default you should try writing "3".
* For vJoy, write 1 unless you use vJoy already and have different configurations.

Then open a simulator and calibrate the controller.

How does it work?
-----------------

* It is possible to ask the controller for its status when it's connected. So this program continuously
	reads the status. It connects through COM. The output from the controller is just a list of numbers,
	but sampling many enough such lists it's easy to see a pattern for which number means what. The biggest issue
	was that the numbers are little endian encoded and uses two's complement, so it took some time to understand how
	each number behaved.
	
* vJoy is a virtual joystick that can be installed on your computer. Windows think it's a normal joystick. mDjiController
	takes the stick positions from the controller and tells Windows that this virtual joystick has the same positions.


TROUBLESHOOTING
---------------
* If something doesn't work, make sure you have enabled logging, it may tell you the error.

* COM can't connect
	Try with other numbers instead of 3. Open up device-manager.
	You should see a category named "Ports (COM & LPT) and then a device named "DJI USB Virtual COM (COMX)"
	The X should be the number you should use.
	If there is nothing there, the driver from DJI is not installed correctly.
	
	If you have any of the DJI Assistant Software installed, make sure they are not running, as this program
	cannot connect then.
	
* vJoy can't connect
	The error message should tell you if it's installed or not. Install the vJoy driver if it's not there.
	
* Not all sticks or buttons work
	*If they look correct in the log:*
	Your vJoy configuration may be wrong. Open "Configure vJoy" and reset configuration 1, or make a new one
	and tell mDjiController.exe to use that configuration.
	*If they are NOT correct in the log:*
	Your controller sends in a different format, so you need to figure that out, edit the code and recompile. 
	(A bit advanced)

	
