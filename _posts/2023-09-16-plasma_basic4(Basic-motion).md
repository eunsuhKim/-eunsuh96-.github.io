---
layout: single # post
title: "플라즈마 기초 공부 4"
date: 2023-09-16
categories: [plasma]
toc: true
toc_sticky: true

---

Basic motion of a charged particle.

어떤 Charged된 입자가 자기장 속을 통과할 때의 움직임이 어떻게 되는지 간단한 두 가지 경우에 대해서 배운다.

# 배운 내용

## Basic motion

\[\begin{equation}m\frac{dv}{dt} = qv\times V + F\end{equation}\]

입자에게 작용하는 힘의 성분을 자기장에 의한 힘인 \(qv\times B\)와 전기장에 의한 힘 \(F\)로 분해할 수 있다. 전기장과 자기장에 의한 힘을 합쳐서 로렌츠 힘 $($Lorentz force$)$라고 부른다.

1. 자기장 없이 \(F= qE(\text{electrostatic force)}\)인 경우를 살펴 보자.

Constant electric field \(E = E_0\) with zero magnetic field \(B = 0\) →

\[\begin{equation}m\frac{dv}{dt} = qE_0~\to~ \frac{dv}{dt}  = \frac{qE_0}{m}\end{equation}\]

로 간단해지므로 초기 위치 \(r_0\)일 때의 변위 \(r\)는 다음과 같다. $t$에 관해 두 번 적분하면 된다.$)$

\[r=r_0+v_0t+\frac{1}{2}\frac{qE_0}{m}t^2\]

$(2)$에 있는 것처럼 자기장에 의한 가속도는 \(\frac{qE_0}{m}\)와 같이 주어진다. 

2. 전기장 없이 Constant magnetic field 인 상황을 살펴보자.

\(B=B_0\hat{z},~~E=0\to\)

\[\begin{split}m\frac{dv_x}{dt} &= qv_yB_0\\\\ m\frac{dv_y}{dt} &= -qv_x B_0\\\\ m\frac{dv_z}{dt} &= 0\end{split}\]

라는 system of ODE가 나온다. 이 식을 풀기 위해 다음과 같이 정리해 보자. 

\[\begin{equation}m\begin{bmatrix}\frac{dv_x}{dt} \\\\ \frac{dv_y}{dt} \\\\ \frac{dv_z}{dt}\end{bmatrix} = \begin{bmatrix}0&qB_0&0 \\\\ -qB_0&0&0 \\\\ 0&0&0\end{bmatrix} \begin{bmatrix}v_x \\\\ v_y \\\\ v_z\end{bmatrix}\end{equation}\]

\(X=\begin{bmatrix}v_x,v_y,v_z\end{bmatrix}^T\)라고 두면 위 식은
\[\frac{dX}{dt}=MX,~M=\frac{qB_0}{m}\begin{bmatrix}0&1&0 \\\\ -1&0&0 \\\\ 0&0&0\end{bmatrix}\]이므로, 이 system of ODE의 해는 간단하게 
\[ X(t)=\exp(Mt)X_0 ,~X_0 = \begin{bmatrix}v_{x0},v_{y0},v_{z0}\end{bmatrix}^T\]이다. 

물론 여기에는 matrix exponential 이 포함되어 있기 때문에 Diagonalization을 하거나 하는 등의 방식으로 계산해야 한다. 약간 복잡해진다.

그래서 Alternative한 방식으로 다음과 같은 관찰을 통해 \(v_x,v_y,v_z\)를 간단하게 explicit하게 구해볼 것이다.

$(3)$을 보면 다음과 같이 \(v_x,v_y\)의 form과 \(v_z = v_{z0}\)라는 것을 알 수 있다. 

\[\begin{equation}\begin{split}m\frac{d^2v_x}{dt^2} &= qB_0 \frac{dv_y}{dt}\\\\& = \frac{qB_0}{m}\cdot qB_0 v_x\\\\\to  \frac{d^2v_x}{dt^2} &= -\left(\frac{qB_0}{m}\right)^2v_x =: -\omega_c^2v_x\end{split}\end{equation}\]

*\(\omega_c\)는 cyclotron 또는 gyration frequency라고 불린다.*

공교롭게도 우리에게 익숙한 1차원 2차 미분방정식이 되었기 때문에 \(v_x=v_{x0}e^{-\lambda t}\)라는 Ansatz을 시도해 보면, 복소수 값의 등장으로 다음과 같은 solution을 얻을 수 있다. 

\[v_x = v_{x0}(c_1\cos \omega_c t+ c_2\sin \omega_c t)\]

\(v_y\) 역시 같은 미분방정식을 만족하므로 다음과 같은 해를 가진다.

