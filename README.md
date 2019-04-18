--------------------------------
<<<<<<< HEAD
# Acoustic Sensor using Raspberry Pi 3
--------------------------------

## This is application development ver 1.1
=======
# Acoustic Sensor using RPi3
--------------------------------

## This is application development ver 1.1 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
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
<<<<<<< HEAD
Hardware configuration

    This program is designed for to ultilize a Rasperry Pi 3 with an USB soundcard and a microphone.
    Ethernet connection is required for saving data to a remote server.
    RPi onboard sound card doesn’t have microphone interface.
=======
Hardware configuration 

    This program is designed for to ultilize a Rasperry Pi 3 with an USB soundcard and a microphone. 
    Ethernet connection is required for saving data to a remote server. 
    RPi onboard sound card doesn’t have microphone interface. 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
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

<<<<<<< HEAD
1.2
Software configuration

    - This program require alsa-utils 1.0.25
    - If your system is using the 1.0.28 version, it is recommended to downgrade to the 1.0.25 version in
    order to avoid bugs.

 To downgrade alsa-ultis, follow these instructions:
=======
1.2 
Software configuration

    - This program require alsa-utils 1.0.25
    - If your system is using the 1.0.28 version, it is recommended to downgrade to the 1.0.25 version in 
    order to avoid bugs.

    To downgrade alsa-ultis, follow these instructions:
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
            - Use “sudo nano /etc/apt/sources.list” command and add the last line.
            - Run “sudo apt-get update.
            - Run “sudo aptitude versions alsa-utils” to check if version 1.0.25 of alsa-util is available.
            - Run “sudo apt-get install alsa-utils=1.0.25-4” to downgrade.
            - Reboot (if necessary).
<<<<<<< HEAD

    To make sure alsa-ultils installation was ready:
            - Run “arecord -r44100 -c1 -f S16_LE -d5 test.wav” to test that your microphone is working.
=======
            
    To make sure alsa-ultils installation was ready:
            - Run “arecord -r44100 -c1 -f S16_LE -d5 test.wav” to test that your microphone is working. 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
            You should see a “test.wav” file in the current folder.
            - Put earphone on. Run “aplay test.wav” to check that your recording is okay.

    This program also requrie libcurl library
        To install libcurl, follow these instructions:
<<<<<<< HEAD
            - First use command “ls /usr/include/curl” to identify that /usr/include/curl/ folder exists
=======
            - First use command “ls /usr/include/curl” to identify that /usr/include/curl/ folder exists 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
            or not.
            - If the folder doesn’t exist. Run “sudo apt-get update” to update the application list.
            - Run “sudo apt-get install libcurl3” to install the libcurl3.
            - Run “sudo apt-get install libcurl4-openssl-dev” to install the development API of libcurl4.


**2. Installation instruction**

<<<<<<< HEAD
        - Install the latest NOOBS version for Raspberry Pi.
=======
        - Install the latest NOOBS version for Raspberry Pi. 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
        Get it at https://www.raspberrypi.org/downloads/noobs/
        - Set the external USB sound card as Default
        - Fix the bug of arecord by downgrade the alsa-utils from 1.0.28 to 1.0.25
        - Install libcurl and its development API

<<<<<<< HEAD
 The source code can be obtain from github by the command:
    git pull https://github.com/Midnightlight/Raspberry_AppDev
    Once the source code has been downloaded, open the file comm.h to edit the url to your own receiving
=======
    The source code can be obtain from github by the command: 
    git pull https://github.com/Midnightlight/Raspberry_AppDev
    Once the source code has been downloaded, open the file comm.h to edit the url to your own receiving 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
    php file: #define SERVER_URL your_url_here
    Then use the command make to automatically compile the program: make
    Run the program from the file wave.a as followed: ./wave.a your_device_name


**3. Operating Instruction**

        - Run command "make" to build the project.
<<<<<<< HEAD
        - Run command "./sound.out" to run the project.
=======
        - Run command "./sound.out" to run the project. 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
        You will see the columns which display the recorded sound.
        - You can also open "testcurl.txt" for accessing the recorded results.
        - To delete excution file, to command "make clean".
        - The recorded data is also sent to school server for storage.


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
<<<<<<< HEAD
	      - sound.php : the data receiving page
        - testcurl.c : the communication testing module


**5. Copyright**
=======
        - sound.php : the data receiving page
        - testcurl.c : the communication testing module


**5. Copyright** 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7

    This project was created by GIANG LE (e1800927).


<<<<<<< HEAD
**6. Contact Info**
=======
**6. Contact Info** 
>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7

    Email: vegiangle2602@gmail.com


**7. Credits and Acknowledgements**

<<<<<<< HEAD
    - Author: GIANG LE (e1800927) (VAMK)
    - Instructor: Mr.GAO CHAO (VAMK)


=======
    - Author: GIANG LE (e1800927) (VAMK) 
    - Instructor: Mr.GAO CHAO (VAMK)

>>>>>>> f65828e7b0045208e1e19c4760a0c088c1e990a7
