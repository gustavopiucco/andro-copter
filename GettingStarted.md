The documentation is still incomplete for now, but it should be more precise soon.

# Required material #
  * A recent Android phone, that features a gyroscope. For the moment, only the Nexus 4 has been tested.
  * The Arduino ADK ("Accessory development kit").
  * A working quadcopter powertrain:
  * 4 brushless motors.
  * 4 ESCs ("electronic speed controllers") that take a PPM signal as input.
  * A battery (ideally 3S).
  * A chassis to hold all this together.
  * A laptop.
  * A gamepad. Only the XBox 360 gamepad has the correct binding for now, but you can change it easily in the source code, to suit your controller.

# Wiring #
Follow this schematic:
![http://andro-copter.googlecode.com/svn/trunk/Hardware/wiring.png](http://andro-copter.googlecode.com/svn/trunk/Hardware/wiring.png)
![http://andro-copter.googlecode.com/svn/trunk/Hardware/propellers_directions.png](http://andro-copter.googlecode.com/svn/trunk/Hardware/propellers_directions.png)

# Building the Android app and the PC software #
Checkout the SVN repository. You should get four directories...more info on the compilation later.

## AndroCopter for Android ##
  * Install Eclipse with ADT (http://developer.android.com/sdk/index.html).
  * Start Eclipse.
  * Go to File > Import > Existing Projects into Workspace. Then set the root directory (andro-copter/Android/
  * Import the Android project (in andro-copter/Android).
  * Wait for the compilation to end.
  * To send the app to the phone: Run As > Android Application.

## AndroCopter Remote for PC ##
  * Install Qt Creator and the Qt 5 library (http://qt-project.org/downloads).
  * Install the SFML 2.3 library (http://www.sfml-dev.org/download.php).
  * Open the project into Qt Creator.
  * Set the pathes in the file AndroCopter.pro (lines 34 and 35), to match your actual SFML installation path.
  * Compile and Run.

## Arduino sketch ##
  * Install the Arduino IDE (http://arduino.cc/en/Main/Software), and the ADK libraries (http://developer.android.com/tools/adk/adk.html).
  * Open the Arduino sketch, and Upload it.

# Fly #

## Wireless connection ##
  * Option 1: share the smartphone internet connection. Even if the Android phone is not connected to the internet, you can use this feature. Go to Settings > More... > Connection sharing > Wi-Fi access point. Connect the PC to this Wi-Fi network.
  * Option 2: create an access point on the computer, and connect the Android phone to it. Note that some network card do not support this.
  * Option 3: use an existing Wi-Fi network. Note that this is less practical outside, and the latency may be higher.

## Start AndroCopter Remote ##
Before starting AndroCopter Remote, be sure that the PC and the Android phone are on the same network, and that the gamepad is plugged into the PC. Then start it.
In the "Smartphone connection" box, you will find the IP address of the computer.

## Start AndroCopter on the phone ##
Power on the Arduino by connecting it to the battery. Do not power the powertrain for now. Then connect it to the phone. A popup should appear, to suggest starting the AndroCopter application. Accept. You can check the box to start AndroCopter automatically, when the ADK is plugged.
Uncheck the "Connect to PC" box, then enter the IP address of the computer. Check "Connect to PC".
The application on the PC should display "Connected to ...", and receive the states data.
Secure the phone to the quadcopter, and be sure that the quadcopter is horizontal on the ground.

## Test that the communication is good ##
Push the "Reset orientation button" to set the current orientation(yaw, pitch and roll) as the reference. Check the "Regulators ON" checkbox. Move the stick, and check that the sliders are moving accordingly. If everything is OK, uncheck the box, then connect the battery to the ESCs.

## Fly ##
Tick the "Regulators ON" checkbox again, and increase the trottle slowly.
![http://andro-copter.googlecode.com/svn/trunk/Hardware/xbox_gamepad_layout.png](http://andro-copter.googlecode.com/svn/trunk/Hardware/xbox_gamepad_layout.png)

## Control states ##
As long as the "Regulators ON" is unchecked, the propeller will remain stopped. The motors will also remain stopped if the thrust slider is at the minimum (zero). But if the thrust is higher than zero, the regulators output may make the propellers spin, so be careful (it can happen when the quadcopter is on the ground, but turned 180° from the reference, so it will try strongly to reach this position).

# PID tuning #
These are the current values I use for my 1300g quadcopter:
  * Yaw: Kp=3, Ki=0; Kd=0.
  * Pitch: Kp=0.5, Ki=0.1; Kd=0.15.
  * Roll: Kp=0.5, Ki=0.1; Kd=0.15.
Changing the PID coefficients in-flight is possible, but not recommended. Always be ready to hit the emergency stop button, in case the quadcopter would become unstable.
Protecting the propellers will make the tuning phase safer. Extended arms, like the Project Home picture, will avoid that the propellers hit the ground.