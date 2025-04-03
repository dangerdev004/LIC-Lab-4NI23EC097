# Experiment - Analysis of Current Mirror

## Question
Design and analyze current mirror circuit as active load in amplifier circuit
1. Design for A<sub>v</sub> > -10 V/V , V<sub>DD</sub> = 1.8 V, P <= 1 mW
2. Design a differential amplifier with current mirror as per experiment 3 and perform DC, Transient and AC Analysis

## [Theory](https://www.allaboutelectronics.org/what-is-current-mirror-mosfet-current-mirror-explained/)
What is Current Mirror?

The current mirror is an analog circuit that senses the reference current and generates the copy or number of copies of the reference current, with the same characteristics. The replicated current is as stable as the reference current source. The replicated current could be the same as the reference current (Icopy = IREF), or it could be either multiple or fraction of the reference current. 
(Icopy = N*Iref or Icopy = (1/N)*IREF).

![image](https://github.com/user-attachments/assets/6da1b67e-8502-46cf-a8cd-adac8b92e048)

Why Current Mirrors are used?

Current Mirrors are particularly useful in the integrated circuits, for biasing the amplifiers. The advantage of biasing the amplifiers with the current source is that it provides a high voltage gain and good biasing stability. This current source can be generated using a simple PMOS transistor or using a MOS transistor in cascode configuration (to achieve higher gain) as shown in Fig.2.

![image](https://github.com/user-attachments/assets/9658281a-492e-46c8-b3b3-ec8308aed465)

But this type of MOS current source (shown in Fig.2) is susceptible to the change in the biasing voltage and the change in temperature. Moreover, the integrated circuit may contain hundred or thousand of such amplifiers. To bias all the amplifiers with precise biasing voltage is another challenge. So, to overcome all these problems, in integrated circuits, one stable current source is fabricated within IC, and using the current mirror the multiple copies of the stable current source is generated (which can be used to bias the amplifiers)

MOSFET- Current Mirror

Fig.3 shows a current mirror circuit using the NMOS transistor. The reference current is converted to the voltage using diode connected transistor and the same is applied between the gate and the source of the another MOSFET.

![image](https://github.com/user-attachments/assets/b4a93552-ceb3-4c4a-aa57-c579d588aca4)

The relation between the ID1 and IREF can be given by the following expression.

![image](https://github.com/user-attachments/assets/44f24a9d-6c39-46a0-b9fe-ce541b36ef2d)

By changing the W/L ratio of the two transistors, the current which is fraction or multiple of the reference current can be generated. The only thing which needs to be ensured is that, the MOSFET should operate in the saturation region.

Effect of Channel Length Modulation on Current Mirror

So far during the discussion, the effect of channel length modulation was neglected. If the channel length modulation effect is also considered, then as shown in Fig. 4, as the drain to source voltage (VDS) of the MOSFET increases, the drain current also slightly increases.

![image](https://github.com/user-attachments/assets/2e706b66-d159-4013-8195-4079cd265615)

Considering the channel length modulation effect, if VDS of MOSFET M1 changes by ΔVDS then the drain current ID1 also changes to ID1 + ΔID1. The same is shown in Fig. 5.

![image](https://github.com/user-attachments/assets/7f7d1fd8-a78b-4234-ab62-95a17c8e19bb)

The effect of channel length modulation can be reduced by increasing the length of the channel for the given W/L ratio.

PMOS Current Mirror

Fig. 6 shows the implementation of current mirror using the PMOS transistors. In PMOS current mirror, the source terminals for both transistors are connected to Supply voltage Vdd.

![image](https://github.com/user-attachments/assets/ce7e73e0-52e9-4ed1-9a2a-68a9981a5f66)

The relation between the ID1 and IREF can be given by the same expression.

![image](https://github.com/user-attachments/assets/0d84a610-1bfa-440c-9bbb-f791fdfccc20)

The only thing which needs to be ensured is that M1 should operate in the saturation region. Or in other words, VSD1 ≥ VSG – |VTP |, Where VTP is the threshold voltage of the PMOS transistor.

## Design
Total Current = I = 10<sup>-3</sup>/1.8 A = 0.555 mA
1. For current ratio 1:1

    I = I<sub>ref</sub> + I<sub>x</sub>

   I<sub>ref</sub> = I<sub>x</sub> = 0.277 mA

2. For current ratio 1:2

    I = I<sub>ref</sub> + I<sub>x</sub>

   2 * I<sub>ref</sub> = I<sub>x</sub> = 0.3703 mA, I<sub>ref</sub> = 0.1851 mA

## ANALYSIS
## Question 1
### CASE 1a : L = 180 nm (1 : 1)
#### Circuit Setup

![Circuit_diagram](https://github.com/user-attachments/assets/1d52c037-1729-497d-8946-bd992b5aac69)

#### DC Analysis

![DC_op](https://github.com/user-attachments/assets/1f2dad89-6388-4a8b-b7d0-85cafd4acc19)

#### Transient Analysis

![transient](https://github.com/user-attachments/assets/c87eb2dc-d0a7-4d6e-abda-c1b3e6296a3a)

#### AC Analysis

![Ac_Analysis](https://github.com/user-attachments/assets/a3739601-9bf5-4a86-be3a-829b728c2c75)


### CASE 1b : L = 500 nm (1 : 1) 
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/a40002b0-33da-45ff-8f31-eaa4316b900d)


#### DC Analysis

![DC_OP](https://github.com/user-attachments/assets/001795bd-6c23-4e95-b0a4-f5e17d8ef3c5)


#### Transient Analysis

![transient](https://github.com/user-attachments/assets/95fffd62-73ac-473f-b664-9b00ada49211)


#### AC Analysis

![AC](https://github.com/user-attachments/assets/2eb61aab-b1b6-4ed0-95e6-5311db255c8c)


### CASE 1c: L = 1 um (1 : 1)
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/567ced08-7e21-43e9-9803-1b78a9a208c6)


#### DC Analysis

![DC_Op](https://github.com/user-attachments/assets/dfadc30a-dfb2-4622-8880-34182ede823c)



#### Transient Analysis

![Transient](https://github.com/user-attachments/assets/0199a497-aa1a-4cb6-8c53-8f294e00af4b)


#### AC Analysis

![AC](https://github.com/user-attachments/assets/4524ef42-4995-4f94-84d6-f9837c97bb34)

### CASE 2a: L = 180 nm (1 : 2)
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/936d9821-7894-49be-ade6-ef56e64d3979)


#### DC Analysis

![Dc_op](https://github.com/user-attachments/assets/7a8614d4-4ef7-4513-8262-dc54c4765213)



#### Transient Analysis

![transient](https://github.com/user-attachments/assets/b23aa9e2-9ec8-457e-9154-6e96b6da170c)


#### AC Analysis

![AC](https://github.com/user-attachments/assets/6750db12-64bb-46b0-af6f-930506150b1c)

### CASE 2b: L = 500 nm (1 : 2)
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/936d9821-7894-49be-ade6-ef56e64d3979)


#### DC Analysis

![DC_Op](https://github.com/user-attachments/assets/0a23a4b8-d07f-4cad-ba71-13c0d1e3a0af)


#### Transient Analysis

![Transient](https://github.com/user-attachments/assets/264704a8-b80e-4cc2-9440-80f63206c621)


#### AC Analysis

![AC](https://github.com/user-attachments/assets/592d3ded-ce8c-4da1-b236-7a6974834b64)

### CASE 2c: L = 500 nm (1 : 2)
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/936d9821-7894-49be-ade6-ef56e64d3979)


#### DC Analysis

![DC_op](https://github.com/user-attachments/assets/d510b795-ba09-4f93-8cbc-41a43bb97fbd)


#### Transient Analysis

![Transient](https://github.com/user-attachments/assets/282b4e19-b20a-4ea9-ac99-1873e8209d74)


#### AC Analysis

![AC](https://github.com/user-attachments/assets/41d70e45-4245-4d7d-a23d-0228a310ce37)

#### Table of results

| Length | Ratio | PMOS 1      | PMOS 2      | NMOS    | VGS (NMOS) | Gain (V/V)   | Bandwidth |
|--------|-------|-------------|-------------|---------|------------|--------------|-----------|
| 180n   | 1:1   | 10µ         | 10µ         | 2.179µ  | 0.9        | 9.67         | 886.2 MHz |
| 500n   | 1:1   | 3.245831µ   | 3.245831µ   | 5.71µ   | 0.9        | 11.95 (5.3µ) | 1.699 GHz |
| 1u     | 1:1   | 6.4719825µ  | 6.4719825µ  | 10.24µ  | 0.9        | 9.45 (9.6µ)  | 1.029 GHz |
| 180n   | 1:2   | 10µ         | 20µ         | 3µ      | 0.9        | 11.7         | 398.8 MHz |
| 500n   | 1:2   | 3.245831µ   | 6.491662µ   | 7.7µ    | 0.9        | 9.95 (7µ)    | 1.027 GHz |
| 1u     | 1:2   | 6.4719825µ  | 12.943965µ  | 13.7µ   | 0.9        | 11.3 (12.8µ) | 656.2 MHz |

## Question 2
#### Circuit Setup

![Circuit_Diagram](https://github.com/user-attachments/assets/6716766d-aa74-4680-94c2-3388de8f3ef3)


#### DC Analysis

![DC_Op](https://github.com/user-attachments/assets/773dcde3-f2f5-4b68-9b39-8f9198d72995)


#### Transient Analysis

![Transient](https://github.com/user-attachments/assets/783b27cb-5401-444f-bf37-93b01d38b892)

**Gain = -25.56 V/V**

#### AC Analysis

![AC](https://github.com/user-attachments/assets/e9129446-1e30-44cc-8ea9-821bf27e6ca9)

**Bandwidth = 745.42 MHz** 

#### Table of results 

| NMOS 1        | NMOS 2        | PMOS 3       | PMOS 4       | NMOS 5        | NMOS 6        | Gain  |
|--------------|--------------|--------------|--------------|--------------|--------------|-------|
| 180n / 10u  | 180n / 22.3446u | 180n / 10u  | 180n / 10u  | 180n / 19.379518u | 180n / 19.379518u | 25.56|


## Inferences
#### **1. Current Mirror Design & Deviations from Ideal Ratios**
- Practical **W/L ratios** deviate from theoretical values (e.g., 10µm/22.345µm instead of 10µm/20µm for 1:2 ratio).
- **Reasons for deviation:**
  - **Channel length modulation** (λ effect) alters drain current.
  - **Threshold voltage mismatches** due to process variations.
  - **Body effect** shifts threshold voltage (V<sub>TH</sub>).
  - **Finite output resistance** affects current accuracy.
- **Fix:** Adjust transistor width (W) to compensate for non-idealities.



#### **2. Trade-offs Between Current, Gain & Bandwidth**
- **Higher current → Higher gain**, but increases **power dissipation & noise**.
- **Gain vs. Bandwidth trade-off:**
  - Higher gain → Increased **Miller capacitance** → Lower bandwidth.
  - Lower gain → Higher bandwidth.
- **We may need to decrease current in a branch to make sure the device is in saturation region for proper amplification**
- **Empirical Data:**

  | **W/L (μm/μm)** | **Current Ratio** | **Gain (V/V)** | **Bandwidth (MHz)** |
  |-----------------|------------------|---------------|----------------|
  | 10/10 (1:1) | 1:1 | 9.67 | 886.2 |
  | 3.24/3.24 (1:1) | 1:1 | 11.95 | 1699 |
  | 10/20 (1:2) | 1:2 | 11.7 | 398.8 |
  | 3.24/6.49 (1:2) | 1:2 | 9.95 | 1027 |
  

#### **3. Why & When to Use Cascoded Current Mirrors?**
- **Issues with simple current mirrors:**
  - Low **output resistance** limits gain.
  - **Channel length modulation** reduces accuracy.
- **Cascoding Benefits:**
  - **Higher output resistance** → Improved gain stability.
  - **Reduced λ effect** → More precise current mirroring.
  - **Better linearity & matching**.
  - **Improved Common-Mode Rejection Ratio (CMRR)**.
- **When to use cascoding?**
  - **Higher gain requirements** without excessive bandwidth loss.
  - **High-frequency applications**
  - **Precision analog circuits**


#### **Final Conclusion**
- **Current mirror as active load boosts gain & stability**, but real-world effects require **fine-tuning of W/L ratios**.
- **Balance between gain, bandwidth, and power** depends on application.
- **Cascoding improves performance but adds complexity**—use when necessary for high-precision designs.