\[v_y = v_{y0}(c_3\cos \omega_c t+ c_4\sin \omega_c t)\]

\(v_{\perp}=\sqrt{v_x^2+v_y^2}\) 라고 약속하면, \(r_c:=\frac{v_{\perp 0}}{\omega_c}\)라는 Gyro-radious$(=$circular motion의 radius$)$ 를 정의할 수 있다.

Circular motion의 속도 \(v_{\perp}\)의 크기는 일정하게 유지된다. 왜냐하면 지금은 \(x,y\) 방향으로의 힘은 존재하지 않기 때문이다.

<aside>
💡 Note: 통상적으로 Circular motion을 묘사할 때, $\odot$는 board를 뚫고 나오는 방향으로, $\otimes$는 board로 들어가는 방향으로 약속한다. $($cf. 이온의 이동방향을 결정할 때에는 "Lion"을 기억하고 왼손으로 오른손법칙과 같은 행동을 해 보면 된다!$)$

</aside>

# ChatGPT Q&A result

## momentum의 변화율이 force인 이유

뉴턴의 두 번째 운동법칙에 따라 모멘텀의 변화율이 힘이라고 한다. 대부분의 물리학 문제에서는 질량이 일정하기 때문에 \(F = ma\) 형태를 사용하지만, 질량이 변하는 경우$($ ex. 로켓 추진 $)$에는 일반적인 아래의 식을 사용해야 한다.  

\[F= \frac{d(mv)}{dt}\]

## Electro”static” force라는 이름이 붙은 이유

static은 멈춰 있다는 뜻이다. 따라서 electrostatic force를 고려한다는 것은 우리가 멈춰있는 전하에 의해서 생기는 전기장과 그것이 만들어내는 힘을 다루고 있다는 것이다. 이와 상대되는 개념으로는 electrodynamics가 있다. electrodynamics에서는 electric charge가 움직이면서 전기장과 자기장을 모두 만들어 낸다.

## $(1)$의 우변 전체를 로렌츠 힘이라고 부르는 이유

로렌츠 힘$($Lorentz force$)$은 그 힘의 발견자인 헨드릭 안토온 로렌트 $($Hendrik Antoon Lorentz$)$의 이름을 따서 명명된 것이다. 로렌츠는 전하가 흐르는 전선에 작용하는 힘을 묘사하기 위해 다음과 같은 식의 힘을 제안했다.

\[F = q(E+v\times B)s\]

- \(F\):로렌츠 힘
- \(q\): 전하량
- \(v\): 전하의 속도
- \(E\): 전기장
- \(B\): 자기장

## 2. 전기장 없이 Constant magnetic field 인 상황에서 첫번째 미분방정식을 유도하는 방법, 그리고 마지막 회전 반경이 성립하는 이유

로렌츠 힘 \(\vec{F} = q\vec{v}\times\vec{B}\) 를 고려할 때, 입자가 순전히 자기장 속에서만 움직인다면 전기장이 \(0\) 이므로 로렌츠 힘은 자기장에 의한 힘만을 고려하면 된다.

자기장은 \(z\) 방향으로 주어져 있으므로 \(\vec{B}=B_0 \hat{z}\) 이다. 
입자의 \(z\)방향 속도는 자기장과 평행하므로 영향을 받지 않는다. (초기속도 그대로이다.) 그러므로 입자의 \(xy\) 평면 상에서의 속도에 대해서만 살펴 보자. 이를 \(\vec{v}=v_x\hat{x}+v_y\hat{y}\)라고 하면, 로렌츠 힘은 다음과 같다. 

벡터 외적의 정의를 사용하면:

\[\vec{F} = qB_0 (-v_y \hat{x}+ v_x\hat{y})\]

이다. 
따라서 로렌츠 힘의 크기는 \(\norm{\vec{F}} = F = qv_{\perp}B_0\) $(v_{\perp}$는 평면 상의 속도이다.$)$가 되며, 이 힘은 항상 입자의 움직임에 수직이다. 

자기장 내에서 입자가 수평 평면에서 원형 궤도로 움직이는 경우, 중심력은 로렌츠 힘에 의해 제공된다고 할 수 있다. 중심력은 \(F_c = \frac{mv_{\perp}}{r_c}\)로 주어진다. $(r_c$는 회전 반경이다.$)$

두 힘이 같다는 식을 세우면:

\[\frac{mv_{\perp}^2}{r_c} = q v_{\perp}B_0\]

이를 정리하면:

\[r_c = \frac{mv_{\perp}}{qB_0}\]

\(\omega_c=\frac{qB_0}{m}\)임을 사용하면 \(r_c = \frac{v_{\perp}}{\omega_c}\)이다. 

이 \(r_c\) 값은 gyro-radius 또는 Larmor radius라고도 불린다. 

