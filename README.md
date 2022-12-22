# Simple-Led-Matrix-Clock-With-Physical-Switch

![Screenshot (647)](https://user-images.githubusercontent.com/118633170/209058019-35986a05-e55f-46dd-92a8-7d385d8290a8.png)


If you have hard-time 3d printing stuff and other materials which i have provided in this project please refer the professionals for the help, [JLCPCB](https://jlcpcb.com/RNA) is one of the best company from shenzhen china they provide, PCB manufacturing, PCBA and 3D printing services to people in need, they provide good quality products in all sectors

[JLCPCB](https://jlcpcb.com/RNA)


Please use the following link to register an account in [JLCPCB](https://jlcpcb.com/RNA)

https://jlcpcb.com/RNA


Pcb Manufacturing

----------

2 layers

4 layers

6 layers

jlcpcb.com/RNA



PCBA Services

[JLCPCB](https://jlcpcb.com/RNA) have 350k+ Components In-stock. You don’t have to worry about parts sourcing, this helps you to save time and hassle, also keeps your costs down.

Moreover, you can pre-order parts and hold the inventory at [JLCPCB](https://jlcpcb.com/RNA), giving you peace-of-mind that you won't run into any last minute part shortages. jlcpcb.com/RNA



3d printing

-------------------

SLA -- MJF --SLM -- FDM -- & SLS. easy order and fast shipping makes [JLCPCB](https://jlcpcb.com/RNA) better companion among other manufactures try out [JLCPCB](https://jlcpcb.com/RNA) 3D Printing servies

[JLCPCB](https://jlcpcb.com/RNA) 3D Printing starts at $1 &Get $54 Coupons for new users

In this project/tutorial, we are going to discuss how we can build a simple yet very helpful device in managing our lives, a digital clock. While there are digital clocks nowadays that you can set by just connecting to the internet, I decided to use a real-time clock (RTC) because: (1) Obviously, it operates even without internet connection. (2) It is inexpensive. (3) It consumes very little amount of power. (4) and so that we can see how it works. This is going to be a very long tutorial so we are going to split this into three parts. In this part, we will discuss the hardware, in the second part the software, and in the last part we will test the digital clock. So now, let’s check first the components that we need to create a digital clock

MAX7219 LED matrix, the time, picked with NTP from web, and every 30 seconds shows the temperature and the humidity measured by the DTH11 sensor. The display light also changed based on the light that the photoresistor measures so even if it's day or night you can read time and temperature properly.

I decided to make a beautiful animated (flip) clock with big digits, which is synchronized over the Internet. The basis for my project was the code of Pawel A. Hernik from which I removed the part that shows the weather information and currency rate. I did this to make the code as simple as possible and more understandable.I also made the following changes to adjust to my project:

- Display of 7 instead of 6 matrices

- Clock and seconds blinking dots are moved for 4 LEDs to the right

- Texts "connecting" and "getting data" are displayed in the middle of the screen

- An increased period of time between two data collections from a server

- UTC offset changed to "1" for my country

We must first install the ESP8266 board on Arduino IDE, and then upload the code on the appropriate board and port. The code cannot be compiled on the latest version of the ESP board (2.5.0), so we must install an older version (2.4.2).

1. ATmega328P-PU, 28-pin IC Socket, 2pcs. 0.1uF Ceramic Capacitors, 16MHz Crystal, 2pcs. 22pF Ceramic Capacitors, 10kΩ Resistor (Minimal/Standalone Arduino Uno)

2. DS3231 Precision Real-Time Clock (RTC) Module

3. 2pcs. 4-in-1 MAX7219 Dot Matrix LED Display Module (Female-to-Female Jumper Wires included)

4. 5pcs. 12mm Tactile Switches

5. 2N3904 BJT & 1kΩ Resistor

6. 2pcs. 470uF Electrolytic Capacitors

7. Male and Female Headers

The DS3231 is an I2C RTC device that maintains accurate timekeeping even when main power is interrupted by incorporating a backup battery. It maintains seconds, minutes, hours, day, date, month, and year information as long as the backup battery is in good condition. If the backup battery is removed when main power is not present, the time and date will be reset to its default values so you will need to set it again.

So the main components for this digital clock are the minimal Arduino Uno (standalone Arduino Uno), DS3231 RTC module, and the MAX7219 dot matrix LED display modules. With these three components, we can already display the time and date. However, we won’t be able to set the clock’s time and date unless we reprogram the microcontroller (MCU) again. So I’ve added tactile switches so that we can set the time and date without reprogramming the MCU and other components to make the digital clock stable. Now, let’s check the hardware connections.

![Screenshot (648)](https://user-images.githubusercontent.com/118633170/209058206-a5b4bba0-a10f-4658-8c35-36a9e00bd24b.png)
![Screenshot (649)](https://user-images.githubusercontent.com/118633170/209058212-2cd3a625-54e6-4962-8920-c3e71ead7e91.png)


So this is the DS3231 RTC module that I used. It’s very common and you can easily purchase it online. The bigger IC in the image is the DS3231 and the smaller IC below it is the AT24C32 which is an EEPROM in case you need to store some values. Good thing about this module is that you don’t need to use external pull-up resistors anymore as it already has on-board 4.7kΩ pull-up resistors connected to the I2C lines. Also, the module includes a 2032 battery holder. As you can see in the image, we have a CR2032 battery there.

However, one thing that I wish they didn’t include in this board is the crappy battery charging circuit. The battery that comes with this module is not even rechargeable. But even if it comes with a rechargeable battery

Now, for the MAX7219 dot matrix LED display module, its driver, MAX7219, has a 3-wire serial interface input which can be connected to the SPI port of the MCU. The MAX7219 device is a common-cathode display driver that interfaces common MCUs to 7-segment displays (up to 8 digits), bar-graph displays, or 64 individual LEDs. The 64 individual LEDs in this case is the 8x8 dot matrix LED display. As mentioned earlier, we can already display the date and time with just the minimal Arduino Uno, the DS3231 RTC module, and the MAX7219 dot matrix LED display modules. However, we won’t be able to set the RTC except if we program the MCU again (later we will see in the code how the RTC is set). So I added four tactile switches so that we can set the time and date without reprogramming the MCU. The 5th switch is for the MCU manual reset. Later in the software/code and demo/testing, we will see how each of these switches work.

![Screenshot (650)](https://user-images.githubusercontent.com/118633170/209058238-4aed6a6c-9980-45da-8438-7c297d22d3b5.png)
![Screenshot (651)](https://user-images.githubusercontent.com/118633170/209058251-8f591a31-b28e-4ce6-abe8-9ece02c9eebe.png)


I have also added two 470uF-16V electrolytic capacitors, C5 and C6. Since we have eight 8x8 dot matrix LED displays (512 LEDs), we can’t avoid inrush current each time we turn on the digital clock. These two capacitors will help us prevent damage to any of the digital clock’s main components or instability in the digital clock’s operation caused by the inrush current. To make the digital clock more stable, I’ve also added the 2N3904 transistor and R2. Later, we will see their function but based on the schematic diagram, I think you can already guess their purpose. The ICSP and the UART headers will be used for programming and debugging. So I think that all for the hardware. In the second part, we will check the software or the code and see how the digital clock’s operation was programmed.

![Screenshot (654)](https://user-images.githubusercontent.com/118633170/209058278-8bb8b1d8-cb89-40a6-94a5-0ee34ef8e47b.png)
![Screenshot (657)](https://user-images.githubusercontent.com/118633170/209058285-42811d3f-963d-4eb1-bb07-c9954b33208b.png)


we can already display the date and time with just the minimal Arduino Uno, the DS3231 RTC module, and the MAX7219 dot matrix LED display modules. However, we won’t be able to set the RTC except if we program the MCU again (later we will see in the code how the RTC is set). So I added four tactile switches so that we can set the time and date without reprogramming the MCU. The 5th switch is for the MCU manual reset. Later in the software/code and demo/testing, we will see how each of these switches work

![Screenshot (662)](https://user-images.githubusercontent.com/118633170/209058315-644e13a9-db4c-48c5-8160-24dfae80dd6f.png)

1. INSTALL LIBRARIES

Before start writing the code and connect all the components you have to install some libraries to make all work properly.

The libraries that you need to install are:

ESP8266WiFi.h
Adafruit_GFX.h
Max72xxPanel.h
DHT.h
To install the ESP8266WiFi library you have to install the ESP8266 board in the Arduino IDE.

You can do it by simply doing this steps:

Open you IDE and click on "File -> Preferences".
In "Aditional Boards Manager URLs" add this line and click on "OK": "http://arduino.esp8266.com/stable/package_esp8266com_index.json"
Go to "Tools -> Board -> Boards Manager", type "ESP8266" and install it.
Go again to "Tools -> Board" and select "Generic ESP8266 Module".
To install the Adafruit_GFX library you only have to:

Open you IDE and click on "Sketch -> #includelibrary-> Manage Library".
Search for the Adafruit GFX library in the search bar and click on install.
Do the same thing to install the Max72xxPanel and the DHT-sensor-library.

Once you have installed all the library you are ready to connect all the components and start writing the code!

NOTE: You have to change two things in the code below:

![Screenshot (659)](https://user-images.githubusercontent.com/118633170/209058371-c0e2807d-838b-4f56-a42b-27d33c49a21e.png)


Wi-Fi credentials: at line 44 you have to insert your SSID and your PASSWORD
POOL Country: at line 48 you have to change the ntp pool. You can search the right one at https://www.ntppool.org/zone/@

