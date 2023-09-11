---
layout: single # post
title: "플라즈마 기초 공부 3"
date: 2023-09-10
categories: [plasma]
toc: true
toc_sticky: true

---


Quasi-neutrality, Application of Debye length

# 배운 내용 정리

## Quasi-neutrality

> Plasma tends to remain neutral for the length scale larger than the Debye length due to the Coulomb force. This property is called *quasi-neutrality*.
> 

> Consider an event where a fraction $(f)$ of the electrons in a small sphere \(V_s\) with radius \(r_s\), spontaneously move out of that volume. Assume that the ions and the remaining electrons are uniformly distributed in \(V_s\).
> 

> The radical electric field produced by the charges in \(V_s\) is given by 
\[E(r) = \frac{f\frac{4}{3}r^3\cdot n_e e}{4\pi \epsilon_0 r^2}=f\frac{n_ee}{3\epsilon_0}r\]
> 

> The corresponding total field energy in \(V_s\) is 
\[W_E = \int_0^{r_s} \frac{\epsilon_0E^2(r)}{2}4\pi r^2dr = f^2 \frac{2\pi}{45\epsilon_0} n_e^2 e^2 r_s^5\]
> 

> This field energy cannot exceed the sum of the initial thermal kinetic energies of the escaping electrons,
\[\begin{equation}W_E\le W_K = f\cdot \left(n_e \frac{4\pi}{3}r_s^3\right)\cdot \frac{3}{2} T_e = 2\pi f n_e T_e r_3^2.\end{equation}\]
> 

> Therefore, in order that such an event can be physically possible, the radius of \(V_s\) must be the following.
\[r_s^2\le \frac{45}{f}\frac{\epsilon_0T_e}{n_e e^2}= \frac{45}{f}\lambda_{D_e}^2~~\Rightarrow r_s <\frac{7}{\sqrt{f}} \lambda_{D_e} \equiv r_{\max}.\]
> 

# ChagGPT Q&A Result

## About the notion of Quasi-neutrality

Quasi-neutrality의 개념을 이해하기 위해서는 Debye 길이의 의미와 역할을 알아야 한다. 

Debye 길이는 *플라즈마 내에서 전하 불균형이 얼마나 빠르게 중성화될 수 있는지*를 나타내는 특성 거리이다. 

*특히 Debyle 길이에 의존하는 특정 거리 \(r_{max}\)보다 짧은 스케일에서는 전하 불균형이 있을 수 있지만, 이 거리보다 긴 스케일에서는 플라즈마가 중성화되기를 기대한다.* 

즉, Debye 길이는 전자와 이온이 서로 어떻게 상호작용하여 전체적인 중성 상태를 유지하는지를 결정하는 길이 스케일이다. 

이것이 위 내용 중에서 전자들이 어떤 sphere을 가끔씩 빠져나가는 상황을 관찰하는 이유이다. 

그렇게 발생된 non-neutral \(V_s\)에서 야기된 전기장이 다시 중성상태를 만들려고 하는데, 이 때 전기장에 의해 행해지는 일의 크기가 escaping electron들의 초기 운동 에너지보다 클 수 없음을 이용하여 \(r_{max}\)를 구할 수 있다.

## Radial electric field가 \(E(r) = \frac{f\frac{4}{3}r^3\cdot n_e e}{4\pi \epsilon_0 r^2}\) 인 이유

이 문제는 Gauss 법칙으로 설명할 수 있다. 

\[\oint \vec{E}\cdot \vec{dA} = \frac{Q_{inside}}{\epsilon_0}\]

- \(\vec{E}\)는 전기장 벡터
- \(\vec{dA}\)는 가상 표면의 작은 면적 요소 벡터
- \(Q_{inside}\)는 표면 내의 전체 전하량이다.

문제 상황: 가상의 sphere를 상정하여 \(r\) 반경에서의 전기장을 결정하려 한다. 

이 sphere 위에서의 전기장은 방사형으로 퍼져 나가고 있으므로 \(\vec{E}\)와 \(\vec{dA}\) 사이의 각도는 0도이다. 따라서 \(E\)를 전기장의 크기, \(dA\)가 면적 요소의 크기라고 하면 \(\vec{E}\cdot{dA}=EdA\)가 된다. 

