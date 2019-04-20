--------------------------------
# Acoustic Sensor Using Raspberry Pi 3
--------------------------------

## This is application development ver 1.1 
## (written by GIANG LE, instructed by GAO CHAO)

This application offers a possibility to turn a Raspberry Pi as a sound device.
The application comes with 2 functions: a sound collector and a test tone generator.

List of Content:
1. Configuration Instruction
2. Installation Instruction
3. Operating Instruction
4. List of Files
5. Copyright/ Copyleft
6. Contact Info
7. Credits and Acknowledgements

--------------------------------

**1. Configuration Instruction**

    This section contains 2 part: hardware configuration and software configuration.

1.1
Hardware configuration 

    + This program is designed for to ultilize a Raspberry Pi 3 with an USB soundcard, a headphone and a 
    microphone, power cable.
    + Ethernet connection is required for saving data to a remote server. 
    + Raspberry Pi 3 onboard sound card doesn’t have microphone interface. 

    We have to change the default audio device to be USB sound card.

    To do this, follow these instructions:
        - Make sure the soundcard and micro phone is plugged in.
        - Use “lsusb” command to check if your USB sound card is mounted.
        - Use “sudo nano /etc/asound.conf” command and put following content to the file
                        pcm.!default {
                        type plug
                        slave {
                        pcm "hw:1,0"
                        }
                        }
                        ctl.!default {
                        type hw
                        card 1
                        }
        - Run "alsamixer" you should be able to see that USB sound card is the default audio device.

1.2 
Software configuration

    - This program require alsa-utils 1.0.25
    - If your system is using the 1.0.28 version, it is recommended to downgrade to the 1.0.25 version 
    in order to avoid bugs.

    To downgrade alsa-ultis, follow these instructions:
            - Use “sudo nano /etc/apt/sources.list” command and add the last line.
            - Run “sudo apt-get update.
            - Run “sudo aptitude versions alsa-utils” to check if version 1.0.25 of alsa-util is 
            available.
            - Run “sudo apt-get install alsa-utils=1.0.25-4” to downgrade.
            - Reboot (if necessary).

    To make sure alsa-ultils installation was ready:
            - Run “arecord -r44100 -c1 -f S16_LE -d5 test.wav” to test that your microphone is working. 
            You should see a “test.wav” file in the current folder.
            - Put earphone on. Run “aplay test.wav” to check that your recording is okay.

    This program also requrie libcurl library
       To install libcurl, follow these instructions:
            - First use command “ls /usr/include/curl” to identify that /usr/include/curl/ folder exists 
            or not.
            - If the folder doesn’t exist. Run “sudo apt-get update” to update the application list.
            - Run “sudo apt-get install libcurl3” to install the libcurl3.
            - Run “sudo apt-get install libcurl4-openssl-dev” to install the development API of libcurl4.


**2. Installation instruction**

        - Install the latest NOOBS version for Raspberry Pi.
        Get it at https://www.raspberrypi.org/downloads/noobs/
        - Set the external USB sound card as Default
        - Fix the bug of arecord by downgrade the alsa-utils from 1.0.28 to 1.0.25
        - Install libcurl and its development API

    The source code can be obtain from github by the command: 
    git pull https://github.com/Midnightlight/Raspberry_AppDev
    Once the source code has been downloaded, open the file comm.h to edit the url to your own receiving 
    php file: #define SERVER_URL your_url_here
    Then use the command make to automatically compile the program: make
    Run the program from the file wave.a as followed: ./wave.a your_device_name

**+ RPi Default Booting & Keyboard Layout**

    1. By default Raspberry Pi boots into X-server (graphic) mode. This increases booting time, but in 
    most cases we don't use a display with Raspberry Pi, so the first thing is to disable it. 
    To do so, you need to connect RPi to a display via HDMI-DIV cable.
    2. You also need a USB keyboard for this step. Connect it to your Raspberry Pi.
    3. Once booted, open a "terminal" window (Ctrl + ESC, and choose from the "Accessories")
    4. Run "sudo raspi-config" command.
    5. Select from "boot options": "Text console, auto-login".
    6. The newer version of Raspbian disables SSH by default, therefore you have to enable it. 
    Navigate to "Interfacing Options" and select "SSH", choose "Yes", Select "Ok".
    7. You can change the keyboard to be "Generic 105 key/Finnish" in "4. Internationalization Options".
    8. Reboot "sudo reboot"


**+ Send IP Address by Email** 

    1. When using Raspberry Pi remotely, you need to know its IP address to connect to it. There are many 
    ways to get the IP address from your Pi. The simplest way to edit "rc.local" file.
    2. First you need to get a digital signature of your student ID. Please run following command: 
    pi@raspberrypi:~ $ curl --url "http://www.cc.puv.fi/~gc/php/sha_stuID.php" -d "id=e1700346"
    And you will get:
    welcome to SHA-1 hashing function
    Your ID : e1700346
    SHA hash of your ID: c040f7cde553dc1739ff9b6eebcb1d6f994ce3cb
    3. Copy the SHA string to clipboard 
    (in Putty window, Ctrl + "Insert" to copy, Shift + "Insert" to paste) 
    and run command .sudo nano /etc/rc.local. and add following lines:
    
    #Print the IP address
    sleep 30
    _IP=$(hostname -I) || true
    if [ "$_IP" ]; then
    printf "My IP address is %s\n" "$_IP"
    curl --url http://www.cc.puv.fi/~gc/php/sendMailRPi.php -d .email=gc@vamk.fi&from=e1700346&hash=YOURHASH.
    curl --url http://www.cc.puv.fi/~gc/php/rasp.php -d "ip=$_IP&name=e1700346"
    curl --url http://www.cc.puv.fi/~juma/raspi/rasp_ip.php -d "auth=mckdoe03&name=e1700346&ip=$_IP"
    fi
    exit 0
            
    4. The line .sleep 30. is to guarantee that IP address is available.
    5. The 1st "curl" command sends IP address to your mail box (please change "email" to your email) using 
    a PHP program. 
    The program will verify your ID and signature so please make sure they are correct.
    6. The 2nd "curl" command sends IP address to GC.s PHP page and you can see your device name/IP on 
    http://www.cc.puv.fi/~gc/php/rasp.php. 
    7. The 3rd .curl. command sends IP address to Jukka Matila.s PHP page and you can see your device in his 
    page: http://www.cc.puv.fi/~juma/raspi/. 


