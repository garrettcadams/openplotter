openplotter-raspbian
==================
Project page: http://campus.sailoog.com/course/view.php?id=9

![OpenPlotter-Raspian](http://campus.sailoog.com/pluginfile.php/715/mod_page/intro/OpenPlotter-SailPi.jpg "OpenPlotter-Raspian")

Instructions
------------

##### Create an SD card with the last version of Raspian:
http://www.raspberrypi.org/downloads/

##### Compile OpenCpn:
http://opencpn.org/ocpn/compiling_source_linux

##### Install dependencies:
```sh
sudo apt-get install libusb-1.0-0-dev libasound-dev libpulse-dev python-pip python-wxgtk2.8 isc-dhcp-server hostapd x11vnc 
```

##### Install kplex:
http://www.stripydog.com/kplex/kplex.html

##### Install pynme2:
```sh
git clone git://github.com/Knio/pynmea2.git
cd pynmea2
sudo pip install pynmea2
```
##### Follow this tutorial:
https://learn.adafruit.com/setting-up-a-raspberry-pi-as-a-wifi-access-point?view=all

##### Install SDR software
```sh
cd
git clone git://git.osmocom.org/rtl-sdr.git
cd rtl-sdr
mkdir build
cd build
cmake ../ -DINSTALL_UDEV_RULES=ON
make
sudo make install
sudo ldconfig
```
##### Install AIS decoder software
```sh
cd
wget http://www.aishub.net/downloads/aisdecoder-1.0.0.tar.gz
tar zxvf aisdecoder-1.0.0.tar.gz
cd aisdecoder-1.0.0
cmake -DCMAKE_BUILD_TYPE=release
make
sudo cp aisdecoder /usr/local/bin
```
```sh
cd /etc/modprobe.d
sudo nano no-rtl.conf
```
add lines:
```sh
blacklist dvb_usb_rtl28xxu
blacklist rtl2832
blacklist rtl2830
```
##### Clone this repository to /home/pi/.config/openplotter
```sh
cd .config
git clone git://github.com/sailoog/openplotter-raspbian.git openplotter
```
##### Set permissions:
```sh
cd /home/pi/.config/openplotter
sudo chmod 755 gps_time_cron.sh
sudo chmod 755 gps_time_daemon.py
sudo chmod 755 openplotter.py
sudo chmod 755 output.py
sudo chmod 755 startup.py

cd /home/pi/.config/openplotter/nmea_wifi_server
sudo chown root:root switch_access_point.sh
sudo chmod 755 switch_access_point.sh
```
##### Run at startup:
```sh
~/.config/openplotter/startup.py
```
##### Run:
```sh
python /home/pi/.config/openplotter/openplotter.py
```



