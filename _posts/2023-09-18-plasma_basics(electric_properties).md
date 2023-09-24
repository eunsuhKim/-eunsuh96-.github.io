---
layout: single # post
title: "플라즈마 기초 공부 7"
date: 2023-09-18
categories: [plasma]
toc: true
toc_sticky: true

---


Electrostatic (ES) and Electromagnetic (EM) properties of unmagnetized plasma

# Contents

이전까지는 단일 입자의 전자기장 내에서의 behavior를 보기 위해 Equation of motion (EoM)을 배웠다면, 지금부터는 collective behavior인 electrical property에 대해 알아보기 위해 fluid equation과 Maxwell’s equation을 배운다. 

## Unmagnetic cold plasma → Density oscillation

$B_0= 0, T_0 \approx 0  ~(\text{or } p_0=0 )$ — temperature 나 pressure가 0이라는 것은 값 자체가 없다는 뜻이 아니고, 그만큼 다른 항들에 비해 작기 때문에 무시할 수 있다는 의미이다.

\[
\begin{aligned}n_sm_s\frac{du_s}{dt} &= -n_sq_s\nabla\phi~~&(\text{momentum equation})\\\\ \frac{\partial n_s}{\partial t} &= -\nabla \cdot(n_su_s)~&(\text{continuity equation=density equation})\end{aligned}
\]

- $n_s$: number density
- $m_s$: mass of one particle
- $u_s$: velocity of chunk of particles
- $\frac{d(sth)}{dt} = (\text{total derivative}) = \frac{\partial }{\partial t} + (sth)\cdot \nabla(sth)$
- $q_s$: charge of one particle
- $\phi$ : electric potential
- 원래는 momentum equation에 자기장에 의한 항과 마찰에 의한 항이 모두 포함되어 있었는데, 우선 simplicity를 위하여 무시하였다.
- Continuity equation의 $n_su_s$는 the number of particles per unit area and unit time, 즉 flux를 의미한다. flux의 단위는 $\frac{1}{l^3}\frac{l}{s} = \frac{1}{l^2s}$이다.
- Continuity equation의 우변에 있는 $\nabla\cdot$ 기호는 그 vector field의 divergence에 의한 항이다. divergence, 즉 빠져나가는 양이 많을수록 number density $n_s$는 작아지므로 $-$기호가 붙었다.

