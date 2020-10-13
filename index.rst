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
- Download and install `<http://thonny.org/>`_
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

============
Example 2 : Reading the state of a push button
============

Introduction
===============
    In this example you are learning how read a digital input from something like a button & use it to turn on and off a LED or any other digital device.
 Learning Outcomes
---------------

From this example, you’ll get an understanding about,

- IF-ELSE conditions
- Variables

Components
------------------
 Magicbit

Theory
---------------
Microcontroller recognizes the signal as 1(HIGH) when the signal is close to 3.3v (or 5v depending on the microcontroller) and recognizes as 0(LOW) when the signal is close to 0v. This reading can be used in the program to do various things.

Methodology
------------------
Magicbit is equipped with two onboard push buttons. Let us select the push button which is wired to D34. Buttons on the board are pulled up internally (to learn more about pullups/pulldowns follow this link), which means when the button is not pressed the status of the button is 1(HIGH), & when the button is pressed the status of the button is 0(LOW).

.. image:: https://github.com/Ruwatech/docu-Magicbit/blob/master/Resources/image7.png?raw=true

Also like in the previous example we need to select a LED to indicate the change, lets select RED LED which is wired to pin D27.

First we set the input output configurations of the Button and the LED using Pin(), in this case button is an INPUT, LED is an OUTPUT. 

Then we can use the variable as the condition of the if block, and if the button is pressed, the bulb should turn on, and the button is not pressed the light should turn off.


Coding
------

 .. code-block:: py

     from machine import Pin

     led = Pin(16, Pin.OUT)
     btn = Pin(34, Pin.IN)

     while True:
          if btn() == 0:
               led.on()
          else:
               led.off() 
Explanation
------------------

**IF/ELSE:** Used to evaluate a digital condition, we can put a digital logic condition in then parenthesis. If the condition is true, it executes the code block immediately below it, if the condition is false it executes the code block in the else block.

 .. code-block:: py

     if (condition)
        # Do if condition is true
     else
        # Do if condition is false

**Note: Write a code to toggle an LED in the button press. LED turns on when button pressed & released, LED turns off when button is pressed & released again. (Hint: Make use of variables to ‘remember’ the state of the button press).**

Example 3: Working with Analog Write
====================================

Introduction
---------------
     In this example you are learning how to turn on and off a LED or any other actuator which can be controlled by a digital output such as relay, bulb, motor.

Learning Outcomes
-------------------
 From this example, you'll get an understanding about,

-  Pulse Width Modulation

Components
------------

- Magicbit

Theory
-----------

To change the brightness of a LED we could change the voltage the LED is supplied with, but in a microcontroller, ability to change the voltage (converting a digital number to an analog voltage) is limited, so a method called PWM (Pulse Width Modulation) is used. What this does is pulsing on and off the pin in a high frequency. The length of the pulses creates the perception of brightness. 

 Duty cycle is a term used to describe the ratio between on and off times.

 .. image:: https://github.com/Ruwatech/docu-Magicbit/blob/master/Resources/image8.png?raw=true

 In this example higher Duty cycle gives higher brightness & lower duty cycle gives lower brightness.

Methodology
-------------
 Lets select green LED (which is wired to D16). We will use a for loop to generate the duty cycle (0 - 0% duty, 255-100% duty). And also to generate 255 cycles.

Coding
------
  .. code-block:: py
    
      from machine import Pin,PWM
      import time
      LED=Pin(16, Pin.OUT)
      pwm = PWM(LED)
      pwm.freq(50)
      while True:
	for i in range (0,256,1):
		pwm.duty(i)
		time.sleep_ms(500)




Explanation
------------
 **for i in range (0,256,1):** There are 3 parameters in a for loop, first parameter we are defining the starting value for the loop. Second parameter specifies the ending value for the loop, third parameter specifies the change happens to the variable in each cycle, in this i is incrementd by one. 

 **pwm.duty(i)** You can input the pin number you need to do pwm and then the pwm value you need to give to that pin. This assigns the corresponding duty cycle to the pin.


**Note This example we have coded to increase the brightness, write a code to do the opposite of that, to fade the brightness of the led, & put both effects together to create a beautiful fade & light up effect.**



Example 4: Reading an Analog Signal
===================================

Introduction
-------------

     In this example you are learning to read an analog sensor.

