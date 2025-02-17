# LIC-Lab-4NI23EC097
## Experiment - 1 {Analysis of CS Amplifier}
### Question
Perform DC, Transient and AC Analysis of the CS Amplifier with following specifications **Using LTSpice**
* Technology: 180nm (TSMC)
* VDD = 1.8 V
* Power Budget = 50 $\mu$ W
Also Extract the following Parameters
* DC operating point
* Gain
* Bandwidth
* Power

##### NOTE: Parts of theory and prerequisite is taken from the webpage linked below
#### [Prerequisites and Theory](https://www.allaboutcircuits.com/technical-articles/introduction-to-the-mosfet-common-source-amplifier/)  {Follow this link for more info}
# Common-Source (CS) Amplifier Overview

## Introduction

Amplifiers are a fundamental part of analog circuit design, and MOSFETs serve as excellent amplification devices. Among the various single-stage amplifier topologies, the **common-source (CS) amplifier** is widely used. It is characterized by having the **gate as the input, the drain as the output, and the source as the common terminal** for AC signals.

This document covers two common implementations of the CS amplifier:  
- **CS Amplifier with a Resistor Load**
- **CS Amplifier with a Current Source Load**

---

## CS Amplifier with a Resistor Load

In this configuration, a **resistor** acts as the load at the drain terminal.

### Large-Signal Operation

The behavior of the circuit changes as the input voltage (VIN) varies:

- When VIN is near zero, the MOSFET remains off, and the output voltage (VOUT) is at VDD.
- As VIN approaches the **threshold voltage (VTH)**, the MOSFET starts conducting, leading to a small voltage drop across the load resistor (RL), causing VOUT to decrease.
- When VIN exceeds VTH, the MOSFET enters **saturation**, and the amplifier operates effectively.
- As VIN continues to increase, the MOSFET eventually enters the **linear region**, causing a further drop in VOUT.

Since MOSFETs function best as amplifiers in saturation, the effective **operating range** of the amplifier is limited to values where the transistor remains in saturation.

