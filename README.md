# Simple Overdrive Effect
---
## Derivasion of cutoff frequency
We consider loaded decouplig capacitor which makes lowpass filter (integrating circuit)

### Voltage devider equasion:
$$U_{out}=U_{in} \cdot \frac{Z_L}{Z_L+Z_R}$$
$$U_{out}=U_{in} \cdot \frac{\frac{Z_C Z_{Ro}}{Z_C+Z_{Ro}}}{\frac{Z_C Z_{Ro}}{Z_C+Z_{Ro}}+Z_R} = U_{in} \cdot \frac{Z_C Z_{Ro}}{Z_C Z_{Ro}+Z_C Z_{R}+Z_RZ_{Ro}}$$

### Laplace's s-domain impedance derividion
Definition of Laplace's transform:
$$F(s) = \mathcal{L}\{f(t)\} = \int_{0}^{\infty} f(t) e^{-st} \, dt$$

Impedance of resistance $Z_R$: 
$$U=I\cdot R$$
<!-- $$\mathcal{L}\{U\}=\mathcal{L}\{I\cdot R\}$$ -->
$$\mathcal{L}\{U\}=R\cdot \mathcal{L}\{I\}$$
$$Z_R(s)=\frac{U(s)}{I(s)}=R$$

Impedance of capacitance $Z_C$:
$$I=C\cdot \frac{dU}{dt}$$
$$\mathcal{L}\{I\}=C\cdot \mathcal{L}\{U'\}$$
$$I(s)=C\cdot sU(s)$$
$$Z_C(s)=\frac{U(s)}{I(s)}=\frac{1}{sC}$$

Back to voltage divider:
$$G(s)=\frac{U_y}{U_x}=\frac{\frac{R_o}{sC}} {\frac{R_o}{sC}+\frac{R}{sC}+RR_o}=\frac{R_o}{R_o+R+sCRR_o}$$
$$G(s)=\frac{(\frac{R_o}{R_o+R})}{1+s(\frac{CRR_o}{R_o+R})}$$
Then: $G(s)=\frac{K}{1+sT}, K=\frac{R_o}{R_o+R},T=\frac{CRR_o}{R_o+R}$

---

### Amplitude characteristic - Fourier analysis
Complex s-plain argument definition: $s = \sigma+j\omega$. To get amplitude characteristic we need to analyse holomorphic furier transform function. To achive that we need to get rid of real part of s-plane (constant component $e^\sigma$).

$$G(j\omega)=\frac{K}{1+j\omega T}\cdot\frac{1-j\omega T}{1-j\omega T}=\frac{K-j\omega KT}{1+\omega^2 T^2}$$
$$G(j\omega)=[\frac{K}{1+\omega^2 T^2}] + j[\frac{-\omega KT}{1+\omega^2 T^2}]$$

To derive amplitude-frequency function we must analyse mod of $G(j\omega)$
$$|G(j\omega)|=\sqrt{\frac{K^2}{(1+\omega^2 T^2)^2}+\frac{\omega^2 K^2 T^2}{(1+\omega^2 T^2)^2}}=\frac{K}{\sqrt{1+\omega^2 T^2}}$$

Finding -3dB frequency will be done based on power amplitude
$$A=20\cdot log(\frac{K}{\sqrt{1+\omega^2 T^2}})$$

Cutoff condition:
$$ A(\omega_{-3dB})=A(0)-3$$
$$ 20\cdot log(\frac{K}{\sqrt{1+\omega^2 T^2}})=20\cdot log(\frac{K}{\sqrt{1+0^2 T^2}})-3$$
$$ 10[log(\frac{K^2}{(1+\omega^2 T^2)})-log(K^2)]=-3$$
$$ log(\frac{1}{(1+\omega^2 T^2)})=-0,3$$
$$ \frac{1}{(1+4\pi^2f^2 T^2)}=10^{-0,3}$$
$$ 10^{-0,3}+10^{-0,3}4\pi^2f^2 T^2=1$$
$$ f=\sqrt{\frac{\frac{10^{-0,3}}{1-10^{-0,3}}}{4\pi^2T^2}} \approx \frac{1}{2\pi T}$$
Substitute T:
$$f=\frac{R_o+R}{2\pi CRR_o}=\frac{R}{2\pi CRR_o}+\frac{R_o}{2\pi CRR_o}$$

$$f=\frac{1}{2\pi RC}+\frac{1}{2\pi R_oC}$$