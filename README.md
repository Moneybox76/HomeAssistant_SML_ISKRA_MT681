# Power metering with SML of ISKRA MT681 in Home Assistant

This project is for reading SML messages from Smart Meter ISKRA MT681, convert the data to readable values and then publish the vaules to a MQTT server. Finally we import the values in Home Assistant for further usage.


First of all I want to say thanks to Stefan Weigert who wrote a really good article (http://www.stefan-weigert.de/php_loader/sml.php) about the implementation of SML and example python scripts. This gave me enough insights in the structure of SML and so finally I was able to modify his script to work with ISKRA MT681.

Also I added mqtt support to the script, so I’m able to get the power values easy in Home Assistant.

### Prerequisites

- Connect USB Infrared Sensor to your system. I'm using one from volkszaehler.org (https://wiki.volkszaehler.org/hardware/controllers/ir-schreib-lesekopf-usb-ausgang)

- Following the instructions to set up the serial settings via minicom.

- Install python2.x, pyserial & paho-mqtt

```
sudo apt install python
sudo apt install pyserial
sudo pip install paho-mqtt
```

### Installing

- Copy the python script readSML.py from repository and change configuration variables for tty and MQTT as you need

- Copy daemon script sml.daemon.service to /etc/systemd/system/sml.daemon.service and edit the PATH to the script
```
sudo cp sml.daemon.service /etc/systemd/system/sml.daemon.service
sudo vi /etc/systemd/system/sml.daemon.service
    --> change <PATH>/readSML.py to your script location
```

- Reload Daemon and enable daemon script
```
sudo systemctl daemon-reload
sudo systemctl enable sml.daemon.service
sudo systemctl start sml.daemon.service
```

- Create mqtt & filtered sensors in Home Assistant (sensor.yaml)

- Customize the filtered sensors in Home Assistant (customize.yaml)

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

