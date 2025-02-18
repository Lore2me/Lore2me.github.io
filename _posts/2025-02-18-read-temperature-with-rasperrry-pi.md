---
layout: post
title: Read temperature with Rasperrry Pi
date: 2025-02-18 16:13 +0100
categories: [raspberry-pi]
tags: [raspberry-pi, temperature, sensor, DS18B20]
description: How to read temperature with a Raspberry Pi.
---
# Read temperature with Raspberry Pi
This guide will show you how to read temperature with a Raspberry Pi using a DS18B20 sensor (mine is waterproof).

## DS18B20
The DS18B20 is a digital temperature sensor that uses the 1-Wire protocol to communicate with the Raspberry Pi.
It is a low-cost sensor that is easy to use and provides accurate temperature readings.
The DS18B20 sensor has a range of -55°C to +125°C with an accuracy of ±0.5°C.

## Pre-requisites
- Raspberry Pi
- Raspbian OS installed on the Raspberry Pi
- DS18B20 sensor
- Jumper wires
- Breadboard
- 4.7kΩ resistor (delivered with the sensor)

## Step by Step
### 1. Connect the DS18B20 sensor
Connect the DS18B20 sensor to the Raspberry Pi as followed on this website:
[DS18B20 Raspberry Pi Tutorial](https://randomnerdtutorials.com/raspberry-pi-ds18b20-python/)

### 2. Enable 1-Wire Interface
The 1-Wire interface is disabled by default on the Raspberry Pi.
To enable it, open the Raspberry Pi configuration tool:
```bash
sudo raspi-config
```

Navigate to `Interfacing Options` -> `1-Wire` and enable the 1-Wire interface.

### 3. Testing the DS18B20 sensor
Load the required kernel modules:
```bash
sudo modprobe w1-gpio
sudo modprobe w1-therm
```

Navigate to the `/sys/bus/w1/devices/` directory:
```bash
cd /sys/bus/w1/devices/
```

List the devices in the directory:
```bash
ls
```

You should see a directory starting with `28-` followed by a unique identifier.
Navigate to the directory:
```bash
cd 28-xxxxxx
```

Read the temperature from the sensor:
```bash
cat w1_slave
```

The output will contain the temperature in degrees Celsius.
It will look something like this:
```
4b 01 4b 46 7f ff 0c 10 3c : crc=3c YES
4b 01 4b 46 7f ff 0c 10 3c t=23187
```

The temperature is the value after `t=` divided by 1000.

### 4. Reading the temperature with Python
You can also read the temperature with Python.
Here is a simple Python script that reads the temperature from the sensor:
```python
import os
import glob
import time
 
os.system('modprobe w1-gpio')
os.system('modprobe w1-therm')
 
base_dir = '/sys/bus/w1/devices/'
device_folder = glob.glob(base_dir + '28*')[0]
device_file = device_folder + '/w1_slave'

def read_temp_raw():
    f = open(device_file, 'r')
    lines = f.readlines()
    f.close()
    return lines

def read_temp():
    lines = read_temp_raw()
    while lines[0].strip()[-3:] != 'YES':
        time.sleep(0.2)
        lines = read_temp_raw()
    equals_pos = lines[1].find('t=')
    if equals_pos != -1:
        temp_string = lines[1][equals_pos+2:]
        temp_c = float(temp_string) / 1000.0
        temp_f = temp_c * 9.0 / 5.0 + 32.0
        return temp_c, temp_f
while True:
	print(read_temp())	
	time.sleep(1)
```
