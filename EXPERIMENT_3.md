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

**As we can see the total current is greater than 0.5 mA which is outside our power budget and thus makes it impractical for our use case, but the MOSFETs are still in saturation, the threshold voltage further increases as seen below also the tail node voltage is also changed**

![Vin_increase_op_log](https://github.com/user-attachments/assets/99a65c31-358f-418b-8570-3ed8a9fde512)

**Calculate maximum input swing and output swing**

V<sub>ICM<sub>min</sub></sub> = V<sub>T</sub> + V<sub>P</sub> (We are observing the condition of **cut-off**)
* V<sub>T</sub> = 0.497 V , V<sub>P</sub> = 0.4 V

**V<sub>ICM<sub>min</sub></sub> = 0.897 V**

Any signal that makes the gate voltage less than this value will give clipped output

V<sub>ICM<sub>max</sub></sub> = V<sub>OCM</sub> + V<sub>T</sub> (We are observing the condition of **MOSFET getting out of saturation region**)
* V<sub>T</sub> = 0.497 V , V<sub>OCM</sub> = 1.1 V

**V<sub>ICM<sub>max</sub></sub> = 1.597 V**

**Maximum Input Swing =  1.247 V** (This is the maximum value which our amplifier can provide input to without clipping, **however bear in mind this is a theoretical value there are many parameters we have not taken into considerations the symmetry of the sine output wave gets affected as early as 102 mV and so this value is for a perfect clipping anything beyond this The output will hit the supply rail or ground rail or both**)

* V<sub>OCM<sub>min</sub></sub> = V<sub>OV</sub> + V<sub>P</sub> (We are observing the **edge of saturation**)

**V<sub>OCM<sub>min</sub></sub> = (1 V - 0.497 V) + 0.4 V = 0.903 V**
* V<sub>OCM<sub>max</sub></sub> = V<sub>DD</sub> - I<sub>SS</sub> * R<sub>D</sub> (**We are observing cutoff**)

At maximum V<sub>OCM</sub> gate voltage will be zero according to voltage transfer characteristics which means there will be no current in the MOSFET

**V<sub>OCM<sub>max</sub></sub> = 2 V**

**Maximum Output Swing = 1.4515 V** (This is also a theoretical value even in simulations it will be very different)

**Gain equation using small signal model**

* G<sub>m</sub> (from DC Analysis) = 3.57 mA/V
* R<sub>D</sub> = 3.6 k $\ohm$, R<sub>SS</sub> = 800 $\ohm$
* A<sub>v</sub> = $\frac{-g_mR_D}{1 + g_mR_{SS}}$ = -3.332

The calculated gain and the gain obtained from the transient analysis are not the same, **there can be missing parameters that we might have overlooked**

##### Transient Analysis

Now we are ready for transient analysis, we take an input of 50mV (Amplitude)

![RSS_transient](https://github.com/user-attachments/assets/712d86a1-4440-406f-ac63-481e54216f79)

We can now calculate gain **A<sub>V</sub> = $\frac{1.3721712 V - 1.0994212 V}{950.22157 mV - 1.0001041}$ = -5.46 V/V**
There is **180 degree phase shift** 

##### AC Analysis
We have to perform the frequency response as we did in previous experiment, the results are below

![RSS_frequency_response](https://github.com/user-attachments/assets/7dde3f19-9a7b-4692-9289-c18e4d8b4d40)

Now we can calculate dB gain using transient analysis 

* **dB gain (Theoretical) = 20 log(A<sub>V</sub>) = 14.74 dB**
* **dB gain (From graph) = 15.038 dB** (close to theoretical value)
* **-3dB gain = 3.663 GHz**
* **Bandwidth = 3.663 GHz**

#### CASE 2 : With Current Source
##### Circuit Setup

![ISS_ckt](https://github.com/user-attachments/assets/f396347d-1fa9-4979-889a-37edcfb138d4)

##### DC Analysis
We have to give the current source the value of total current else it will violate the kirchoff's current law and will change the biasing of MOSFETs

![ISS_1 1_DC](https://github.com/user-attachments/assets/1b47b282-666d-47f4-b90e-4ba6c6e795f6)

The DC Operating Point and other DC Parameters is exactly the same as in previous case however something very interesting happens when we increase the V<sub>ICM</sub> to 1.1 V the operating point is still similar, MOSFETs are still in saturation region and we are still under our prescribed power budget thus this configuration **increases operation stability**

![ISS_1 1V](https://github.com/user-attachments/assets/183fb043-c1aa-403e-8d58-6d248c2e4efe)

**However there is change in output voltage**

This configuration will keep the swing same as before as R<sub>SS</sub> had no effect on input and output swing

Coming to gain the gain should increase as now thw gain is **A<sub>v</sub> = -g<sub>m</sub>R<sub>D</sub> = -12.852** (theoretical). However this gain is very different from the gain we are going to observe in the transient analysis

##### Transient Analysis

![ISS_Transient](https://github.com/user-attachments/assets/27ee21a0-08d4-4893-ab4b-d20db219c443)

Using this we can now calculate the gain using **A<sub>v</sub> = $\frac{1.3334705 V - 1.0997587 V}{950.35135 mV - 1.0000624 V}$ = -4.701 V/V**
There is a **180 degree phase shift**

This gain is much lower then the one we calculated and there are some good reasons for that
* Even though the gain should increase as an ideal current source has infinite output impedance in practicality less so, and thus due to this reason the gain is lower
* If we notice this gain is lower than R<sub>SS</sub> case as well, this may have happened due to decrease in **Common Mode Rejection Ratio** which directly affects differential gain.
* We have not yet accounted for the channel length modulation which can actually substantially decrease the gain

With this analysis we can now move on to AC Analysis

##### AC Analysis

![ISS_AC_ANALYSIS](https://github.com/user-attachments/assets/fc5b50f7-6809-450f-bf53-ed51cdb66e8d)

* **dB gain (Theoretical) = 20 log(A<sub>V</sub>) = 13.44 dB**
* **dB gain (From graph) = 13.54 dB** (close to theoretical value)
* **-3dB gain = 3.85 GHz**
* **Bandwidth = 3.85 GHz**

Now we can move to our final case 

#### CASE 3 : With NMOS
##### Circuit Setup

![NMOS-3-ckt-setup](https://github.com/user-attachments/assets/cd4a232a-3174-423a-bfb9-c973a965e3a9)

##### DC Analysis

Before moving forward we have to set gate voltage and aspect ratio so we assume L = 180nm, we perform two parameter sweeps separately for W and V and we get following information

![MOS_Sweeps](https://github.com/user-attachments/assets/4b51ee16-abda-4118-8f58-5c00ca6d92a7)

Here we choose 700 mV as our gate voltage and then perform a parameter sweep again and find particular value of W

![IDvs_W_MOSFET](https://github.com/user-attachments/assets/65f3be39-b5d7-4118-80ee-b239511f68f6)

From the curve we get **W = 14.156872 $\mu$ m** and then we can proceed with operating point calculations

![M3_Data](https://github.com/user-attachments/assets/edd6e062-5d4c-481e-bf44-4921dc2ee31c)

The other parameters are still same with this we can move on to transient analysis

##### Transient Analysis

![transient_nmos](https://github.com/user-attachments/assets/7f23c1ba-2452-43b7-b143-ca95994e6068)

Gain = **A<sub>v</sub> = $\frac{1.3415149 V - 1.0997433 V}{950.33984 mV - 1.0000624 V}$ = -4.862 V/V** 
There is a **180 degree phase shift**

We can now move to AC Analysis

##### AC Analysis

![NMOS_frequency_response](https://github.com/user-attachments/assets/83de25b1-ea75-40a5-97ea-2644e253a219)

* **dB gain (Theoretical) = 20 log(A<sub>V</sub>) = 13.74 dB**
* **dB gain (From graph) = 13.87 dB** (close to theoretical value)
* **-3dB gain = 3.85 GHz**
* **Bandwidth = 3.85 GHz**

### Inferences
After all that back and forth what do we learn from all that analysis

1. Be sure you know all the parameters we have missed some parameters and their effect that's why our theoretical and practical gain is not matching
2. We calculate some value for input and output swing but distortions and clipping starts with much smaller signals this can be attributed to various factors including channel width modulation and other factors
3. Even though the gain should increase as an ideal current source has infinite output impedance in practicality less so, and thus due to this reason the gain is lower. If we notice this gain is lower than R<sub>SS</sub> case as well, this may have happened due to decrease in **Common Mode Rejection Ratio** which directly affects differential gain. We have not yet accounted for the channel length modulation which can actually substantially decrease the gain
4. Note that the AC / Transient Analysis we have applied an input AC Voltage is given at only one end.This helps to better analyse the analysis part. However adding the 180 deg phase shift signal to other end increases the gain as the difference of these 2 signals increases.
5. **Common-Mode Input and Output Range:** The **common-mode input voltage** range was found to be **0.897 V to 1.597 V**, while the **common-mode output voltage** range was **0.903 V to 2 V**, defining the operational limits.
6. The threshold voltage changes for each MOSFET due to body effect
7. All the configurations have a 180 degree phase shift

![summary](https://github.com/user-attachments/assets/7f165db9-8323-495c-b1a1-e2123b272697)

8. A lot of parameters of current source and MOSFET are common this is due to the reason in real world application we use FETs as constant current source
9. For any differential amplifier the best amplification and the most stable operating point if with an ideal current source
10. The gain of current source should be higher but it is less due to reasons mentioned in above points
