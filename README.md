# Minorly refactored

The original MicroBasic script by Clear path did not intialize the second channel. 

One of the ways to make this ros driver work with two channels for the roboteq motorcontroller. You would need to:

1. Download Roborun which is only supported in Windows [here](https://www.roboteq.com/index.php/support/downloads).

2. Load the minorly altered "script.mbs" onto the STM32 of the microcontroller via Roborun. That's it!

## Compiling and launching roboteq_driver

```
catkin_make --pkg roboteq_driver roboteq_msgs roboteq_diagnostics
source ~/catkin_ws/devel/setup.bash
roslaunch roboteq_driver example.launch #This has been altered minorly to support two channels
```

## Topics published and subscribed by default if you don't alter example.launch
```
/channel1/cmd #subscribing
/channel1/feedback #publishing
/channel2/cmd #subscribing
/channe2/feedback #publishing
/roboteq_driver/status #publishing
```


roboteq
=======

ROS driver for serial Roboteq motor controllers. This driver is suitable for use with Roboteq's
Advanced Digital Motor Controllers, as described in [this document][1]. Devices include:

Brushed DC: HDC24xx, VDC24xx, MDC22xx, LDC22xx, LDC14xx, SDC1130, SDC21xx  
Brushless DC: HBL16xx, VBL16xx, HBL23xx, VBL23xx, LBL13xx, MBL16xx, SBL13xx  
Sepex: VSX18xx

The node works by downloading a MicroBasic script to the driver, which then publishes ASCII sentences at 10Hz and 50Hz with the data corresponding to the Status and per-channel Feedback messages published by the driver.

[1]: https://www.roboteq.com/index.php/docman/motor-controllers-documents-and-files/documentation/user-manual/272-roboteq-controllers-user-manual-v17/file
