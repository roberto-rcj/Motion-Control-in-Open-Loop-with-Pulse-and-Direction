# Motion-Control-in-Open-Loop-with-Pulse-and-Direction

There are many applications using pulse and direction. These applications, normally are destinated to stepper motors motion, but can be used without any change to servo motors or any type of motor that requests pulses to be controlled.

In this project, you will see an example made in C++ using Arduino UNO to generate a speed ramp in a stepper motor. In this code, the system controll will be in a open loop, so the controller (Arduino UNO) will send pulses to move the stepper motor and our plant will ensure that the motor will receive the comands without losses or interferences. The plant is basically our hardware.

## The Hardware

