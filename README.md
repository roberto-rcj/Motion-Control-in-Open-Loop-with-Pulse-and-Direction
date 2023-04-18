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

### *Pulses generator formula*
 The total of pulses generated to rotate some turns the stepper motor can be calculated by:
 
### Nº pulses = microsteps x stepper resolution x Nº turns (I)
where:
 Nº pulses = total number of pulses necessary to turn the motor to the desired position
 microsteps = stepping reduction ration to smooth the movements;
 stepper resolution = number of pulses to turn once the stepper motor
 Nº turns = number of desired turns
 
 example: for this project, microsteps = 4, stepper resolution = 200, number of turns = 20
 so, the total pulses that can need to be genereted are: 
 Nº pulses = 4 x 200 x 20 = 16000 pulses
 
 ### *distance moved formula*
 Using some mechanical system (pulley, rack and pinion, ball screw, etc...) we can convert rotary moving to linear moving. By this manner, each mechanisc has a conversion formula, but we can skip this part and understand that the important information is the number that correlates this transformation. This number is the *relation constant* and needs be from turns to linear unit, as milimeters, for example. In this project we will convert turns to milimeters. let´s take a look at the formula:
 
 ### Distance = Nº turns x K (II)
  where:
   Distance = distance in millimeters moved;
   Nº turns = number of turns desired to the motor;
   K = convertion constant that converts pulses in millimeters.
   
example: imagine a system of ball screw coupled in the motor that has a relation of 5mm/turn, so with 20 turns we will have:
Distance = 20 x 5 = 100mm moved by the motor.

but if we join the equations I and II, we can manage the variables to hide the number of turns, and let explicit the relation between distance and pulses. look:

### Nº pulses = (microsteps x stepper resolution x Distance) / K (III)

### *speed and aceleration formula*

in a real application, normally we request from the user, the distance that will be moved, the motor top speed and acceleration. For this example we will deal with a constant acceleration ratio.

if we divide the distance to the time, we have the speed, so, doing this to the equation III

### speed = Nº pulses / time = (microsteps x stepper resolution x Distance) / (K * time)(III)

