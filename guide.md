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
8. Go to bitwise/blink and create a directory with your intra name.    
NOTE: since there are two arduinos per each raspberry pi we need to specify which: ```/dev/ttyUSB0``` or ```/dev/ttyUSB1```  
then run the following if you are using /dev/ttyUSB0:   
  ```pio run -t upload --upload-port pio@your_pi_ip_address:/dev/ttyUSB0```   
You should get a success message and your arduino should blink. Well done!  
10. Now you can start developing your board and write a program.   

```diff 
! Remember - when working on your breadboard you need to unplug your arduino from the raspberry pi,   
! the cable needs to be detached at the raspberry pi side first!
! And when you plug the data cable back, start with connecting it to arduino and then into the raspberry pi.
```  

# Arduino board development
   We need a guid here...   

# Program your arduino
1. Edit your program on your local machine in src/main.cpp  
2. Once you completed the program on the local machine, you need to synchronise it with your arduino via:   
  ```rsync -avp . pi@your_pi_ip_address:bitworks/your_intra_name --mkpath```   
  this does the following:  
   - This copies your local PlatformIO project to the Raspberry Pi && into ~/bitworks/your_intra_name  
3. Then you need to trigger the upload from the Pi through the following steps:
  ```ssh pi@your_pi_ip_address```  
  ```cd bitworks/your_intra_name```  
  NOTE: Remember which arduino you are using:  
  ```pio run -t upload --upload-port pio@your_pi_ip_address:/dev/ttyUSB0```   
4. And there was the blink! Well done!  