Learning Outcomes
------------------

 From this example, you'll get an understanding about,

-  Analog Read


Components
-----------

- Magicbit

Theory
-------

 In real world most of the signals we encounter are analog signals (temperature, air pressure, velocity), they are continuous. But computers work on digital domain, to interact between the worlds, representing an analog signal in the digital domain is important. 
 (to read more about analog to digital conversation, follow this link)

Methodology
------------

 For this example we use the potentiometer on the Magicbit board, which is connected to pin, D39. It generates a voltage between 0 and 3.3V according to the angle of the potentiometer. 

 .. image:: https://github.com/Ruwatech/docu-Magicbit/blob/master/Resources/image1.png?raw=true

 We read the analog signal and store it in an int type variable(0v= 0 analog value, 3.3v = 4096 analog value), sensorValue, later, we use this value to light up the  red LED(D27) if the analog value exceeds than 2048.

Coding
------
 .. code-block:: py
    
     from machine import Pin,ADC
     LED=Pin(16,Pin.OUT)
     adc=ADC(Pin(39))
     while True:
        sensorValue=adc.read()
	if sensorValue>2048:
	    LED.off()
	else:
	    LED.on()



Explanation
-----------
 **adc.read():** this reads and assigns the corresponding analog value to the left.

Activity
---------

**Note: Do the same example using the LDR on the board (D36)**

Example 6: Generating Tones
=============================

Introduction
-------------

     In this example you are learning to generate a tone using the onboard buzzer on the Magicbit.

Learning Outcomes
------------------

 From this example, you'll get an understanding about,

-  genearting square waves

Components
-----------

- Magicbit

Theory
-------
 Piezo buzzers are commonly used in embedded systems to give audible tones. It works well with a square wave as input.
 
Methodology
-----------
 For this example we use the piezo buzzer wired to pin 25 of the Magicbit. 

 .. image:: https://github.com/Ruwatech/docu-Magicbit/blob/master/Resources/image2.png?raw=true

Coding
-------
 .. code-block:: py

  from machine import Pin,PWM
  import time
  BUZZER=Pin(25, Pin.OUT)
  while True:
  	BUZZER.on()
        time.sleep_ms(300)
        BUZZER.off()
        time.sleep_ms(300)
    
Explanation
-----------
 There is no function for micropython to generate a square wave to activate the buzzer. Therefore we should create a square wave to replicate the tone function used in   arduino.
 
Activity
--------
**Note:: Create a program that plays one frequency when one push button on the board pressed, and another frequency when the other push button when pressed.**

Example 7: Using the onboard OLED Screen
=========================================

Introduction
------------
     Color OLED screen on Magicbit can display text as well as simple logos & images.

Learning Outcomes
------------------

 From this example, you'll get an understanding about,

-  Using Adafruit OLED library

Components
-----------

- Magicbit

Theory
---------
 Magicbit has a 0.96" OLED Screen which can be communicated with from I2C protocol. The display has the address, **0x3c**.

Methodology
-------------
 Adafruit OLED library(Adafruit_SSD1306) is used to handle the LCD, its important to install those libraries beforehand. First we create the content we need to print onto the screen and then use display.display command to update the screen.

Coding
---------
.. code-block:: py

    from machine import Pin, I2C
    import ssd1306
    from time import sleep

    # Magicbit Pin assignment 
    i2c = I2C(-1, scl=Pin(22), sda=Pin(21))


    oled_width = 128
    oled_height = 64
    oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c)

    oled.text('Hello, World 1!', 0, 0)
    oled.text('Hello, World 2!', 0, 10)
    oled.text('Hello, World 3!', 0, 20)

    oled.show()

Explanation
-----------

 **oled_width , oled_height :** Define the OLED width and height on the following variables:

 **oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c) :** create an SSD1306_I2C object called oled. This object accepts the OLED width, height, and the I2C pins you’ve defined earlier.S1e2n3

 **oled.text():** The text() method accepts the following arguments (in this order):

     - Message: must be of type String
     - X position: where the text starts
     - Y position: where the text is displayed vertically
     - Text color: it can be either black or white. The default color is white and this parameter is optional.
             - 0 = black
             - 1 = white

 **oled.show():** To print on the screen.

**Note:: Make a program to display the ADC value of the potentiometer on the OLED display.** 









Learning Outcomes
===============    


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
  