두 식을 합치면 아래 식을 얻는다. (continuity equation을 시간에 대해 미분해서 momentum equation을 대입하면 된다. 

\[
\frac{\partial ^2 n_{1s}}{\partial t^2} = - \nabla\cdot\left(\frac{n_{0s}q_s}{m_s}\nabla \phi_1\right) = \frac{n_{0s}q_s}{m_s} \nabla^2\phi_1
\]

양변에 $q_s$를 곱하고 모든 particle들에 대하여 합하며, Poisson relation \(\nabla\cdot E = \frac{\rho_q}{E_0}\to -\nabla^2\phi = \sum_s \frac{q_sn_{s1}}{\epsilon_0}\)을 적용하면 아래와 같다. 

\[
\begin{aligned}\frac{\partial ^2}{\partial t^2} \sum_{s} q_sn_{1s} &= \left(\sum_{s}\frac{n_{0s}q_s^2}{m_s}\right)\nabla^2 \phi-1 \\\\ \frac{\partial^2}{\partial t^2}(-\epsilon_0\nabla^2\phi_1) &= \left(\sum_{s}\frac{n_{0s}q_s^2}{m_s}\right)\nabla^2 \phi-1\\\\\frac{\partial ^2}{\partial t^2}\rho_1 &= \left(\sum_{s}\omega_{ps}^2\right)\rho_1\\\\\frac{\partial ^2\rho_0}{\partial t^2} =& = -\omega_p^2\rho_1\end{aligned}
\]

- $\rho_1= \sum q_sn_{1s}$ : the charge density
- $\omega_{ps} = \left(\frac{n_{0s}q_s^2}{\epsilon_0m_s}\right)^{1/2}$: the plasma frequency of speies $s$
- electrostatic perturbation 에 의한 charge density의 oscillation frequency는 $\omega_p \equiv (\sum_s \omega_{ps}^2)^{1/2}$이다.

# Ex. 1

> Explain why $\omega_p \equiv (\sum_s \omega_{ps}^2)^{1/2}\approx \omega_{pe}$ for typical plasma comprised of electrons and ions. Here $\omega_{pe}$ is the electron plasma frequency.
> 

sol. The electron plasma frequency \(\omega_{pe}\) is given by 
\[\omega_{pe} = \sqrt{\frac{n_e e^2}{\epsilon_0 m_e}}\]
where \(n_e\) is the density of electron, \(e\) is the charge of an electron, \(\epsilon_0\) is the vacuum permitivity, and \(m_e\) is the mass of an electron.

Similarly, the ion plasma frequency \(\omega_{pi}\) is
\[\omega_{pi}^2 = \frac{n_iZ^2e^2}{\epsilon_0M_i}\]
where \(n_i\) is the ion density, \(Z\) is the ion charge state, \(m_e\) is the ion mass.

Because ions are much more massive than electrons $(M_i\gg m_e)$, 
their contribution to the plasma frequency tends to be much smaller than that of electrons. So for a typical plasma, we can use the following approximation:

\[\omega_p = \sqrt{\omega_{pe}^2 + \omega_{pi}^2}\approx \omega_{pe}^2.\]

# Ex. 2

> What is the electron plasma frequency for the plasma with $n_e = 1\times 10^{13}cm^{-3}$.
> 

sol. Using the NRL formulary for the electron plasma frequency, 

\[
f_{pe} = \frac{\omega_{pe}}{2\pi}\approx 8.98\times 10^3\sqrt{n_e}= 8.98\times 10^3\times (10^{13})^{1/2} = 8.98\times 10^{9.5}
\]

So $\omega_{pe}\approxeq 8.98\times10^{9.5}\times 2\pi \approx 1.78\times 10^{11}$

---

> **First order approximation (= Linearization)**
> 

많이 사용되는 테크닉 중에 각 quantity들을 small variable $\epsilon$ 등에 대한 다항식으로 근사하여 first order term만 남기는 방법이 있다. 

\[
\begin{aligned}u= u_0 +u_1\\\\ \phi = \phi_0 + \phi_1\\\\n = n_0 + n_1\end{aligned}
\]

이와 같은 방식으로 Equilibrium이 존재한다면, $($혹은 가능하다면$)$ equilibrium에서는 0차, 그리고 1차항까지 사용하는 방식이다. 이런 근사 식을 적용하면 예를 들면 아래와 같은 reducing 과정으로 linearizaiton이 가능하다. 

\[
(u_0+u_1) \cdot \nabla(u_0+u_1) = u_1\cdot \nabla u_1 \approx 0
\]

---

## Recall: Maxwell equations

\[
\nabla\cdot B = 0~(\text{no magnetic charge})\\\\ \nabla\cdot E = -\frac{\rho_q}{\epsilon_0} ~(\text{Poisson's equation = Gauss' law})\\\\ \nabla\times E = - \frac{\partial B}{\partial t}~(\text{Faraday's law})\\\\ \nabla\times B = \mu_0 J + \frac{1}{c^2} \frac{\partial E}{\partial t}~~(\text{Ampere-Maxwell equation})
\]

## Electro Magnetic (EM) properties → Oscillation of electric current

~~Cole plasma, low pressure~~으로, 이제 finite value of temperature, pressure인 상황을 살펴 보자. 

여전히 unmagnetic assumpation $B_0 = 0$과, static plasma에서는 $u_0 = 0,E_0= 0$ 임은 가정하자. 

\[
n_{0s}m_s\frac{\partial u_{1s}}{\partial t} = n_{0s} q_s E_1 - \nabla p_{1s} - \nu_s n_{0s} m_s u_{1s}
\]

양변에 charge $q_s$를 곱하고 모든 particle에 대해 합하면, current density $J:= \sum_s n_sq_su_s$라는 quantity가 등장하게 된다. 

\[
\frac{\partial J_1}{\partial t} = \omega_p^2\epsilon_0 E_1 - \sum_s \frac{q_s}{m_s} \nabla p_{1s} - \sum_{s} \nu_s q_s n_{0s} u_{1s}
\]

Effective collision frequency $\nu_*$라는 개념을 도입 $(\nu_*J_1 \equiv\sum_s\nu_s J_s)$하면 다음과 같이 식이 간단해 진다. 

\[
\frac{\partial J_1}{\partial t} = \omega_p^2\epsilon_0 E_1 - \sum_s \frac{q_s}{m_s}\nabla p_{1s} - \nu_* J_1
\]

양변에 $\nabla\times$  (curl)을 취하면 Faraday’s law에 의해

\[
\begin{equation}\frac{\partial }{\partial t}\nabla\times J_1 = \omega_p ^2 \epsilon_0 \nabla \times E_1 - \nu_* \nabla\times J_1 = - \omega_p^2 \epsilon \frac{\partial B_1}{\partial t} - \nu_* \nabla \times J_1\end{equation}
\]

- 가운데 항은 $\nabla\times\nabla f = 0,\forall f$ (Curl of any gradient is zero) 이므로 없어졌다.

---

> **Sinusoidal perturbation for first order electric field $E_1$**
> 

$E_1\sim \exp(ik\cdot x- i\omega t)$ $($여기서 $k$가 벡터인 이유는 공간 dimension이 $n$개일 때 일반적으로 각 dimesion에 corresponding하는 계수가 붙을 수 있기 때문인 것 같다.$)$으로 가정했을 때, 시공간에 대한 미분 항들이 굉장히 간단하게 아래와 같이 나타난다. 

\[
\begin{aligned}\frac{\partial E_1}{\partial t}= -i\omega E_1\\\\ \nabla\cdot E_1 = ik\cdot E_1\end{aligned}
\]

이러한 sinusoidal perturbation을 항상 가정할 수 있는 것은 아니며, 그렇지 않은 경우에 대한 연구 역시 좋은 research topic이다. 이 테크닉을 Fourier Transform을 활용한다고 하기도 한다.

---

이제 식 (1)에 Maxwell- Ampere’s law를 적용할 차례이다. 즉, first order 자기장 $B_1$과 first order current density $J_1$간의 다음과 같은 관계식을 적용해 볼 것이다. 

\[
\nabla\times B_1 = \mu_0\epsilon_0\frac{\partial E_1}{\partial t}+ \mu_0 J_1
\]

 양변에 $\nabla\times$를 취하고 Sinusoidal perturbation for $E_1$를 가정하여 정리하면 아래와 같이 $B_1$항들을 없애버릴 수 있다. $($단, $\mu_0\epsilon_0 = \frac{1}{c^2}$이고 $k = \frac{2\pi}{\lambda}$ $($?$)$$)$

\[\begin{aligned} -\nabla^2 B_1 &= -\frac{1}{c^2} \frac{\partial^2  B_1}{\partial t} - \frac{\omega}{\omega + i \nu_* }\frac{\omega_p^2}{c^2} B_1 \\\\ c^2k^2 &= \omega^2- \frac{\omega}{\omega i \nu_* } \omega_p^2\end{aligned}\]

결과적으로 얻어진 위 식을 보면, wave number $k$과 wave frequency $\omega$에 관한 implicit relation이라고 할 수 있다. 이 관계식을 *dispersion relation* 이라고 부른다. 왜냐하면