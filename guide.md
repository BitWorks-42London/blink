# Platformio installation guide

# Raspberry Pi/Arduino connection, project setup   
1. cd to sketches directory/blink and create a new repo:
   ```mkdir your_intra_name; cd $_```
2. Create a new embedded development project with PlatformIO via the pio command-line tool and specify which tool would you like to use - vim or vscode:   
  if vim:  
    ```pio project init --board nanoatmega328new --ide vim --sample-code```     
  if vscode:   
    ```pio project init --board nanoatmega328new --ide vscode --sample-code```     
3. Approve the project initalisation - congrats. you have created your first PlatfromIO project!
4. Got your src/main.cpp and copy in syntax from the following source: https://docs.platformio.org/en/latest/core/quickstart.html
5. Go to your public key and copy the content
6. Save your public key under the list of existing keys in .ssh/authorised_keys file
7. Log into your raspberry pi via ssh
  ```ssh pi@your-pi-ip-address```
8. Go to bitwise/blink and create a directory with your intra name;    
NOTE: since there are two arduinos per each raspberry pi we need to specify which: ```/dev/ttyUSB0``` or ```/dev/ttyUSB1```  
then run the following for example:
  ```pio run -t upload --upload-port pio@192.168.1.42:/dev/ttyUSB1```   
You should get a success message and your arduino should blink. Well done!  
10. Now you can start developing your board and programming. Remember - always unplug arduino first!  

# Arduino board development

# Program your arduino
1. Edit your program on your local machine in src/main.cpp  
2. Once you completed the program on the local machine, you need to synchronise it with your arduino via:   
  ```rsync -avp . pi@your_pi_ip_address:bitworks/your_intra_name --mkpath```
  this does the following:
   - This copies your local PlatformIO project to the Raspberry Pi && into into ~/bitworks/your_intra_name  
3. Then you need to trigger the upload from the Pi through the following steps:
  ```ssh pi@your_pi_ip_address```  
  ```cd bitworks/your_intra_name```  
  ```pio run -t upload --upload-port pio@192.168.1.42:/dev/ttyUSB1```
4. And there was the blink! Well done!  

