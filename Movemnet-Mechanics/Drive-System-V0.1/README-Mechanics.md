# Drive Mechanics V0.1

So, since we will be dealing with a lot of liquids we will need as much traction as possible. So I decided to use a 2-wheel drive (FWD) system with a freely rotating ball in the ball to provide stability.

Similar to Arcbotics Sparki:

![](Images/Wheel-concept.png)

So first things first let's design and simulate this drive system. We don't want to just keep 3D printing components over and over if things go wrong. Because they will... Instead, let's simulate a DC motor in Simulink and attach it to our Solidworks Part. This way we can run many simulations over and over, faster and cheaper.

Therefore, I am going to design a wheel with a fixed gear attached to it. So we can run the motor with a gear attachment and transfer power through the gear system. This way we can play around with gear ratios in case power issues arise.

Here is the part:
![](Images/Wheel-gear-part.png)

Now that we have our part let's export to Simulink! To do this we need to convert from a (.SLDALASM) to a (.XML).
*I will provide both files and the separate files in the repo*:)

This is what the model looks like in Simulink *(in orange border)*
![](Images/simulink-model.png)  

If you run the model SimMechanics Explorer will have your part built.
![](Images/SimMech-Part.png)


This is all handled by Simiulinks Library -> SimscapesMechanics and Simscapes Multibody Link. Lucky me!
Anyways now that we have a model all set up and ready, we now need our motor.

I will use a simple DC motor, an H-bridge (to control the direction of the motor rotation), a PWM module, a GearBox, and an Ideal Torqure Sensor.

Here is the circuit:
![](Images/Circuit-DC-motor.png)

### List of Components and their parameters:
- **Voltage Source : 5V**
- **Controlled PWM Voltage Block**: This is where we have to do some math! So to figure out the max frequency we can run our motor we need to find the max RPM our motor can handle. I have provided the datasheet of this motor.
I found that this motor can handle 8804(+-)10%. For safety reasons, I will use 7923 RPM. To find its max frequency(Hz) we can use this formula:***f = (RPM * #Communication Cycles)/60***. *Commutations are the number of pole switches in a motor*. Since we using a brushed motor, there is one switch occurring in the mechanical rotations. Anyways, let's plug in our values and we see that our motor can operate at a frequency of 132Hz. Let's do that for the simulation's sake, and because we can.
-**H-Bridge** : Simulation mode = PWM everthing else default.



