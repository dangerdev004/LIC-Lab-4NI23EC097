# LIC-Lab-4NI23EC097
## Experiment - 1 {Analysis of CS Amplifier}
### Question
Perform DC, Transient and AC Analysis of the CS Amplifier with following specifications **Using LTSpice**
* Technology: 180nm (TSMC)
* VDD = 1.8 V
* Power Budget = 50 uW
Also Extract the following Parameters
* DC operating point
* Gain
* Bandwidth
* Power

#### [Prerequisites and Theory](https://www.allaboutcircuits.com/technical-articles/introduction-to-the-mosfet-common-source-amplifier/) 
Analog circuits are everywhere, and amplifiers are a part of basically every analog circuit. MOSFETs make excellent amplifying devices, which is why there are multiple single-stage amplifier topologies based around them. These are differentiated based on which transistor terminal is the input and which is the output.

In this article, we’ll discuss the common-source (CS) amplifier, which uses the gate as its input terminal and the drain as its output. The source terminal is common to both the input and output in terms of the AC signal, hence the name common-source. 
##### Common-Source Amplifier With a Resistor Load
![image](https://github.com/user-attachments/assets/e9db85d3-6b86-489f-bc76-45a591712ec0)
###### Large-Signal Operation of the CS Amplifier With Resistor Load
![image](https://github.com/user-attachments/assets/72ffa374-5021-4c25-b239-c6099b1ac53d)

Examining the figure more closely, we see that the following occurs as VIN increases from zero:
* When we start increasing VIN from zero, M1 remains off and VOUT remains at VDD until VIN nears the threshold voltage (VTH).
* At this point, M1 begins to conduct current. That causes a small voltage drop across the load resistor (RL), which in turn causes VOUT to decrease slightly.
* When VIN reaches VTH, M1 turns on. Because VOUT is greater than (VIN – VTH), M1 is biased in saturation.
* M1 remains in saturation as VIN increases until VOUT = VIN – VTH.
* Once VIN has increased to this point, M1 goes into the linear region and VOUT continues to decrease to nearly zero.

MOSFETs operate best as amplifiers when saturated—if the MOSFET falls out of saturation, the amplifier performance degrades rapidly. For that reason, we can consider the CS amplifier’s effective operating range to cover only the values of VOUT produced in saturation. In Figure 3, we can see that these output voltages range from when M1 turns on (VIN = VTH) to when M1 goes into the linear region (VOUT = VIN – VTH). Since VOUT = VDD – IDRL, we must minimize the product of IDRL to maximize the operating range of the amplifier.

###### Small-Signal Operation of the CS Amplifier With Resistor Load
Small-signal definitions are only valid when the transistor is operated in saturation and can therefore be estimated as a linear device. However, as we stated above, this encompasses the entire effective operating range of our amplifier. 

![image](https://github.com/user-attachments/assets/34b8c469-859b-4631-8000-44a5fa32670c)

Because the body of our circuit is shorted to the source terminal, gmbvbs = 0. We can calculate the small-signal voltage gain using Kirchhoff’s voltage and current laws:

$$ \frac{vout}{ro||RL} = −gmvin → \frac{vout}{vin} = −gm(ro||RL) $$

If we ignore the channel length modulation, this would imply infinite output resistance (ro) for the MOSFET. We can then simplify the gain equation to just gmRL. If we want to maximize the output gain, we should maximize gm and/or RL. Because gm is proportional to ID, however, maximizing the gain comes at the cost of the amplifier’s operating range.
Interestingly, if we multiply the output resistance by the transconductance of the MOSFET (gm), we obtain the small-signal gain we found in Equation 1. Furthermore, the gain of the CS amplifier then becomes equal to the resistance seen at the drain of M1 divided by the resistance seen at the source of M1, which is the reciprocal of the transconductance $\frac{1}{g_m}$. Therefore, from here on out we can generically define the voltage gain of all CS amplifiers as:

$$ A_v = −G_mR_{Out} $$

where Gm is the amplifier’s transconductance.

Because of the trade-off between high gain and operating range, the resistor load isn’t necessarily the best choice for a CS amplifier. In addition, large resistors are needed for large gains, and these result in very large devices on-chip. The resistance value can also change up to 20% due to process variations. For all of these reasons, it’s worth looking at load options that don’t require passive devices.

##### Common-Source Amplifier With a Diode-Connected Load
#### Analysis of CS Amplifier with a Resistor Load
In this section we will analyse the CS Amplifier with a resistive load, for that we will go ahead and install a simulation software more specifically LTSpice and assemble a very basic CS Amplifier Circuit as shown below, choose **NMOS4**, it has 4 terminals namely **Gate (G)**, **Drain (D)**, **Source (S)** and **Body (B)** terminals. Connect the Body terminal to Source of the MOSFET. Also add voltage sources and resistance, add supply for 1.8 V and set gate voltage to be around 50% of the supply voltage i.e. 0.9 V 

![PIc1](https://github.com/user-attachments/assets/9dab765c-b49a-4309-9914-6ca94b02d4a8)

##### Procedure
1. Create a new Experiment Workspace
2.  Enter a spice directive by clicking on **.t** option on the ribbon
<code> .lib tsmc018.lib </code> This specifies the BSIM3 Model of the MOSFET, if you stored this file in some other location specify that in the command
3. **Calculation**: We need to calculate the current according to our power budget since we have both supply voltage and power budget we can calculate the current from $I = \frac{P}{V}$. We will get our maximum permissible current to be $27.77 \mu A$
4. Now we can start finding appropriate **Aspect Ratio** for our MOSFET, we will take a range and combination of values for **W (width)** and **L (length)** of the MOSFET
5. After getting a suitable value we will perform **Transient** and **AC Analysis**

##### DC Operating Point
For the DC Operating Point:
* Go to **Simuate** -> **Configure Analysis** -> **DC operating point**
* Add the **.op** text on the experiment workspace
* Click on the **Play** button to turn on the simulation, this will generate a text file with all the voltages and currents for more info go to **View** -> **SPICE Output Log**

###### Observations
Now the value of our $I_D$ will be different for different W, L ,R and $V_{GS}$ values, so we have 4 parameters to work around with, we will see what affect they have on current one by one
1. **Affect of L (Channel length)**

For this analysis we will keep $R_D = 1k \ohm$, $V_{GS} = 0.9 V$ and perform a **Linear parameter sweep** for W and **List paramter sweep** for L, with the help of the commands

<code>.step param W 30n  250n 1n</code>

Keep L = 180nm , then you will get a curve for <code>ID vs W</code> for L = 180 nm

![Experiment-1(Id_vs_W)](https://github.com/user-attachments/assets/9ce97280-0051-4b10-8af6-1596d98758e9)

As you can see, for our conditions at no value of W is the current near $27.77 \mu A$, it is always higher than that thus going over the power budget, also notice the spikes at the beginning of the curve and at particularly low values of 30nm - 40nm the current decreases but according to the current equation $I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T)^2$, W is directly proportional to $I_D$ so if other parameters are constant then $I_D$ must increase linearly with respect to W but that is not the case here

We further analyse this curve for various values of L using parameter sweeps at the same time

![Experiment-1(Id_vs_L_varied)](https://github.com/user-attachments/assets/05108b77-821b-46e8-b296-04b132e4c845)

**In the figure as we go down length increase**

As you can observe, at higher lengths with R and $V_{GS}$ constant we can see the linearlity in the relation thus a higher value of L is recommended

So for this reason we will choose **L = 600nm**

2. **Affect of W (Channel width)**

For this analysis we will keep $R_D = 1k \ohm$, $V_{GS} = 0.9 V$ and perform the parameter sweep again but this time for L,

![Experiment-1(Id_vs_L_W)](https://github.com/user-attachments/assets/a5df5d1d-0ef2-47da-9103-1ab9cc461f38)

This curve is quite normal in the sense it follows the MOSFET current equation becuase as $I_D$ increases L decreases and that is exactly what is happening here, however we cannot go lower than 180nm as it is a bound specified by the manufacturer in our case TSMC,

So for our case for L = 600nm we take **W = 592nm** , you can also perform hit and trial for this to get the same result

![Experiment-1(Id_vs_L)](https://github.com/user-attachments/assets/a01d9821-3514-43fe-a1c5-0d6a1e4f9ecc)
![DC_Operating_Point](https://github.com/user-attachments/assets/5920f3df-9976-4db1-ac01-83db3e22aa88)

3. **Affect of R (Drain Resistance)**

Now $R_D$ will definitely change the current, decreasing the resistance will increase the current, but it can overshoot our specified power budget and it lowers the amplifier gain, so for this reason we will increase $R_D$ this will for sure decrease the current from maximum permissible amount but we can get much higher gains (a reasonable trade off), however we should be careful as very high resistance can tip the MOSFET out of the saturation region which will be catastrophic for an amplifier therefore be very careful while varying the resistance, we will start with basic MOSFET characterstics first for a constant R and then we will see the affect of change of $R_D$

**Voltage Transfer Characterstics**

![VTC](https://github.com/user-attachments/assets/2b571034-90a8-41de-b61b-7756211f7277)

**Drain Characterstics**

![Drain_Characterstics_25k](https://github.com/user-attachments/assets/8d0e9504-9377-438e-b35e-b99bac69f94a)
