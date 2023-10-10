---
layout: single # post
title: "플라즈마 기초 공부 8"
date: 2023-10-06
categories: [plasma]
toc: true
toc_sticky: true

---

probability of collisions, electron collision rate coefficients, differential cross sections etc.

# Recall

- various collisions
- probability of collisions : experimental concept
  
probability of collision \(P_c\)에 대한 내용을 조금 복습해 보자. 

1cm, 1 Torr, 273K 의 조건에서 실험적으로 관찰한 collision 횟수에 관해서는 다음과 같은 식을 배웠다. 

\[\begin{equation}P_c(v_e) = \frac{d_0}{l_{mfp}} = d_0n_0\sigma(v_e) = d_0\frac{P_0}{T_0}\sigma(v_e)\end{equation}\]

- \(d_0\)는 specified path length이다.
- \(v_e\)는 전자의 속도이다.
- \(l_{mfp}:=\frac{1}{n_0\sigma}\)는 mean free path이다.
- \(\sigma\)는 cross-section이다.
- \(n_0= \frac{P_0}{T_0}\)는 이상기체방정식 때문에 성립한다. 즉, \(P_0=1\text{Torr}\)는 참조 압력, \(T_0=273\text{K}\)는 참조 온도이다.

사실 이 변환을 한 이유는, 우리가 실험적으로 측정할 수 있는 값들로 cross-section \(\sigma\)을 나타내기 위해서이다. 

\[\begin{equation}\sigma = \frac{T_0}{P_0}d_0^{-1}P_c\end{equation}\]

이 식에서 RHS에는 모두 실험적으로 측정할 수 있는 값들이 있다는 사실을 기억하면, 우리가 cross-section을 구하는 한 가지 방법을 알게 되었음을 알 수 있다. 

collision frequency \(\nu\) 역시 다음과 같이 실점적인 값들을 이용해서 구할 수 있게 된다. 

\[\nu = v_e n \sigma = v_e \left(\frac{P}{T}\frac{T_0}{P_0}\right)d_0^{-1}P_c\]

그러면 cross-section \(\sigma\)와 collision frequency \(\nu\)에 영향을 주는 전자의 속도 \(v_e\)는 어떻게 조절할까? 전자는 보통 전압 \(V\)를 걸어줌으로서 발사 시키기 때문에, electro-static energy \(eV\)가 운동에너지 \(\frac{1}{2}mv_e^2\)로 변환된다는 사실을 이용하면 다음과 같은 관계실을 얻을 수 있다. 

\[\begin{equation}v_e = \sqrt{\frac{2eV}{m_e}}\end{equation}\]

- \(e\)는 전자의 전하량이다.
- \(m_e\)는 전자의 질량이다.

이와 같이 Voltage \(V\)를 높이면 전자 속도를 제어할 수 있다. 

## 식 $(1)$에서 \(d_0\)는 무엇인가

앞서 probability of collision \(P_c\)이라는 개념은 실험적인 것임을 강조했다. 
\(d_0\)란 바로 현재 실험 상황에서 관찰하고 있는 path의 길이를 의미한다. 
예를 들어, 플라즈마 안에서 전자가 이동할 때 특정 거리 $($ex. 1mm$)$ 동안의 충돌 확률을 측정하는 상황이라면 1mm가 \(d_0\)가 된다. 

# Electron collision rate constants

\[\begin{aligned}e+A&\to e+A&(\text{elastic})\\\\ e+A &\to e+A^* &(\text{excitation})\\\\ e+A &\to 2e+A^+&(\text{ionization})\end{aligned}\]

이와 같은 collision 식은 마치 chemical reaction처럼 생겼다. 

실제로 각각의 collision의 rate coefficient $($반응 계수$)$ \(K\)는 다음과 같이 collision으로 인한 각 species들의 농도 변화율을 결정하는 데에 쓰인다. 
\[\frac{dn_{A^*}}{dt} = K_{ex}n_e n_A\]

Rate coefficient \(K_{ex}\)의 아래 첨자는 excitation collision의 반응 계수를 의미한다. $($여러 경우 중 exciation의 경우를 예로 들면$)$ 

\[\begin{equation}\begin{split}K_{ex} n_e &= \frac{1}{n_A}\frac{d n_{A^*}}{dt} = \nu_{eg,ex} \\\\ K_{ex} &= \frac{\nu_{ex}}{n_e}= \int_0^\infty \sigma_{ex}(v) v f_e(v)dv /n_e = \lt \sigma_{ex}(v) v \gt \end{split}\end{equation}\]

잠시 distribution function \(f_e(\eta)\)에 대한 이야기로 넘어가보자. 
전형적인 예시로 Maxwell Boltzman distribution이 모델링에 많이 쓰이며, 이 distribution을 결정하는 parameter는 half height의 높이에서의 full width 하나 뿐이다. 그러나 일반적으로는 아르곤처럼 funny shape을 가질 수도 있으며, 그럴 경우 Maxwell Boltzman distribution을 사용할 수 없고 그 모양을 잘 근사하는 특정 form의 함수를 사용한다. $($주로 exponential function들을 결합해서 쓴다. $)$

Rate coefficient를 위와 같이 쓰면 자연스럽게 \(v,\sigma_{ex}(v)\)를 결정하는 입자 간 상대속도\(v\)에 직접적인 영향을 주는 전자 온도 \(T_e\)가 rate coefficient를 결정하는 데에 중요하게 작용한다는 점을 유추할 수 있다. 이런 이유로 전자 온도 \(T_e\)와 rate coefficient \(K\)의 관계를 보는 경우가 많다. $($아래 그림 참고$)$

또한 식 $(3)$을 보면 electro-static energy 를 결정하는 \(V\)가 상대속도 \(v\)를 결정하고, 또 cross-section이 \(v\)에 의해 결정되므로, Energy \(V\)와 cross-section \(\sigma\)간의 관게를 보는 것 또한 자연스럽다. $($아래 그림 참고$)$ 

# Coulomb collision : collision between charged particles

Charged particle들의 collision 중에서도 elastric collision을 다룬다. 

## Differential scattering cross-section
- event \(\triangleq\) scattering into the solid angle \(d\Omega(\theta)\)
- collision between field particle and test particle that have same charge
  