#### Circuit Diagram:
![CS Amplifier with Resistor Load](https://github.com/user-attachments/assets/e9db85d3-6b86-489f-bc76-45a591712ec0)

#### Transfer Characteristics:
![Large-Signal Characteristics](https://github.com/user-attachments/assets/72ffa374-5021-4c25-b239-c6099b1ac53d)

### Small-Signal Operation

For small-signal analysis, the MOSFET can be approximated as a **linear device** in saturation.

The **voltage gain (Av)** is given by:

$$A_v = -g_m (r_o || R_L)$$

where:
-  $g_m$ = transconductance of the MOSFET  
-  $r_o$ = output resistance of the MOSFET  
-  $R_L$ = load resistance  

If **channel length modulation** is ignored, $r_o$ becomes very large, simplifying the gain to:

$$A_v \approx -g_m R_L$$

This means the gain increases with higher transconductance or a larger load resistor. However, increasing **R_L** leads to larger chip area and variations in resistance due to process changes, making it less practical for integrated circuits.

#### Small-Signal Model:
![Small-Signal Model](https://github.com/user-attachments/assets/34b8c469-859b-4631-8000-44a5fa32670c)

---

## CS Amplifier with a Current Source Load

To overcome the limitations of a resistor load, **a current source can be used instead**.

#### Circuit Diagram:
![CS Amplifier with Current Source Load](https://github.com/user-attachments/assets/73a2ca8b-b223-4be7-af89-1674b945fc5f)

### Small-Signal Analysis

The **small-signal gain** for a CS amplifier with a current source load is:

$$A_v = -g_{m,n} (r_{o,n} || r_{o,p})$$

where:
- $g_{m,n}$ = transconductance of NMOS  
- $r_{o,n}$, $r_{o,p}$ = output resistances of NMOS and PMOS transistors  

Since $r_{o,p}$ is much larger than **$1/g_{m,p}$**, this configuration provides **higher gain** than a resistor-loaded amplifier.

### Operating Region

For proper operation, the circuit must satisfy:

$$V_{TH,N} \leq V_{IN} \leq V_{OUT} + V_{TH,N}$$

$$V_{IN} - V_{TH,N} \leq V_{OUT} \leq V_{DD} - V_{B} - |V_{TH,P}|$$

A lower bias voltage **increases the operating range** but reduces the resistance of the PMOS load, which decreases gain. The trade-off between gain and operating range makes this configuration more suitable for applications requiring higher amplification at the cost of design complexity.

---

## Conclusion

- A **CS amplifier with a resistor load** offers a straightforward design but has limitations in gain and stability.  
- A **CS amplifier with a current source load** provides higher gain but requires careful biasing.  

The choice between these configurations depends on the application and design constraints.



#### <ins>Analysis of CS Amplifier with a Resistor Load</ins>
In this section we will analyse the CS Amplifier with a resistive load, for that we will go ahead and install a simulation software more specifically LTSpice and assemble a very basic CS Amplifier Circuit as shown below, choose **NMOS4**, it has 4 terminals namely **Gate (G)**, **Drain (D)**, **Source (S)** and **Body (B)** terminals. Connect the Body terminal to Source of the MOSFET. Also add voltage sources and resistance, add supply for 1.8 V and set gate voltage to be around 50% of the supply voltage i.e. 0.9 V 

![PIc1](https://github.com/user-attachments/assets/9dab765c-b49a-4309-9914-6ca94b02d4a8)

##### <ins>Procedure</ins>
1. Create a new Experiment Workspace
2.  Enter a spice directive by clicking on **.t** option on the ribbon
<code> .lib tsmc018.lib </code> This specifies the BSIM3 Model of the MOSFET, if you stored this file in some other location specify that in the command
3. Add the transistor **NMOS4** and Change the name of the transistor to **CMOSN**
4. **Calculation**: We need to calculate the current according to our power budget since we have both supply voltage and power budget we can calculate the current from $I = \frac{P}{V}$. We will get our maximum permissible current to be $27.77 \mu A$
5. Now we can start finding appropriate **Aspect Ratio** for our MOSFET, we will take a range and combination of values for **W (width)** and **L (length)** of the MOSFET
6. After getting a suitable value we will perform **Transient** and **AC Analysis**

##### <ins>DC Operating Point</ins>
For the DC Operating Point:
* Go to **Simuate** -> **Configure Analysis** -> **DC operating point**
* Add the **.op** text on the experiment workspace
* Click on the **Play** button to turn on the simulation, this will generate a text file with all the voltages and currents for more info go to **View** -> **SPICE Output Log**

###### <ins>Observations</ins>
Now the value of our $I_D$ will be different for different W, L ,R and $V_{GS}$ values, so we have 4 parameters to work around with, we will see what Effect they have on current one by one
1. **Effect of L (Channel length)**

For this analysis we will keep $R_D = 1k \ohm$, $V_{GS} = 0.9 V$ and perform a **Linear parameter sweep** for W and **List paramter sweep** for L, with the help of the commands

<code>.step param W 30n  250n 1n</code>

Keep L = 180nm , then you will get a curve for <code>ID vs W</code> for L = 180 nm

* **I<sub>D</sub> vs W {for L = 180nm}**
![Experiment-1(Id_vs_W)](https://github.com/user-attachments/assets/9ce97280-0051-4b10-8af6-1596d98758e9)

As you can see, for our conditions at no value of W is the current near $27.77 \mu A$, it is always higher than that thus going over the power budget, also notice the spikes at the beginning of the curve and at particularly low values of 30nm - 40nm the current decreases but according to the current equation $I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T)^2$, W is directly proportional to $I_D$ so if other parameters are constant then $I_D$ must increase linearly with respect to W but that is not the case here

We further analyse this curve for various values of L using parameter sweeps at the same time

* **I<sub>D</sub> vs W {for various W}**
![Experiment-1(Id_vs_L_varied)](https://github.com/user-attachments/assets/05108b77-821b-46e8-b296-04b132e4c845)

**In the figure as we go down length increase**

As you can observe, at higher lengths with R and $V_{GS}$ constant we can see the linearlity in the relation thus a higher value of L is recommended

So for this reason we will choose **L = 600nm**

2. **Effect of W (Channel width)**

For this analysis we will keep $R_D = 1k \ohm$, $V_{GS} = 0.9 V$ and perform the parameter sweep again but this time for L,

* **I<sub>D</sub> vs L {for various W}**
![Experiment-1(Id_vs_L_W)](https://github.com/user-attachments/assets/a5df5d1d-0ef2-47da-9103-1ab9cc461f38)

This curve is quite normal in the sense it follows the MOSFET current equation becuase as $I_D$ increases L decreases and that is exactly what is happening here, however we cannot go lower than 180nm as it is a bound specified by the manufacturer in our case TSMC,

So for our case for L = 600nm we take **W = 592nm** , you can also perform hit and trial for this to get the same result

* **I<sub>D</sub> vs L** 
![Experiment-1(Id_vs_L)](https://github.com/user-attachments/assets/a01d9821-3514-43fe-a1c5-0d6a1e4f9ecc)

* **DC Operating Point**
![DC_Operating_Point](https://github.com/user-attachments/assets/5920f3df-9976-4db1-ac01-83db3e22aa88)

3. **Effect of R (Drain Resistance)**

Now $R_D$ will definitely change the current, decreasing the resistance will increase the current, but it can overshoot our specified power budget and it lowers the amplifier gain, so for this reason we will increase $R_D$ this will for sure decrease the current from maximum permissible amount but we can get much higher gains (a reasonable trade off), however we should be careful as very high resistance can tip the MOSFET out of the saturation region which will be catastrophic for an amplifier therefore be very careful while varying the resistance, we will start with basic MOSFET characteristics first for a constant R and then we will see the Effect of change of $R_D$
**Gain is directly dependent on drain resistance and hence we will need to increase $R_D$ for increased gain but be careful as it may tip off the saturation point**

**<ins>Voltage Transfer Characteristics</ins>**

![VTC](https://github.com/user-attachments/assets/2b571034-90a8-41de-b61b-7756211f7277)

**<ins>Drain Characteristics</ins>**

![Drain_Characteristics_25k](https://github.com/user-attachments/assets/8d0e9504-9377-438e-b35e-b99bac69f94a)

* **I<sub>D</sub> vs V<sub>DS</sub> {for various R}**
![Drain_Characteristics_R](https://github.com/user-attachments/assets/ecfa7fe8-6a0f-435a-a147-011f12221a35)

**The second graph is for various values of R the topmost curve has lowest R while bottom most have highest R**

**<ins>Transfer Characteristics</ins>**

![Experiment-1(Id_vs_VgsvaryR)](https://github.com/user-attachments/assets/5cef4f5d-7a0b-42e6-b502-776213ec9f05)

This is transfer characteristics for various values of $R_D$ (Lowest R for highest curve, same as that in drain characteristics)

* **I<sub>D</sub> vs V<sub>GS</sub> {For V<sub>DD</sub> = 1.8 V}**
![Experiment-1(Id_vs_Vgs)](https://github.com/user-attachments/assets/5a8b6ad5-ba45-40a7-9591-f318df57600c)

The above graph shows that for $V_{DD} = 1.8 V$ we get maximum current at $V_{GS} = 0.9 V$ for $R_D = 1k \ohm$

These graphs are pretty standard for a MOSFET, we will continue our analysis,

Now let us see how $I_D$ varies with $R_D$ 

* **$I_D$ vs R {for various L}**
![Experiment-1(R1_vs_Id_varyL_1)](https://github.com/user-attachments/assets/707e6841-e5d0-4722-996b-3d41b1296cf1)

From the graph we can observe for L = 180nm and W = 100nm we will get maximum current at resistance of $58 k \ohm$ (approx)
We can also see that for higher L the current will never reach the maximum value for any value of R.

So for lower values of L and W the drain resistance should be high to reach max current, so if we keep our L and W high we can use lower values of R

So now we have **L = 600nm W = 592nm R = 1 k $\ohm$**

4. **Effect of $V_{GS}$**

This is the main parameter for turning on the MOSFET and hence it is very important, we have actually seen it's effects in the section of Effect of drain resistance.

For increased gain we can change our $R_D = 25k \ohm$

Our final values **L = 600 nm  W = 592 nm  $R_D = 25k \ohm$  $V_{GS}$ = 0.9 V**

##### <ins>Transient Analysis<\ins>

We will now add a time varying (sine) source to our input gate and observe the output from drain terminal, we are not using any filters so be careful of the offset

***Procedure***

1. Edit your source with DC offset - 0.9V, Amplitude = 50mV, Frequency = 1kHz
2. Go to **Configure Analysis -> Transisent**
3. Add **Stop time = x ms** (replace x with your desired value)
4. Add spie directive to your workspace and then run the simulation
5. Place the probe near the resistance (**A red probe will appear**)
6. Observe the grpahs
7. Also plot a curve for input

***Observations***

**CIRCUIT**

![Transient_ckt](https://github.com/user-attachments/assets/1990c466-8295-4c6e-9dee-512da7a2c6ad)

**INPUT**

![Transient(Vin_inc)](https://github.com/user-attachments/assets/d9ce155f-6359-470c-8fe2-2c6cd57159d6)

**OUTPUT**

![Transient(Vout_inc)](https://github.com/user-attachments/assets/99c4120a-35e1-4278-8650-91f10e6001d2)

We can calculate the gain from the $frac{Vo}{Vi}$ , which comes out to be $frac{1.24-1.12}{50m}$ = -2.4 (due to 180 phase shift)

We can also calculate gain from $A_v = -g_mR_{out}$
$A_v = -(0.104m)(25k) = -2.6$ 
This gain matches with the one calculated before, it is also important to note down the DC operating point here to verify that the MOSFET is in saturation
We can also calculate power consumption using this data

![DC_Operating_Point_25k](https://github.com/user-attachments/assets/76cef1db-e467-4b1e-9577-b347a5485fbb)

**Power Consumed** P = VI = 1.12169 * 27.132 $\mu$ A = 30.4 $\mu$ W (***Under specifier power budget***) 

Now we can move to AC analysis but before that it will be easy for analysis to take lower drain resistance, hence we take $R_D = 15k \ohm$

##### <ins>AC Analysis</ins>

This is also known as frequency and phase response

***Procedure***

1. Change your source and simply Add **"1"** to **Small Signal AC Analysis**
2. Go to **Configure Analysis -> AC Analysis -> Put "Decade" in "Type of Sweep" -> Put "20" in "Number of Points" -> Set "Start Frequency" as "0.1" and "Stop Frequency" as "1T" (terahertz)**
3. Add the spice directive to your workspace
4. Run the simulation
5. Place the cursor near the drain and resistor until you see a red probe and then click
6. You will get frequency and drain response

**CIRCUIT**

![Frequency Response](https://github.com/user-attachments/assets/27c36f07-399f-4c8f-bf75-f39902b34f3c)

**GRAPH**

![Frequency_Response_data](https://github.com/user-attachments/assets/8f76e5bf-11c4-4991-af14-384db7d0ef66)

This graph can help us calculate bandwidth, according to the graph the max gain = 9.6 dB then the frequency for -3dB gain = 16.5GHz but we don't have the data for F<sub>L</sub> this checks out as our circuit has no capacitors or filters which are the reason for low gain at the beginning of the curve hence, bandwidth cannot be determined at this stage

***SUMMARY***

1. Length (**L** = **600nm**)
2. Width (**W** = **592nm**)
3. **R<sub>D</sub> = 25 k $\ohm$**
4. Gain = **-2.5**
5. Bandwidth = Cannot be determined
6. At L > **300nm** the **W/L (Aspect Ratio) = 0.97899 (approximately)** 

#### <ins>Analysis of CS Amplifier with a Current Source Load</ins>

Now we replace the resistive load with PMOS the library you just attached has BSIM3 MOdel for PMOS as well
The circuit is as follows:

**CIRCUIT**

![PMOS](https://github.com/user-attachments/assets/970cbbaf-8abe-4106-a3ca-efe6f9aa06dc)

If you connect the gate and drain of PMOS together you will get a diode connected load and your PMOS will act as a resistor as shown below

**DIODE CONNECTED LOAD**

![Pmos](https://github.com/user-attachments/assets/74b627ef-7bd8-45e1-8fde-6e9787c5eb66)

But we will keep our discussion till current source load,

##### <ins> DC Operating Point </ins>

**<ins>Procedure</ins>**
1. Setup the circuit as shown above
2. Make sure to load the library file and add the spice directive to your workspace
3. Add **PMOS4** and change it's name to **CMOSP**
4. Get suitable value for W, L for PMOS by **hit and trial**
5. Perform a DC Sweep and get a value for **V<sub>b</sub>**
6. Repeat steps for DC operating point from previous condition

**<ins>Observations</ins>**
By hit and trial we get **L = 2 $\mu$ m and W = 0.2 $\mu$ m**
For the value of V<sub>b</sub> we did a DC Sweep

* **I<sub>D</sub> vs V<sub>b</sub>**
![PMOS_Vb](https://github.com/user-attachments/assets/55ab139b-340b-48aa-91bc-1b19d93dd8c7)

From the graph above it is apparent that we will get the current nearest to maximum permissible current somewhere near **V<sub>b</sub> = -5V**

Now that the values has been set we perform the DC Operation Point Analysis

* **DC Operation Point**

![PMOS-OP](https://github.com/user-attachments/assets/7deeb8c3-b283-47bd-9d57-897ca808cdc3)

Power Consumption = V * I = 1.11 V * 2.712E-05 A = **30.1 $\mu$ W** (Way under power budget) 

**CIRCUIT**
![PMOS_OPERATING](https://github.com/user-attachments/assets/6971440f-e83f-480d-af91-eff8834fc580)

We now perfrom drain and transfer characteristics of the circuit

* **Drain Characteristics**
![Drain_Characterstics_PMOS](https://github.com/user-attachments/assets/5a6e0181-1b09-4e91-9d46-eb45fa893a73)

Above is the drain characteristics, from the looks of it , it looks linear for some values that is due to current source

* **Transfer Characteristics**
![Transfer_Characterstics_PMOS](https://github.com/user-attachments/assets/f7f2e99f-6d08-4495-b66b-9e657421b6f8)

Above is the transfer characteristics, it is similar to the drain characteristics of the condition with resistive load

* **Voltage Transfer Characteristics**
![VTC_PMOS](https://github.com/user-attachments/assets/9dc27a6b-ca2d-42c1-9dad-8c6990891ba4)

##### <ins>Transient Analysis</ins>

Follow the same steps as in previous case 

**CIRCUITS**

![PMOS_TRANSIENT](https://github.com/user-attachments/assets/8c447467-9d6f-4d1f-83df-00b3e3e929ab)

**GRAPHS**

![Transient](https://github.com/user-attachments/assets/fea3423d-0bab-44cb-b994-9f2499cda0c0)

**Calculation**

$\frac{V_O}{V_i}$ = - $\frac{1.23 - 1.11}{50m}$ = **-2.4**

##### <ins> AC Analysis </ins>

Follow the same steps as in previous case

**CIRCUIT**

![PMOS_FREQUENCY_RESPONSE](https://github.com/user-attachments/assets/44a3b698-9525-44e6-a15d-1e42201ad5e8)

**GRAPH**

![FrequencyResponse_PMOS](https://github.com/user-attachments/assets/b957b76f-4656-4d59-a67d-7ba3507986f7)

-3dB Gain = **2.17 GHz**

#### <ins>INFERENCE</ins>
1. The term 180 nm technology specifies minimum length possible to be manufactured, we can easily manufacture transistors with higher value than these
2. At low values of length (L) the relation between current (saturation) and width (W) is no longer linear it deviates from the current equation due to short channel length effect, channel length modulation and other parameters
3. At high values the linear relation between W and current is maintained
4. We should be very carefull while changing the value of drain resistance as that can easily tip off the MOSFET from the saturation region we can use degeneration and voltage divider bias to overcome this problem of senstivity and add a source filter to remove the effect of degeneration
5. The lower cutoff of frequency response is not present in absence of filters in the circuit, higher cutoff is still there because it is caused by parasitic capacitance which is an intrinsic property of MOSFET
6. Value of drain resistance in this case is directly tied to the gain so increasing it will increase the gain however increasing it after a certain value will take the MOSFET to edge or out of Saturation which are not ideal or usable conditions for CS Amplifier
7. We may trade off some current for higher gain
8. Resistors take a lot of space in a circuit so we generally replace it with a MOSFET in diode connected load configuration, in this configuration V<sub>GD</sub> = 0 i.e gate and drain terminals are shorted together and hence MOSFET stays is linear region and acts as a resistor
9. One more exmaple that can increase gain with less or same power consumption is current source load configuration which we have done analysis for
10. The drain characteristics of this configuration has a linear region due to addition of current source and the transfer characteristic looks similar to drain characteristics of resistive load configuration
11. PMOS is in saturation region (from circuit diagram)
