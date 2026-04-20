# Simple Overdrive Effect
---

## 1. Project overview
---
## 2. Block diagram
---
## 3. Circut analisys math derivition

<details>
<summary><b>Click to read about mathematical derivisions</b></summary>

### 3.1 Derivasion of cutoff frequency of coupling/decoupling capacitor

In this derivision we consider loaded decouplig capacitor which makes lowpass filter (integrating circuit).
The last derived equasion in 3.1 is identical for coupling capacitor working with resistance (differentiating circuit), but it is different on laplace's s-domain, and in fourier analisys (phase and magnitude plots).

#### Voltage devider equasion:
$$U_{out}=U_{in} \cdot \frac{Z_L}{Z_L+Z_R}$$
$$U_{out}=U_{in} \cdot \frac{\frac{Z_C Z_{Ro}}{Z_C+Z_{Ro}}}{\frac{Z_C Z_{Ro}}{Z_C+Z_{Ro}}+Z_R} = U_{in} \cdot \frac{Z_C Z_{Ro}}{Z_C Z_{Ro}+Z_C Z_{R}+Z_RZ_{Ro}}$$

#### Laplace's s-domain impedances derivition
Definition of Laplace's transform:

$$F(s) = L[f(t)] = \int_{0}^{\infty} f(t) e^{-st} \, dt \Rightarrow L\left[\frac{d^nf(t)}{dt^n}\right] = s^nF(s)$$

considering no initial conditions.

Impedance of resistance $Z_R$: 

$$U=I\cdot R$$
<!-- $$\mathcal{L}\{U\}=\mathcal{L}\{I\cdot R\}$$ -->
$$L[U]=R\cdot L[I]$$
$$Z_R(s)=\frac{U(s)}{I(s)}=R$$

Impedance of capacitance $Z_C$:

