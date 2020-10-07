==
.. image:: https://github.com/magicbitlk/Magicbit-MicroPython/raw/master/Resources/micropython.png


MicroPython is a lean and efficient implementation of the Python 3 programming language that includes a small subset of the Python standard library and is optimised to run on microcontrollers and in constrained environments.
`Learn more about MicroPython <https://micropython.org/>`_

Magicbit is based on ESP32 which in supported by `MicroPython <http://docs.micropython.org/en/latest/esp32/quickref.html>`_ and `muEditor <https://codewith.mu/>`_

================
Getting Started
==============

*************************
Installation Instructions
*************************
- Download and install `https://thonny.org/`
- Open the Magicbit Utility and connect the Magicbit Board to the PC
- Choose the port connected to the device and choose Micropython as the platform
- Click 'Update Firmware'
- Open Thonny IDE 
- Click Run > Select Interpreter
- Choose Micropython(ESP32) from the first dropdown box and leave the other dropdown box as it is.

***********
Powering Up
***********
     Magicbit can be powerup by either connecting USB cable or connecting battery. For programming USB cable must be connected to the computer. For the first time powering up Magicbit self test program will be running on the magicbit and you can see the features available and functional tests on Magicbit display.       

To check whether drivers are correctly installed open the Ardunio IDE and go the Tools menu. There should be a port (Eg:COM1) shown when plugging Magicbit to the computer as shown below. If not please follow Installation drivers section.


********************
Installation Drivers (Optional)
********************

Magicbit has CH340 chip as USB-Serial converter which driver already packaged with Ardunio IDE. If port not shown in the Arduino as shown below please install `driver <https://github.com/magicbitlk/Magicbit-Arduino/blob/master/Resources/CH34x_Install_Windows_v3_4.EXE>`_


*************
First Project
*************

- Open Thonny IDE
- Paste following code on editor and click save as
.. code-block:: python

     from machine import Pin
     import time
     led = Pin(16, Pin.OUT)
     for i in range(10):
          led.on()
          time.sleep_ms(500)
          led.off()
          time.sleep_ms(500)
- Click 'Micropython Device' and choose file name as 'boot.py'
-Click Run (Green Arrow) on the IDE
- If Green Led on backside of the Magicbit is blinking your have just begun the magic with Magicbit

========
Hardware
========

Brain of the magicbit is ESP32, which is a series of low-cost, low-power system on a chip microcontrollers with integrated Wi-Fi and dual-mode Bluetooth. Therefore any project or document available on internet which supports ESP32 is supported for Magicbit as well.

**************
Specifications
**************
- **Processor** - Xtensa dual-core
- **Speed**- Up to 240Mhz
- **Flash Memory**-4MB
- **Ram**-520KB
- **Inputs**-Pushbutton, LDR, Potentiometer
- **Outputs**-LEDs, OLED Display, Buzzer
- **Other**- Dual Motor Driver, Li-Ion Charger
- **Connectivity**- USB, WiFi, Bluetooth

*****************
Features
*****************
.. image:: https://github.com/magicbitlk/Magicbit-Arduino/raw/master/Resources/Layout.png

***************
Pinmap
***************

.. image:: https://github.com/magicbitlk/arduino-esp32/raw/master/docs/pinout.png

***********
Accessories
***********

=========================
MicroPython Documentation 
=========================

Detailed documentation about functions and usage can be found in original `MicroPython documentation <https://docs.micropython.org/en/latest/esp32/quickref.html>`_
  