따라서, 구 표면에서의 \(\oint \vec{E}\cdot \vec{dA}\)는 모든 지점에서의 \(EdA\)의 합이 되므로, \(E(r) \cdot 4\pi r^2 \)이 된다. 이 값이 \(\frac{Q_{inside}}{\epsilon_0}\)이므로 다음을 유도할 수 있다. 

\[E(r) = \frac{Q_{inside}}{\epsilon_0\cdot 4\pi r^2}\]

## 전기장으로 인해 발생하는 에너지의 양을 계산하는 방법

\[W_E = \int_0^{r_s} \frac{\epsilon_0E^2(r)}{2}4\pi r^2dr\]

이 식이 왜 성립하는지 알기 위해서는 에너지 밀도 \(u_E\) 계산을 통해 전기장에 인해 발생하는 총 에너지를 계산하는 방법을 알아야 한다. 

에너지 밀도는 다음과 같이 정의된다. 

\[u_E = \frac{\epsilon_0 E^2}{2}\]

- \(\epsilon_0\)는 진공의 유전율
- \(E\)는 전기장의 크기

이다. 

이제 구 형태의 볼륨 내에서 이 에너지 밀도를 적분하면 된다. 

\[\iiint u_E dV = \int_0^{r_s}\int_0^\pi\int_0^{2\pi}E(r)r^2\sin\theta dr d\theta d \phi\]

\(E(r)\)이 \(r\)에만 의존하므로 \(\theta\)와 \(\phi\)에 대한 적분은 각각 \(2\pi\)와 \(\pi\)로 단순화되어, \(r\)에 대한 단일 적분만 남게 된다. 마저 계산하면 다음과 같다. 

\[W_E = \int_0^{r_s} \frac{\epsilon_0 E^2(r)}{2}4\pi r^2dr\]

## 열 운동 에너지$($Thermal kinetic energy$)$를 전자기장에 의한 에너지가 초과할 수 없는 이유

우선 열 운동 에너지 $($Thermal kinetic energy$)$란, 플라즈마의 전자와 이온들의 무작위 운동에 기인한 에너지이다. 주로 플라즈마의 온도와 관련이 있다. 각 전자의 열 운동에너지는 단순한 점 입자에 대한 자유도 \(F=3\)을 이용하여 계산한 \(\frac{F}{2}k_BT = \frac{3}{2}k_BT_e\)라고 할 수 있다. $($선형 분자는 회전과 평행이동의 두 종류 운동까지도 할 수 있기 때문에 자유도는 \(5\)이고, 비선형 분자는 3개의 평행이동 방향과 3개의 회전축이 있기 때문에 자유도가 \(6\)이라고 한다.$)$

탈출하는 전자들의 에너지 원천 역시 열 운동 에너지라고 볼 수 있다.  따라서 전자들이 탈출하면서 남긴 전기장으로 인한 에너지는, 전자들이 원래 가지고 있던 에너지보다 클 수 없다는 것이다. 시스템 내에서 에너지는 소멸되거나 생성되지 않는다는 에너지 보존의 기본 원칙을 반영한 해석이라고 할 수 있다.

# Exercise

> Assume that each electron has the same probability \(p\) of escaping the spherical volume \(V_s\) $($radius \(r_s\)$)$, and initially there are \(10^5\) electrons and the same number of ions in the volume. What is the probability of the electron depletion with \(f=0.01\)?
> 

$($1$)$에서 $f\cdot \left(n_e \frac{4\pi}{3} r_s^3\right)$ 부분은 escaping 전자들이 나가고 나서 남아있는 전자들의 수이다. 따라서 전자들이 deplete $($고갈$)$될 확률은 다음과 같다. 

\[1-\frac{f\cdot \left(n_e \frac{4\pi}{3}r_s^3\right)}{10^5}\]

여기서 \(n_e = \frac{10^5}{\frac{4\pi}{3}r_s^3}\) 인데 그러면 답은 \(0.99\)인가?