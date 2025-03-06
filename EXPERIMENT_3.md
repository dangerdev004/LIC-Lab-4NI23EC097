## Experiment - 3 {Analysis of Differential Amplifier}
## Question
Design a differential amplifier for the following specifications **Using LTSpice**
* V<sub>DD</sub> (Supply) = 2 V
* P (Power Budget) = 1 mW
* V<sub>ICM</sub> (Gate Voltage) = 1 V (Input)
* V<sub>OCM</sub> (Drain Voltage) =  1.1 V (Output)
* V<sub>P</sub> (Tail Voltage) = 0.4 V

Perform **DC Analysis**, **Transient Analysis**, **Frequency Response** and find out required parameters

**Please refer to previous experiment if you don't know the steps to carry out analysis in LTSpice**

**NOTE: Theory portion is taken from Sedra Smith Book Chapter 9 (Page no. 594)**
### Theory (From Sedra - Smith)
Figure below shows the basic MOS differential-pair configuration. It consists of two matched transistors, Q<sub>1</sub> and Q<sub>2</sub> , whose sources are joined together and biased by a constant-current source I. The latter is usually implemented by a MOSFET circuit of the type studied earlier. For the time being, **we assume that the current source is ideal and that it has infinite output resistance**. Although each drain is shown connected to the positive supply through a resistance R<sub>D</sub> , in most cases active (current-source) loads are employed, as will be seen shortly. For the time being, however, we will explain the essence of the differential-pair operation utilizing simple resistive loads. Whatever type of load is used, **it is essential that the MOSFETs not enter the triode region of operation.**

![image](https://github.com/user-attachments/assets/b7deed39-0114-4712-8ceb-d2f8ce13b2d6)

**Advantages of Differential Amplifiers**
* Robust operation → noise do not affect its performance
* Higher output voltage swing
* Higher gain in comparison to single-stage amplifiers
* Linear Performance and simpler biasing
* Doesn't require coupling capacitors, thus increasing bandwidth

### Design
We have performed some basic calculations based on our specification and the **required parameters** are listed below
* I<sub>SS</sub> = 500 $\mu$ A (Total Bias Current)
* I<sub>D<sub>1</sub></sub> = I<sub>D<sub>1</sub></sub> = 250 $\mu$ A (Branch currents are equal due to symmetry of circuit)
* R<sub>D<sub>1</sub></sub> = R<sub>D<sub>1</sub></sub> = 3.6 k $\ohm$
* R<sub>SS</sub> = 800 $\ohm$ (Tail Resistance)
* Q point = (V<sub>DS</sub> = 0.7 V, I<sub>D</sub> = 250 $\mu$ A) @ V<sub>GS</sub> = 0.6 V

### ANALYSIS
#### CASE 1 : With R<sub>SS</sub>
##### Circuit Setup

![RSS_Circuit_Setup](https://github.com/user-attachments/assets/a1d346b9-a9c4-4659-97e8-2dfe3beeff9c)

##### Prerequisites
Before we start with finding DC Operating point it is important we setup L and W **(Aspect Ratio)** of our MOSFETs, we set our L (Channel length) = 180 nm and then perform a parameter sweep for W(Width) we can then use this to get the exact branch current from our design from our graph we got **W = 19.35 $\mu$ m** (approximately) 

![IDvsW](https://github.com/user-attachments/assets/59e3e6e5-0701-4949-970e-aa75e9269c8f)

Now with that settled we can move forward with DC Analysis
##### DC Analysis
We now find the DC Operating Point of the circuit 

![RSS_OP_POINT](https://github.com/user-attachments/assets/34f9a3d7-e392-4064-8867-37fee6bae68a)

**Output Log**

![RSS_OP_POINT_OP_LOG](https://github.com/user-attachments/assets/b610616c-87ba-4627-a47e-826d323b8a10)

This data is according to our design specifications. 

**However pay attention to the threshold voltage we know that in the SPICE Netlist the threshold voltage is mentioned as 0.366 V but while doing DC Analysis the threshold voltage is now 0.497 V, this is due to body effect.**

Now we increase V<sub>ICM</sub> to 1.1 V  

![Vin_increase](https://github.com/user-attachments/assets/22e85561-6b7f-4a28-aed4-26c04412caa2)

**As we can see the total current is greater than 0.5 mA which is outside our power budget and thus makes it impractical for our use case, but the MOSFETs are still in saturation, the threshold voltage further increases as seen below**

![Vin_increase_op_log](https://github.com/user-attachments/assets/99a65c31-358f-418b-8570-3ed8a9fde512)

**Calculate maximum input swing and output swing**

V<sub>ICM<sub>min</sub></sub> = V<sub>T</sub> + V<sub>P</sub> (We are observing the condition of **cut-off**)
* V<sub>T</sub> = 0.497 V , V<sub>P</sub> = 0.4 V
**V<sub>ICM<sub>min</sub></sub> = 0.897 V**

Any signal that makes the gate voltage less than this value will give clipped output

V<sub>ICM<sub>max</sub></sub> = V<sub>OCM</sub> + V<sub>T</sub> (We are observing the condition of **MOSFET getting out of saturation region**)
* V<sub>T</sub> = 0.497 V , V<sub>OCM</sub> = 1.1 V

**V<sub>ICM<sub>max</sub></sub> = 1.59V V**

**Maximum Input Swing = 0.7 V** (This is the maximum value which our amplifier can provide input to without clipping, **however bear in mind this is a theoretical value there are many parameters we have not taken into considerations the symmetry of the sine output wave gets affected as early as 102 mV and so this value is for a perfect clipping anything beyond this The output will hit the supply rail or ground rail or both**)

* V<sub>OCM<sub>min</sub></sub> = V<sub>OV</sub> + V<sub>P</sub> (We are observing the **edge of saturation**)

**V<sub>OCM<sub>min</sub></sub> = (1 V - 0.497 V) + 0.4 V = 0.903 V**
* V<sub>OCM<sub>max</sub></sub> = V<sub>DD</sub> - I<sub>SS</sub> * R<sub>D</sub> (**We are observing cutoff**)

At maximum V<sub>OCM</sub> gate voltage will be zero according to voltage transfer characteristics which means there will be no current in the MOSFET

**V<sub>OCM<sub>max</sub></sub> = 2 V**

**Maximum Output Swing = 1.097 V** (This is also a theoretical value even in simulations it will be very different)


**Gain equation using small signal model**

##### Transient Analysis

Now we are ready for transient analysis, we take an input of 50mV (Amplitude)

![RSS_transient](https://github.com/user-attachments/assets/712d86a1-4440-406f-ac63-481e54216f79)

We can now calculate gain **A<sub>V</sub> = $\frac{1.3721712 V - 1.0994212 V}{950.22157 mV - 1.0001041}$ = -5.46 V/V**

##### AC Analysis
We have to perform the frequency response as we did in previous experiment, the results are below

![RSS_frequency_response](https://github.com/user-attachments/assets/7dde3f19-9a7b-4692-9289-c18e4d8b4d40)

Now we can calculate dB gain using transient analysis 

* **dB gain (Theoretical) = 20 log(A<sub>V</sub>) = 14.74 dB**
* **dB gain (From graph) = 15.038 dB** (close to theoretical value)
* **-3dB gain = 3.663 GHz** 
