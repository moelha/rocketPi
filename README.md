


# Pi<img src="https://upload.wikimedia.org/wikipedia/commons/3/36/SpaceX-Logo-Xonly.svg" alt="alt text" width="50" height="60"> 
Rocket flight recorder based on Raspberry Pi Zero W v1.3)

<table border="0">
  <tr>
    <td><img src="/PiX_front.jpg" alt="Front"></td>
    <td><img src="/PiX_back.jpg" alt="Back"></td>
  </tr>

</table>



 
 ---
 
 ## Table of Contents
- [Electronic components](#electronic-components)
- [Model rocket](#model-rocket)
- [Setup](#setup)
  - [Raspbian Jessie](#raspbian-jessie)
  - [Python](#python)
  - [Mosquitto](#mosquitto)
  - [RPi Cam Interface](#rpi-cam-interface)
  - [Node-RED](#node-red) 
 ---
 
 ## Electronic components 

| Component             |        Description       |     Source      |                          Price                            |
| -------------         |:-------------:           |:-----:          | -----:                                                    |
| Raspberry Pi Zero W   | Version 1.3              |[Pimoroni](https://shop.pimoroni.com/products/raspberry-pi-zero)|       £4.58            |
| Camera   | Camera for Raspberry Pi Zero   |[Pimoroni](https://shop.pimoroni.com/products/raspberry-pi-zero-camera-module)|       £14            |
| LiPo SHIM             | Enables the RPi to be power supplied from a battery |[Pimoroni](https://shop.pimoroni.com/products/lipo-shim)| £10 |
| LiPo Battery          | 150mAh                   |[Pimoroni](https://shop.pimoroni.com/products/lipo-battery-pack) |    £5                  |
| BMP280                | Pressure, temperature and humidity sensor|[Pimoroni](https://shop.pimoroni.com/products/adafruit-bmp280-i2c-or-spi-barometric-pressure-altitude-sensor)|    £10.50       |
| MPU6050         | Accelerometer and Gyroscope     |[Sparkfun](https://www.sparkfun.com/products/11028)  |   £21.26       |

## Model rocket:

| Component             |        Description       |     Source      |                          Price                            |
| -------------         |:-------------:           |:-----:          | -----:                                                    |
| SpaceX Falcon 9   | Model rocket              |[SpaceX](https://shop.spacex.com/accessories/f9-flying-model-rocket-kit.html)|       £20.59            |

<img src="/image_from_rocket.jpg" alt="Shot from model rocket">

## Setup

### Raspbian Jessie

Download and flash [Raspbian Jessie](http://downloads.raspberrypi.org/raspbian_lite/images/raspbian_lite-2017-07-05/2017-07-05-raspbian-jessie-lite.zip) on a micro SD card (preferably a 64GB one) with [Etcher](https://etcher.io/), or an alternative flasher.

---
### Python
Python will be used to read from the sensors and transmit the data to Node-RED via mqtt
```
sudo apt-get install python-2.7 python-pip
```
Now let's install the mqtt library for Python
```
sudo pip install paho-mqtt
```
In order to read from the I2C from Python, we need to install the smbus module
```
sudo apt-get install python-smbus
```
---
### Mosquitto
Now let's install a MQTT broker, Mosquitto
```
wget http://repo.mosquitto.org/debian/mosquitto-repo.gpg.key
```
```
sudo apt-key add mosquitto-repo.gpg.key
```
```
cd /etc/apt/sources.list.d/
```
```
sudo wget http://repo.mosquitto.org/debian/mosquitto-jessie.list
```
```
sudo apt-get update
```
```
sudo apt-get install mosquitto mosquitto-clients
```
---
### RPi Cam interface

RPi Cam Web Interface is a web interface for the Raspberry Pi Camera module. It can be used for a wide variety of applications including surveillance, dvr recording and time lapse photography. We will be using it to capture images and live video from the camera. 

Connect the camera with the Raspberry Pi Zero W and proceed with the instructions below.

First, let's clone the RPi Cam Web Interface repository and install it
```
git clone https://github.com/silvanmelchior/RPi_Cam_Web_Interface.git
```
```
cd RPi_Cam_Web_Interface
```
```
./install.sh
```
---

### Node-RED

Now let's install Node-RED
```
bash <(curl -sL https://raw.githubusercontent.com/node-red/raspbian-deb-package/master/resources/update-nodejs-and-nodered)
```
Install the dashboard module
```
sudo npm install node-red-dashboard
```
Make it autostart on boot
```
sudo systemctl enable nodered.service
```
