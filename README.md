TweepyOne
=========

TweepyOne - Raspberry Pi Twitter/RSS-Feed Monitor

*WHY?*

The “Internet of Things” is the next wave of the internet. Basically, if any device can connect to the internet, it can take part in a worldwide network of sensors and output devices. Using this Internet of Things, it will be possible for tiny devices to be connected together into much larger systems. In February 2011, Ericsson predicted there will be 50 billion connected devices by 2020.

Basically, any tiny connected device can produce data that is uploaded to the internet. This data can then be analysed on large servers, presented on mobile apps, or even used to send messages to other internet connected devices that make things happen in the real world.



### Install Required Packages

We will still need to install modules to search Twitter with Python. Several exist, but I recommend [Twython](https://github.com/ryanmcgrath/twython).

`sudo apt-get update

sudo apt-get install python-pip

sudo pip install twython`


Also you will need a LCD I2C Driver Library. You can use the Adafruit Classes as well but I suggest the LCD i2C Library from ARCADIALABS. You can find it in my GIT Reprository or you can clone it by yourselve.

`git clone https://github.com/CaptainStouf/raspberry_lcd4x20_I2C.git`

*more instructions will follow ...*


### Install the LCD on Raspberry Pi

######Wireing

5v0 / 3v3 side :

AVcc -> Pi + 5v0 or 3v3
GND -> Pi GND Pin
ASCL -> SCL Pin on Pi
ASDA -> SDA Pin on Pi

######Enable and setup the I²C in Raspbian

We add the modules to the startup

`sudo nano /etc/modules
`
Add those 2 lines:

`i2c-bcm2708 
i2c-dev
`
We reboot

`sudo reboot
`
we now install the required components :

`sudo apt-get install python-smbus i2c-tools
`
We remove the I²C modules from the blacklist :

`sudo nano /etc/modprobe.d/raspi-blacklist.conf
`
comment out the line

`blacklist i2c-bcm2708
`

Also remove the I²C modules from the blacklist.

`sudo nano /etc/modprobe.d/raspi-blacklist.conf
`
Comment out the line

`blacklist i2c-bcm2708
`
Our Raspberry should be ready to use I²C devices after a new reboot. Check it !!

`ls -las /dev/i2c*

0 crw-rw---T 1 root i2c 89, 0 Jun 30 19:17 /dev/i2c-0
0 crw-rw---T 1 root i2c 89, 1 Jun 30 19:17 /dev/i2c-1
`

Install the required components

`sudo apt-get install python-smbus i2c-tools
`

######Testing the I²C

We are going to use the i2cdetect command to list every I²C devices. This command is not the same on a Rev 1 or Rev 2 Pi (I²C bus address is different), so it’s important to choose the right one:

`sudo i2cdetect -y 0 (for Rev 1)
sudo i2cdetect -y 1 (for Rev 2)`

You should see many numbers (00). Write down a number like 3f or 33 or 2h. This is your LCD address on the I2C bus. Head over to the LCDlib. Change line 5 in **lcddriver.py** file, you’ll have to set the I²C address. *It defaults to #27.*

`# LCD Address

ADDRESS = 0x27`

### **Changelog**



Version 1.1

* Erste Implementierung online



*This project is released under the GPLv2 license. Please use this at your own risk.*