# Motion-Control-in-Open-Loop-with-Pulse-and-Direction

There are many applications using pulse and direction. These applications, normally are destinated to stepper motors motion, but can be used without any change to servo motors or any type of motor that requests pulses to be controlled.

In this project, you will see an example made in C++ using Arduino UNO to generate a speed ramp in a stepper motor. In this code, the system controll will be in a open loop, so the controller (Arduino UNO) will send pulses to move the stepper motor and our plant will ensure that the motor will receive the comands without losses or interferences. The plant is basically our hardware.

## HARDWARE

The hardware is made by:

### controller
  an Arduino UNO, operating with 5V, using pin 9 as fast output, that provides the pulses output and pin 8 providing the direction pin. the pin 7 will be used to start/stop the controlling.

### plant
  is the stepper motor drive. There are many types in the marketplace, but basically they convert the pulses received into rotation to the stepper motor. For this project, the drive used was TB6600, that contains the pulse and direction inputs with a level voltage of 5V. there is a enable pin that is used to stop the controlling.
  
### controlled object
 For this example was used an stepper motor of 200 pulses per rotation.
 
 the figure below shows the electrical conection. To smooth the motor motion, a stepping reduction ratio (microsteps) of 1:4 was set into the drive. This configuration can be set by hardware and reduces the motor cogging and hard motion, turning more linear the movements.
 
## MOTION EQUATION
there are some formulas to calculate the motor motion. let´s take a look:

### Pulses generator formula
 The total of pulses generated to rotate some turns the stepper motor can be calculated by:
 
# Nº pulses = microsteps x stepper resolution x Nº turns
where:
 Nº pulses = total number of pulses necessary to turn the motor to the desired position
 microsteps = stepping reduction ration to smooth the movements;
 stepper resolution = number of pulses to turn once the stepper motor
 Nº turns = number of desired turns
