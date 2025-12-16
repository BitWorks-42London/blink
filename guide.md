# Platformio installation guide
   We need a guide here...   
   
# Raspberry Pi/Arduino connection, project setup  
1. On your local machine create a directory sketches/blink/your_intra_name:  
   ```mkdir -p sketches/blink/your_intra_name; cd $_```   
2. Create a new embedded development project with PlatformIO via the pio command-line tool and specify which tool would you like to use - vim or vscode:   
  - if vim:  
    ```pio project init --board nanoatmega328new --ide vim --sample-code```     
  - if vscode:   
    ```pio project init --board nanoatmega328new --ide vscode --sample-code```     
3. Approve the project initalisation - congrats. you have created your first PlatfromIO project!
4. Got your src/main.cpp and copy in syntax from the following source: https://docs.platformio.org/en/latest/core/quickstart.html#codecell4   
5. Go to your public key and copy the content
6. Log into your raspberry pi via ssh, the password is: 123456   
  ```ssh pi@your-pi-ip-address```
7. Save your public key under the list of existing keys in .ssh/authorised_keys file  
   Now you will be able to log in without the password.  
8. Go to bitworks/blink and create a directory with your intra name.    
NOTE: since there are two arduinos per each Raspberry Pi we need to specify which: ```/dev/ttyUSB0``` or ```/dev/ttyUSB1```  
then run the following if you are using /dev/ttyUSB0:   
  ```pio run -t upload --upload-port pio@your_pi_ip_address:/dev/ttyUSB0```   
You should get a success message and your arduino should blink. Well done!  
10. Now you can start developing your board and write a program.   

```diff 
! Remember - when working on your breadboard you need to unplug your Arduino from the Raspberry Pi,   
! the cable needs to be detached at the Raspberry Pi side first!
! And when you plug the data cable back, start with connecting it to the Arduino and then into the Raspberry Pi.
```  

# Arduino board development
1. Arduino board pinout:   
![pinout.png](https://lastminuteengineers.com/wp-content/uploads/arduino/Arduino-Nano-Pinout.png)   

2. In your kit you have:  
- Arduino Nano  
- yellow jump Dupont wire    
- 5 red mini jump wires, 3 red long jump wires, 3 blue medium jump wires  
- button  
- diode   
- 2 resistors  
- breadboard  

3. Kit item description:
 - The Arduino Nano is a small, versatile, open-source microcontroller board based on the ATmega328P.  
 - yellow Dupont wire connector used for prototyping and electronic projects.
 - jump wires - same as the Dupont wire, easy to connect and disconnect, convenient for insertion into your breadboard.  
 - button will allow you to test whether the program you wrote performs as it should - diode blinks or switches off.  
 - diode is a light bead.  
 - resistors are fundamental passive components that limit electrical current flow, divide voltages, and adjust signal levels in circuits, measured in Ohms (Ω).  
 - a breadboard is a reusable, solderless platform for building and testing temporary electronic circuits, featuring a grid of holes with internal metal clips that connect components like resistors, LEDs, and jumper wires, making it ideal for prototyping and education before creating permanent circuits.   

 4. The anatomy of a breadboard
 <img src="https://cdn.sparkfun.com/assets/3/d/f/a/9/518c0b34ce395fea62000002.jpg" width="600" height="600">  
 Aside from horizontal rows, breadboards usually have what are called power rails that run vertically along the sides.   
 These power rails are metal strips that are identical to the ones that run horizontally, except they are, typically*, all connected.   
 When building a circuit, you tend to need power in lots of different places. The power rails give you lots of easy access to power  
 wherever you need it in your circuit. Usually they will be labeled with a ‘+’ and a ‘-’ and have a red and blue or black stripe,  
 to indicate the positive and negative side.
 It is important to be aware that the power rails on either side are not connected, so if you want the same power source on both sides,   
 you will need to connect the two sides with some jumper wires. Keep in mind that the markings are there just as a reference.  
 There is no rule that says you have to plug power into the '+' rail and ground into the '-' rail, though it's good practice to keep everything in order.  
 

 5. Overview of connecting individual parts onto the breadboard:
 - Arduino needs to be placed exactly in the middle of the horizontal rails, joining the two unconnected parts of the breadboard.  
 - We need to find the ground pin && use the blue wire to connect it to the negative vertical rail.
 - We need to input diode, the longer leg always facing the Arduino.  
 - We need to identify the Arduino pin which is responsible for providing the power, and connect the jellow jumper Dupont wire  
 between that pin and the shorter leg of the diode.
 - The button needs to be placed exactly in the middle, just like we have done it with the Arduino.    
 - Now, we need to identify the general-purpose I/O pin on the Arduino used for input/output. We need to use the red, long jumper wire  
 between that pin and the button upper leg (the leg closer to the Arduino).  
 - We also need to use a resistor, in the exact same pin (Arduino general purpose I/O) && connect it to the negative vertical rail of the breadboard.
 - Another step is to identify the RESET pin on the Arduino && use the red wire to connect it to the lower leg of the button (further away from the Arduino).  
 
# Program your Arduino
1. Edit your program on your local machine in src/main.cpp  
2. Once you completed the program on the local machine, you need to synchronise it with your arduino via:   
  ```rsync -avp . pi@your_pi_ip_address:bitworks/your_intra_name --mkpath```   
  this does the following:  
   - Copies your local PlatformIO project to the Raspberry Pi && into ~/bitworks/your_intra_name  
3. Then you need to trigger the upload from the Raspberry Pi through the following steps:
 - ```ssh pi@your_pi_ip_address```
 -  ```cd bitworks/your_intra_name```  
NOTE: Remember which Arduino you are using:  
 -  ```pio run -t upload --upload-port pio@your_pi_ip_address:/dev/ttyUSB0```   
4. And there was the blink! Well done!  

