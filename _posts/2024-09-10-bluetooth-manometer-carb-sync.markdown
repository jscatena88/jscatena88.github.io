---
layout: post
title:  "Bluetooth Manometer for Carburetor Synchronization"
date:   2024-04-26 00:00:00 -0800
tags: ESP32 Bluetooth Carburetor Manometer BLE
---

## Bottom Line Up Front

In this project, I work towards creating a portable device for synchronizing carburetors that uses bluetooth to stream pressure readings to a phone or laptop. Pressure readings are presented as a time series plot making it easier to review how adjustments are affecting the readings. Below are some photos of the device and screenshots of the UI as I used it to synchronize the carbs on my Honda. 
| ![Prototype Device]() | ![UI Screenshot](/assets/bluetooth_manometer/UI_screenshot_cropped.jpg)  | 
| :--: | :--: |
| The device as it exists right now | The prototype UI |

## Electrical Components Design

The key enabler of this design is a Honeywell 0-25 PSI digital absolute pressure sensor. Specifically, for the prototype I am using the [SparkFun Qwiic MicroPressure](https://www.sparkfun.com/products/16476) which provides an economical and convenient breakout board for the sensor. This sensor provides accurate readings across the entire pressure range we are interested in and is easy to work with using I2C for communication. For this prototype, I am using two of the sensors since I personally own a two cylinder motorcycle; however, scaling up the design to 4 or even 6 sensors would not be difficult. 

| ![SparkFun Qwiic MicroPressure](/assets/bluetooth_manometer/SparkFun_Qwiic_MicroPressure_Sensor.jpg) |
| :--: |
| SparkFun Qwiic MicroPressure Device. Image from [SparkFun](https://www.sparkfun.com/products/16476)  and licensed [CC BY 2.0](https://creativecommons.org/licenses/by/2.0/) |

Reading the sensors and serving Bluetooth Low Energy communications is handled by the [SparkFun ESP32 WROOM Thing Plus with USB-C](https://www.sparkfun.com/products/20168) which uses the Espressif ESP32 microcontroller. This was my first time using this development board and I was extremely impressed. The board's battery management and power system is very well designed and by staying in the SparkFun product ecosystem connecting the pressure sensors using their Qwiic system was painless. 

Finally, rounding out the electrical components is a LiPo battery, a small switch for turning on and off the device, and a I2C Mux board. I used the mux board to allow using two sensors from the one Qwiic connector on the Thing Plus board. As provided by Sparkfun, the sensors all share the same I2C address which would clash if they shared the same I2C bus. Honeywell provides the sensor with up to 8 different I2C addresses, but each must be ordered as a separate model of the device. For this reason it is very reasonable the SparkFun only provides the one model, however in the future a larger production run of this device would be able to simplify the design by using separate models of the sensor.

| ![Electrical Components Connected](/assets/bluetooth_manometer/Electrical_Compononets.jpg) |
| :--: |
| The electrical components less the battery connected together |

## Firmware

The firmware was written using the Arduino IDE mainly for ease of development. SparkFun provides examples and libraries for most of their components in the Arduino ecosystem. The firmware stands up a Bluetooth Low Energy Service and offers two characteristics one for each of the sensors. Each characteristic advertises a single 32 bit float value. When a client connects the device it begins sampling the sensors and publishing their values in a loop with a 10 Millisecond delay at the end of each iteration. 

The code can be [seen here on github]()

## Web UI

To display the data I decided the path of least resistance would to use the Bluetooth Web Standards. This approach ended up working really well and was very easy to develop; however, the Bluetooth web standard is not particularly well supported so it will only run on certain combinations of browsers and devices. I found Chrome on my Android phone to work very well.

The actual data is plotted using calls to the Canvas API (which has great browser support),  this makes the page highly performant and means it has no external dependencies. The HTML and Javascript all fit in one file comfortably. The code is [available here]() but I will warn I have almost no experience with Javascript and heavily leaned on ChatGPT to write this page so don't judge it too harshly.

## Physical Design

Finally, I designed a 3D printable case that holds everything. By chance some flow regulator valve's I already had that were designed for 4mm ID tubing happen to slide over the sensor's port with a nice positive pressure fit. The pressure sensors are somewhat fragile especially with the extra leverage of the valve adapters when they are attached, I already managed to break one of them. So when designing the case I took extra care to ensure that the valve body and sensors were both held securely. Especially since the other half of the valve body extends from the case and is the primary touch point of the device in use.

## Next Steps

With the work described above I have a device that works for me and my use case. In fact it has already helped me get my motorcycle running better. Hopefully the information above is also enough that anyone else who is interested could make their own. However, if it seems like their is potential interest I have been batting around the idea of spending more time on the project to really elevate it from a one-off prototype to at least an Alpha product, maybe even trying to sell kits or PCBs on my site or a crowd funding site. If I went that direction the below is a minimum of the additional work I would want to do before launching.

 1. New PCB, to cut down on costs and reduce part count
 2. Case design that integrates a pressure manifold for the sensors, this would require they be manufactured with a process other than FDM 3D printing.
 3. Improve firmware to add battery information to BLE outputs and possibly look into using power saving modes when the device it idle
 4. Improve UI, at the very least it needs X and Y scales on the graph and some configurable smoothing factor to reduce noise. I will also probably have to reevaluate whether the Web Bluetooth standard is the right tool for the job. I love how light weight and easy to use it is, but I don't love that it forces users to have a web connection just to interact with a simple application, and the lack of support on iOS and Linux devices is less than ideal

