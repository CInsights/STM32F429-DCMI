# STM32F429-DCMI usage example code

This program is made for a STM32F429 discovery board AND OV9655 camera. The demo program samples a 320x240px image from a OV9655 camera into the SRAM and encodes it into JPEG. It then transmits the image by serial to the computer where it can be displayed. The STM32F429 discovery board has actually external SDRAM but the project's goal is it, to solve this problem without any external SDRAM.

**Anvantages:** No external memory needed, small capture outputs, 1/80sec shutter time<br>
**Disadvantages:** No VGA possible (only QVGA)

![Demo capture](https://raw.githubusercontent.com/DL7AD/STM32F429-DCMI/master/example.jpg)

Demo capture taken by STM32F429 with OV9655

![Demo capture](https://github.com/DL7AD/STM32F429-DCMI/blob/master/stm32f4_ov9655.jpg)

STM32F429 discovery board connected to Omnivision OV9655


Code sources
------------
- DCMI example http://mikrocontroller.bplaced.net/wordpress/?page_id=1115
- JPEGant http://sourceforge.net/projects/jpegant.berlios/
- To make this demo work ChibiOS is needed https://github.com/ChibiOS/ChibiOS

Hardware recommondations
------------------------
*ST STM32F429 discovery board*
- Datasheet disco board: http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00093903.pdf
- Datasheet Microcontroller: http://www.st.com/web/en/resource/technical/document/datasheet/DM00071990.pdf
- Reference Manual: http://www.st.com/web/en/resource/technical/document/reference_manual/DM00031020.pdf

*Omnivision OV9655 camera*
- Datasheet: http://www.waveshare.com/w/upload/0/0a/OV9655.pdf

Hardware connections
--------------------
The STM32F429 discovery board must be connected to the camera to spectific pins

Camera | Disco-Board   | _Notes_
------ | ------------- | -------
3.3V   | VDD           | Disco board supplies 3.0V but that's OK
GND    | GND           |
SIOC   | PB10          | I2C CLK
SIOD   | PB11          | I2C SDA
VSYNC  | PB7           |
HREF   | PA4           |
PCLK   | PA6           |
XCLK   | PA8           | Camera clock input (Generated by STM32)
D9     | PE6           | Data pin
D8     | PE5           | Data pin
D7     | PB6           | Data pin
D6     | PE4           | Data pin
D5     | PE1           | Data pin
D4     | PC8           | Data pin
D3     | PC7           | Data pin
D2     | PC6           | Data pin
RET    | _unconnected_ | Reset pin (clears all registers)
PWDN   | _unconnected_ | Power down

Installation/Building/Flashing
------------------------------
To be able to build this project, a modification in the ChibiOS submodule must be done:
- Make sure you have a GCC toolchain installed (http://www.wolinlabs.com/blog/linux.stm32.discovery.gcc.html)
- The compile it with **make**
- And then flash the STM32 with **make flash** (You probably have to adjust the variable **STLINK** in the Makefile)

Taking photos
-------------
- The programm initializes the camera once at startup by I2C.
- The programm will take a photo from the camera and transmit the encoded picture by UART on PD5. The red LED on the demoboard will light up while taking the picture.
- Thereafter the green LED on the discovery board will blink green to signal, that the board is idling.

Author
------
sven.steudte@gmail.com