$$I=C\cdot \frac{dU}{dt}$$
$$L[I]=C\cdot L[U']$$
$$I(s)=C\cdot sU(s)$$
$$Z_C(s)=\frac{U(s)}{I(s)}=\frac{1}{sC}$$

#### Substituting s-domain impedances to voltage divider equation:

$$G(s)=\frac{U_{out}}{U_{in}}=\frac{\frac{R_o}{sC}} {\frac{R_o}{sC}+\frac{R}{sC}+RR_o}=\frac{R_o}{R_o+R+sCRR_o}$$
$$G(s)=\frac{(\frac{R_o}{R_o+R})}{1+s(\frac{CRR_o}{R_o+R})}$$

Then:

$$\boxed{G(s)=\frac{K}{1+sT}},\qquad   \boxed{K=\frac{R_o}{R_o+R}},\qquad   \boxed{T=\frac{CRR_o}{R_o+R}}$$

---

#### Amplitude characteristic - Fourier analysis
Complex s-plain argument definition: $s = \sigma+j\omega$. To get amplitude characteristic we need to analyse holomorphic furier transform function. To achive that we need to get rid of real part of s-plane (constant component $e^\sigma$).

$$G(j\omega)=\frac{K}{1+j\omega T}\cdot\frac{1-j\omega T}{1-j\omega T}=\frac{K-j\omega KT}{1+\omega^2 T^2}$$
$$G(j\omega)=\left[\frac{K}{1+\omega^2 T^2}\right] + j\left[\frac{-\omega KT}{1+\omega^2 T^2}\right]$$


<!-- ![](img\desmos_decoupling_Fourier.svg)(https://www.desmos.com/calculator/vwyactze44) -->
$P(\omega)\left[Q(\omega)\right]$ characteristics:
<p align="center">
  <img src="img\desmos_decoupling_Fourier.svg" width="400" alt="Podpis alternatywny">
</p>
<p align="center">
    (https://www.desmos.com/calculator/vwyactze44)
</p>
To derive amplitude-frequency function we must analyse mod.

$$|G(j\omega)|=\sqrt{\frac{K^2}{(1+\omega^2 T^2)^2}+\frac{\omega^2 K^2 T^2}{(1+\omega^2 T^2)^2}}=\frac{K}{\sqrt{1+\omega^2 T^2}}$$

Finding -3dB frequency will be done based on magnitude.

$$A=20\cdot \log\left(\frac{K}{\sqrt{1+\omega^2 T^2}}\right)$$

Cutoff condition:

$$ A(\omega_{-3dB})=A(0)-3$$

$$ 20\cdot \log\left(\frac{K}{\sqrt{1+\omega^2 T^2}}\right)=20\cdot \log\left(\frac{K}{\sqrt{1+0^2 T^2}}\right)-3$$
$$ 10\left[\log\left(\frac{K^2}{(1+\omega^2 T^2)}\right)-\log\left(K^2\right)\right]=-3$$
$$ \log\left(\frac{1}{(1+\omega^2 T^2)}\right)=-0,3$$
$$ \frac{1}{(1+4\pi^2f^2 T^2)}=10^{-0,3}$$
$$ 10^{-0,3}+10^{-0,3}4\pi^2f^2 T^2=1$$
$$ f=\sqrt{\frac{\frac{10^{-0,3}}{1-10^{-0,3}}}{4\pi^2T^2}} \approx \frac{1}{2\pi T}$$
Substitute T:
$$f=\frac{R_o+R}{2\pi CRR_o}=\frac{R}{2\pi CRR_o}+\frac{R_o}{2\pi CRR_o}$$

$$\boxed{f=\frac{1}{2\pi RC}+\frac{1}{2\pi R_oC}}$$

---

### 3.2 Derivasion of voltage divider resistance values

We consider loaded symetric voltage divier

#### Impedance

$$R_{eq1}=\frac{RR_o}{R+R_o}$$
$$\lim_{R_o \to \infty} R_{eq1}= \lim_{R_o \to \infty}\frac{R}{\frac{R}{R_o}+1}=R$$
$$R_{eq}=2\cdot R$$

#### Flowing current loss

$$I=\frac{V_{cc}}{R_{eq}}=\frac{V_{cc}}{2R}$$

#### Thevenin's resistance

$$R_{TH}=\frac{RR}{R+R}=\frac{R}{2} \Rightarrow R = 2\cdot R_{TH}$$

#### Current loss vs Thevenin's resistance

Substituting both equations:

$$\boxed {I(R_{TH})=\frac{V_{cc}}{4\cdot R_{TH}}}$$

Ideal voltage source should have $R_{TH} \to 0$, to be as stable as possible. Ideal current loss should be $I \to 0$. Graphing this function allow to pick optimal resistance values.

$I(R_{TH})$  with $V_{cc}=9V$ characteristics:
<p align="center">
  <img src="img\desmos_voltage_divider_I(Rth).svg" width="400" alt="Podpis alternatywny">
</p>
<p align="center">
    (https://www.desmos.com/calculator/zl9quwhx7r)
</p>

---

### 3.3 Derivasion of pullup resistor value

Considering methodology of choosing pullup resistors, low potential on signal line should not draw much current.
On the other hand, operational amplifier has its bias current which will be drawn no matter what. It limits upper value of resistance, voltage drop on this resistor should not affect effect.

In project LM358 was used, so its bias current is around $45 nA = 45\cdot 10^{-9} A$

$$ U = I\cdot R $$
$$ R = \frac{U_{loss}}{45\cdot 10^{-9}}$$

Characteristics:
<p align="center">
  <img src="img\desmos_pullup_R.svg" width="400" alt="Podpis alternatywny">
</p>
<p align="center">
    (https://www.desmos.com/calculator/fuyu1ywsum)
</p>

---

### 3.4 Operational amplifiers

Op amps has very high input impedance ($ Z_{in} \to \infty $) and very low output impedance ($ Z_{out} \to 0 $).
They can be analised using 2 rules:
1. Op amps try to sustain same potential on both of its inputs,
2. Op amps bias current is negligible small (often $I \to 0$).

</details>

---

## 4. Element selection

<details>
<summary><b>Click to read about elements selection</b></summary>

### 4.1 Voltage divider

Using $I(R_{TH})=\frac{V_{cc}}{4\cdot R_{TH}}\qquad$ (3.2).
Voltage divider should not drain more than $0.5 mA$, so:

$$0.5 \cdot 10^{-3} > \frac{9}{4\cdot R_{TH}}$$
$$2 \cdot 10^{-3} \cdot R_{TH} > 9$$
$$R_{TH} > 4,5 \cdot 10^3 \Rightarrow R_{1,2} > 9 k\Omega$$
$$\boxed{R_{1,2} = 10 k\Omega}$$

### 4.2 Pullup resistor

Using $ R = \frac{U_{loss}}{45\cdot 10^{-9}}$ (3.4).
Maximal acceptable voltage drop is around $0,05 V$, so:
$$R_3 = \frac{0,05}{45\cdot 10^{-9}} \approx 1,111 \cdot 10^6 \Omega \approx 1 M\Omega$$
$$\boxed{R_3 = 1M\Omega}$$

### 4.3 Input resistor

### 4.4 Filtering potentiometers

Potentiometers were chosen based on availability and functionality.
Picking $ 10k\Omega $ potentiometers grants optimal selection of coupling and decoupling capacitors to work with.
$$ \boxed{R_{V2,V3} = 10k\Omega}$$

<!-- Minimal voltage increase should be higher than $0,6V$ to allow diodes to work, so based on guitar voltage ($10 mV$) we can derive minimal gain.
$$ k_{min} = \frac{U_{out}}{U_{min}} = \frac{0,6}{0,01} = 60 \Rightarrow  $$  -->


### 4.5 Coupling/decoupling capacitors

Main passive filtering is done by two segments.

Using buffer alows to separate 2 filters. Load resistance in approximation infinitely small. Derived equasion looks like this (3.1):
$$ \lim_{R_o \to \infty} f= \lim_{R_o \to \infty} \frac{1}{2\pi RC}+\frac{1}{2\pi R_oC} = \frac{1}{2\pi RC}+\frac{1}{2\pi \infty C} = \frac{1}{2\pi RC}$$

High pass maximal cutoff point - 40Hz:
$$ 60 = \frac{1}{2\pi \cdot 10000 \cdot C }\Rightarrow C = \frac{1}{2\pi \cdot 10000 \cdot 10} \approx 3,18 \cdot 10^{-6}$$
$$ \boxed{C_6 = 3,3 \mu F} $$

Low pass maximal cutoff point - 5 kHz:
$$ 5000 = \frac{1}{2\pi \cdot 10000 \cdot C }\Rightarrow C = \frac{1}{2\pi \cdot 10000 \cdot 5000} \approx 3,18 \cdot 10^{-9} F$$
$$ \boxed{C_7 = 3,3 nF} $$

### Main op amp feedback loop

Using 2 rules described in 3.4, non-inverting amp can be modeled with:
$$ U_{in} = U_{+} = U_{-} = Z_1 \cdot I $$
$$ U_{out} = U_{Z_1} + U_{Z_2} = I\cdot Z_1 + I\cdot Z_2 \Rightarrow I = \frac{U_{out}}{Z_1 + Z_2} $$
$$ G(s) = \frac{Z_2 (s)}{Z_1(s)} + 1 $$

In this effect we are abling user to regulate $Z_2$ (diode type, potentiometer and capacitor). We use capacitor $C_4$ to limit gain for DC current.
Considering only $1M\Omega$ potentiometer and using information derived in 3.1:
$$ G(s) = \frac{R_{V1}}{R_5+ \frac{1}{sC_4}} + 1 = \frac{sR_{V1} C_4}{sR_5 C_4 + 1} + 1 = \frac{1 + sC_4(R_{V1} + R_5)}{1 + sR_5C_4}$$

To calculate gain in somewhat same way that we derived 3.1 $s = j\omega$:

$$G(j\omega) = \frac{1 + j\omega C_4(R_{V1} + R_5)}{1 + j\omega R_5C_4} = [\frac{1+\omega^2 C_4^2 R_5 (R_{V1}+R_5)}{1+\omega^2 R_5^2 C_4^2}] + j [\frac{\omega C_4 R_{V1}}{1+\omega^2 R_5^2 C_4^2}]$$
$$ |G(j\omega)| = \sqrt{Re[G(j\omega)]^2+Im[G(j\omega)]^2} = \sqrt{\frac{1 + \omega^2 C_4^2(R_{V1} + R_5)^2}{1 + \omega^2 R_5^2 C_4^2}} $$

So impedance for DC current is:
$$ \lim_{\omega \to 0} |G(j\omega)| = 1$$

So impedance for high frequency AC current is:
$$ \lim_{\omega \to \infty} |G(j\omega)| = \frac{R_{V1}}{R_5} + 1$$

To give wide range of gain we picked $R_{V1} = 1 M\Omega$,
for enormous $1000x$ voltage boost we need to calculate $R_5$ value:

$$ R = \frac{R_{V1}}{k+1} = \frac{1 M\Omega}{1000+1} \approx 999 \Omega$$
$$ \boxed{R_5 = 1k\Omega} $$

Based on this selection we choose $C_4$ value:



## 4.x Active buffer

Buffer takes advantage of impedance characteristics of op amp. Using rule 1 we can derive:
$$ U_{-in} = U_{+in} = U_{out} $$
Voltage on input is the same that voltage on input.
Buffer seperates audio pipline.

</details>