**+ Install USB sound card as default audio device**

    1. Install alsamixer using command "sudo apt-get install alsa".
    2. Boot up RPi, and apply the USB sound card.
    3. RPi onboard sound card does not have microphone interface. We have to change the default audio 
    device to be USB sound card.
    4. Use command "lsusb" to check if your USB sound card is mounted.
    5. Use "sudo nano /etc/asound.conf" command and put following content to the file:
                    pcm.!default {
                    type plug
                    slave {
                    pcm "hw:1,0"
                    }
                    }
                    ctl.!default {
                    type hw
                    card 1
                    }
    6. Go to home directory. Use "nano .asoundrc" command and put the same content to the file.
    7. Run "alsamixer" you should be able to see that USB sound card is the default audio device.
    For a more sensitive sound detection, it is better to maximize the volume of "Mic".


**+ Install libcurl library**

    1. First use command "ls/usr/include/curl" or "ls/usr/include/arm-linux-gnueabihf/curl" to identify 
    that libcurl library is installed
    2. If the folder doesn't exist. Run "sudo apt-get update" to up-date the application list.
    3. Run "sudo apt-get install libcurl3" to install the libcurl 3.
    4. Run "sudo apt-get install libcurl4-openssl-dev" to install the development API of libcurl 4.


**+ Adding files to your Github**
    ***- First setup -***
    
    1. Create a respository on Github with "your respository name".
    2. Go to your directory that you want to remote to Github on Linux.
    3. Use command "echo "# your respository name" >> README.md".
    4. Use command "git init".
    5. git add README.md
    6. git commit -m "first commit"
    7. git remote add origin https://github.com/your username/your respository name.git
    8. git push -u origin master

***- Uploading files -***

    1. Use command line "git add" + your filenames that you want to upload.
    2. Use "git status" to make sure it has been added for committing.
    3. Use "git commit -m" + "your commit".
    4. Use "git push origin master -u".
    5. Login to your account and check the pushed files on your Github page.


**3. Operating Instruction**

        - Run command "make" to build the project.
        - Run command "./sound.out" to run the project. 
        
3.1 Run a program that records the frequency and peaks from the sound card.
        
        1. Prepare all the files from this resporitory into your Raspberry Pi's directory.
        2. Connect a sound card including a microphone.
        3. Run the command "make". Notice that there are .o files created.
        4. Run the command "./sound.out" 
        You will see the columns which display the recorded sound.
        You can also open "testcurl.txt" for accessing the recorded results.
        5. Clap into the microphone and notice that the peak value recorded every 1 minute.
        6. See your frequency recorded on the .php site.

        - To delete execution file, to command "make clean".
        - The recorded data is also sent to school server for storage.
        
3.2 Run a program that generates sound based on the frequency value the user enters.

        1. Prepare all the files from this resporitory into your Raspberry Pi's directory.
        2. Run the command "make". Notice that there are .o files created.
        3. Run the command "./sound.out" + frequency wanted to generate **from 30 to 16000Hz**
        4. Choose how many channels (1 for mono / 2 for stereo).
        5. Choose how long is the sound generated. (from 1 to 10 seconds).
        6. Run command "scp testTone.wav user@host.com:/your directory"
        7. Go to your destinated directory and use headphone to check out the testTone.wav sound 
        with the chosen frequency and channels.


**4. List of Files**

	- README : this file
	- comm.c : the communication part of the project
	- comm.h : the header file of comm.c
	- main.c : contains the main() function
	- makefile : the makefile of the project
	- screen.c : the displaying part of the project
	- screen.h : the header file of screen.c
	- sound.c : the sound analyzing part of the project
	- sound.h : the header file of the sound.c
	- testcurl.c : the communication testing module


**5. Copyright** 

    This project was created by GIANG LE (e1800927).


**6. Contact Info** 

    Name: GIANG LE
    Email: vegiangle2602@gmail.com


**7. Credits and Acknowledgements**

7.1
Credits
    
    - Author: GIANG LE - e1800927 (VAMK)
    - Instructions by Dr. GAO CHAO - Principal Lector (VAMK) (http://www.cc.puv.fi/~gc/newhome/index.html)
    - Equipment provided by Vaasa University of Applied Sciences.
    
7.2
Acknowledgements
    
    - Basic knowledge of how to create a project on Raspberry Pi/Linux system.
    - Basis of developing an application for a sound sensor of an LED light (switching on/off by clapping).
    - Creating an application that generates different tones in Linux.
    
    
