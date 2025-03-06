## Experiment - 3 {Analysis of Differential Amplifier}
## Question
Design a differential amplifier for the following specifications **Using LTSpice**
* V<sub>DD</sub> (Supply) = 2 V
* P (Power Budget) = 1 mW
* V<sub>ICM</sub> (Gate Voltage) = 1 V (Input)
* V<sub>OCM</sub> (Drain Voltage) =  1.1 V (Output)
* V<sub>P</sub> (Tail Voltage) = 0.4 V

Perform **DC Analysis**, **Transient Analysis**, **Frequency Response** and find out required parameters

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
