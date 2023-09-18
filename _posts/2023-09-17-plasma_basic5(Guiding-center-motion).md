---
layout: single # post
title: "플라즈마 기초 공부 5"
date: 2023-09-17
categories: [plasma]
toc: true
toc_sticky: true

---

Guiding center motion of a charged particle.

# 배운 내용 정리 

자기장이나 전기장이 \(0\)인 특수한 상황이 아니라면, charged 입자의 변위벡터 \(x(t)\)와 속도벡터 \(v(t)\)는 아래와 같이 guiding center motion 성분과 cyclotron motion 성분을 모두 가질 것이다. 이번에는 guiding center motion에 대해 먼저 배운다.

\[\begin{equation}\begin{split} x(t) &= x_g(t) + r_c(t) \\\\ v(t) 
 & = v_g(t) + v_c(t)\end{split}\end{equation}\]

Guiding center motion에 관해 소개될 이론들은 다음과 같은 많은 조건을 가정한 결과물이다. 

> Assumptions
> - fast cyclotron motion
> - slow guiding $(=$ drift$)$ motion
> - 즉, 입자가 한바퀴 돌 동안 drift 방향으로 진행은 거의 안한다.
> - \(\frac{E}{B}\) has dimension of speed \(\ll c\) $(c$ is the speed of light$)$
> - weak spatial gradients for \(E,B\) → They are almost constant withn one cycle$(=$ cylotron orbit$)$


가정을 적용하면 먼저 다음과 같이 자기장과 전기장을 reduce시켜서 표현할 수 있다. 벡터 버전의 Taylor series 전개를 통해서 second order 이상의 derivative 항들은 아주 작기 때문에 없애버린 근사 과정이라고 할 수 있다.

\[\begin{split}B(x) &= B(x_g+r_c)\approx B_g + r_c \cdot \nabla B_g \\\\ E(x) &= E(x_g+r_c)\approx E_g + r_c \cdot \nabla E_g\end{split}\]

<aside>
💡 Note: $r_c \cdot \nabla B_g$에서 $r_c\cdot \nabla$라는 부분은 "gradient $($w.r.t. sptial direction$)$ along the direction of $r_c$"라고 해석할 수 있다.

</aside>

이제 charged particle의 motion에 관한 근본 방정식인 \(m\frac{dv}{dt} = qE + qv\times B\)에 위의 reduced \(E,B\)를 대입해 보자.

\[\begin{split}m\frac{dv}{dt} &= qE + qv\times B \\\\ m\frac{dv_g}{dt} + m\frac{dv_c}{dt} & = q(E_g+r_c\cdot \nabla E_g) + q(v_g+v_c) \times (B_g + r_c\cdot \nabla B_g)\\\\ m\frac{dv_g}{dt}+ m\frac{dv_c}{dt} & = q(E_g+r_c\cdot \nabla E_g) + qv_g\times(B_g+r_c\cdot \nabla B_g) + qv_c\times(r_c\cdot \nabla B_g)\end{split}\]

- line2 → line3 : \(v_g\times B_g= 0~(\because v_g \parallel B_g)\) 

이제 one cyclotron period에 대한 평균$(=$Integral along the trajectory$)$을 취해 보자. 

Average over one cyclotron period → \(m\frac{dv_c}{t},r_c\cdot \nabla B_g,r_c\cdot \nabla B_g\) disappear.

그 결과 다음과 같은 항들만 남게 된다. 

\[\begin{equation}m\frac{dv_g}{dt} = qE_g + q v_g \times B_g + \lt qv_c\times (r_c\cdot  \nabla B_g)\gt \end{equation}\]

마지막 항 $\lt qv_c\times (r_c\cdot  \nabla B_g) \gt $는 공간적인 불균일성 $($즉, 자기장이 공간에 따라 어떻게 변하는지$)$ 때문에 charged particle이 받는 추가적인 힘을 나타낸다. 앞 두 항은 기본적으로 로렌츠 힘에 의해서 자연스럽게 들어가는 항이라고 볼 수 있지만, 마지막 항은 *grad-B force* $(F_{\nabla B})$라고 따로 이름 붙인다. 

다음과 같은 cyclotron motion $($Local coordinatet 를 \(\hat{z} = \hat{B}\)라고 정의하면$)$의 expression을 이용해서 grad-B force를 계산해 볼 것이다.

\[\begin{equation}\begin{split}\vec{v}_c & = v_c(\hat{x}\cos\omega_c t - \hat{y} \sin \omega_c t)\\\\ \vec{r}_c & = \frac{v_c}{\omega_c}(\hat{x}\sin\omega_c t + \hat{y}\cos \omega_c t)\end{split}\end{equation}\]

이를 grad-B force 에 대입해 보면 아래와 같이 전개할 수 있다. 

\[\begin{split}\vec{F}_{\nabla B} &= q\lt v_c\times (\vec{r}_c\cdot \nabla B_g)\gt\\\\ &= \frac{qv_c^2}{2\omega_c}(\hat{x} \times \frac{\partial B}{\partial x}- \hat{y}\times \frac{\partial B}{\partial y})\\\\& = \frac{qv_c^2}{2\omega_c}(\hat{z}(\frac{\partial B_y}{\partial y}+\frac{\partial B_x}{\partial x}) - \hat{y}\frac{\partial B_z}{\partial y} - \hat{x}\frac{\partial B_z}{\partial x})\\\\&=-\frac{qv_c^2}{2\omega_c}(\hat{z}\frac{\partial B_z}{\partial z} + \hat{y}\frac{\partial B_z}{\partial y} + \hat{x}\frac{\partial B_z}{\partial x}) = -\frac{qv_c^2}{2\omega_c}\nabla B_z \\\\\ & \approx-\frac{qv_c^2}{2\omega_c}\nabla B = -\frac{mv_c^2}{2B}\nabla B\end{split}\]

- line 1 → line 2 : \[\vec{r}_c \cdot \nabla \vec{B}_f = \left(\frac{v_c}{\omega_c}\sin\omega_c t\frac{\partial}{\partial x}+\frac{v_c}{\omega_c}\cos\omega_ct\frac{\partial }{\partial y}\right)\vec{B}_g\]이며, \[\begin{split}\lt \sin \omega t \cos\omega_c t\gt = 0\\\\ \lt \cos\omega_c t \cos\omega_c t\gt = \frac{1}{2}\end{split}\]라는 사실을 이용하면 된다.
- line 2 → line 3 : 전개
- line 3 → line 4 : \(\nabla\cdot B = 0\) $($ by Maxwell equation$)$
- line 4 → line 5 : \(B\approx B_z\)를 가정하면 식이 어떻게 더 계산될 수 있는지 따진 것. 이때는 다음이 성립한다. \[\vec{v}_c \times\vec{r}_c\cdot (\vec{B}_g \hat{z}) = \vec{v}_c\times\left(\frac{v_c}{\omega_c}\sin\omega_c t\frac{\partial}{\partial x} B_g \hat{z} + \frac{v_c}{\omega_c}\cos\omega_ct\frac{\partial}{\partial y}B_g\hat{z}\right)\]

<aside>
💡 Note: 마지막 항 $-\frac{mv_c^2}{2B}\nabla B$의 dimension이 힘이 맞는지 확인해보자.
</aside>
\[\begin{aligned}mv_c^2 & \frac{\nabla B}{B} &~\\\\ (\text{energy}) & \frac{1}{(\text{length})} & = (\text{force})\end{aligned}\]


## Decomposition of guiding center motion
지금까지의 상황을 정리하면 guiding center motion에서 입자에게 작용하는 힘을 다음과 같이 나타내었다.

\[\begin{equation}m\frac{dv_g}{dt} = qE_g + q v_g\times B_g + f_{\nabla B}\end{equation}\]

\(v_g = v_{g\perp}+v_{\parallel}\hat{B}\)와 같이 자기장 방향에 수직인 성분과 평행인 성분으로 분해하고 \[\frac{d\hat{B}}{dt} = \frac{ds}{dt}\frac{\partial \hat{B}}{s} = v_{\parallel}\hat{B}\cdot \nabla \hat{B}\] 임을 기억하면 $(4)$는 다음과 같이 decomposed될 수 있다.

\[\begin{equation}\begin{split}\frac{v_g}{dt} & = \frac{dv_{g\perp}}{dt}+\frac{v_{\perp}}{dt}\hat{B}+v_{\parallel}\frac{d\hat{B}}{dt}\\\\ & = \frac{dv_{g\perp}}{dt}+\frac{dv_{\parallel}}{dt}\hat{B}+v_{\parallel}^2\hat{B}\cdot\nabla \hat{B}\end{split}\end{equation}\]

> The parallel part of the equation : 

\[\begin{equation}m\frac{dv_{\parallel}}{dt} = qE_{\parallel} + (F_{\nabla B})~\tiny{\parallel} \normalsize = qE_{\parallel}-\frac{qv_c^2}{2\omega_c}\nabla_{\parallel}B = qE_{\parallel} - \frac{qv_c^2}{2\omega_c}\frac{\partial B}{\partial s}\end{equation}\]


> The perpendicular part :

\[\begin{equation}\begin{split}m\frac{dv_{g\perp}}{dt} + mv_{\parallel}^2\hat{B}\cdot \nabla B & = qE_{\perp} + q v_{q\perp}\times B_g + (F_{\nabla B})~\tiny{\perp}\\\\ \normalsize\longrightarrow m\frac{dv_{g}}{dt} & = q v_{g\perp}\times B_g+F_{\perp}\end{split}\end{equation}\]



- $F_{\perp} = qE_{\perp} + (F_{\nabla B}) ~\tiny{\perp} \normalsize - mv_{\perp}^2 \hat{B}\cdot\nabla \hat{B} = qE_{\perp} - \frac{qv_c^2}{2\omega_c}\nabla_{\perp}B- mv_{\perp}^2 \kappa$
- \(\kappa = \hat{B}\cdot \nabla\hat{B}\) : the curvature vector of the field line \(B\)

### Perpendicular $(\perp)$ guiding center motion

\[m\frac{v_{g\perp}}{dt} = q v_{g\perp}\times B_g + F_{\perp},~ F_{\perp} \equiv qE_{\perp} - \frac{mv_c^2}{2B}\nabla_{\perp}B - mv_{\parallel}^2 \hat{B}\cdot \nabla \hat{B}\]

여기서 좌변을 \(0\)두고 푸는 first order solution을 구해 보면 다음과 같다.

\[ v_F \equiv v_{\perp (1)} = F_{\perp} \times \frac{B}{qB^2} \]

> Derivation :

\[\begin{split}(qv_{\perp}\times B + F & = )\times B \\\\ (v_{\perp}\times B)& = B(v_{\perp}\cdot B)- v_{\perp}(B\cdot B)\\\\ -qv_{\perp}B^2 + F\times B &= 0\\\\ v_{\perp} &= \frac{F\times B}{B^2}\end{split}\]

e.g. Drift due to time-constant electric field \(E\) is given by
\[\begin{split}v_E = qE_{\perp}\times \frac{B}{q|B|^2} = E\times \frac{B}{|B|^2} \\\\ v_E &= |v_E| = \frac{|E|}{|B|^2}\end{split}\]

**Other drifts**

1. curvature drift

    \[\kappa\equiv\hat{B}\cdot \nabla \hat{B}~(\text{curvature})\]

    Curvature는 단위 상으로 \(\frac{1}{(\text{length})}\) scale을 가지고 있다.
    Curvature 값은 cyclotron radius와 반비례한다.

    \[F_{\perp} \equiv q E_{\perp} - \frac{mv_c^2}{2B} - mv_{\parallel}^2\hat{B}\cdot \nabla\hat{B}\]
    의 마지막 항 \(-mv_{\parallel}^2\cdot \kappa \times \frac{B}{qB^2}\)을 curvature drift \(v_{\kappa}\)라고 약속한다. 

2. polarization drift
   
   Polarization drift는 2nd order solution to guiding center motion equation으로부터 나온다. 2nd order solution 을 \(v_{\perp} = v_F + v_p\)라고 하면,
   \[\begin{split}m\frac{d(v_F+v_p)}{dt} &\approx m\frac{dv_F}{dt} = q(v_F+v_p)\times B_g + F_{\perp} = qv_p\times B_g\\\\ v_p &\approx - \left(m\frac{dv_F}{dt}\right)\times \frac{B}{q|B|^2}\end{split}\]
   
   - \(v_p\)는 polarization drift라고 불린다.. 이 타입의 drift는 time-varying electric field를 활용한 실험에서 처음 발견되었다. 왜냐하면 전기장의 시간에 대한 변화가 separation of charge$($polarization$)$을 발생시켰기 때문이다.

### Parallel drift

식 $(6)$의 양변에 \(v_{\parallel}\)를 곱하면 다음을 얻는다.

\[\begin{equaation}m\frac{dv_{\parallel}}{dt}v_{\parallel} = \frac{d}{dt}\left(\frac{mv_{\parallel}^2}{2}\right) = qE_{\parallel}v_{\parallel}-\frac{qv_c^2}{2\omega_c} v_{\parallel}\frac{\partial B}{\partial s}\end{equation}\]

한편 우리의 근본방정식에 \(v\)과의 내적을 취하면

\[\begin{equation}\begin{split}m\frac{v}{dt}\cdot v& = (qE+qv\times B)\cdot v \\\\ \frac{d}{dt}\left(\frac{mv^2}{2}\right)& = qE\cdot v\\\\\frac{d}{dt}\left(\frac{mv_{\parallel}^2}{2}+\frac{mv_{\perp}^2}{2}\right) &= qv_{\parallel}E_{\parallel}+qv_{\perp} \cdot E_{\perp} \end{split}\end{equation}\]

두 식을 combine하면

\[\begin{equation}\frac{d}{dt}\left(\frac{mv_{\perp}}{2}\right)^2 = \frac{d}{dt}\left(\frac{mv_c^2}{2}\right) = qv_{\perp}\cdot E_{\perp} + \frac{qv_c^2}{2\omega_c}v_{\parallel}\frac{\partial B}{\partial s}\end{equation}\]

가 된다. \(E=0\)이며 axisymmetirc \(B\) field $(\hat{z})$인 간단한 상황에서의 parallel motion of equation은 다음과 같다.


\[\begin{equation}m\frac{dv_z}{dt} = -\frac{qv_c^2}{2\omega_c} \frac{\partial B}{\partial s} = -\frac{mv_c^2}{2B}\frac{\partial B}{\partial s}\end{equation}\]

**Magnetic moment**

# ChatGPT Q&A result

## 식 $(3)$이 성립하는 이유

변위 \(\vec{r}_c(t)\)가 속도 \(\vec{v}_c(t)\)의 시간 \(t\)에 대한 적분이라는 사실을 통해서 첫번째 줄에서 두 번째 줄로 유도하는 것은 할 수 있지만 $($적분상수 같은 것은 simplicity 를 위해서 0으로 설정한 것 같고$)$, \(\vec{v}_c = v_c(\hat{x}\cos\omega_c t - \hat{y}\sin \omega_c t)\)인 점이 잘 이해가 되지 않았었다. 

전기장은 없고 자기장도 상수로 주어진 경우에 비슷한 식을 유도했었는데, 

\[v_x = c_1\cos \omega_c t+ c_2\sin \omega_c t\]

\[v_y = c_3\cos \omega_c t+ c_4\sin \omega_c t\]

였었다. \(c1,c2,c3,c4\)가 만족해야 하는 조건은 \(v_x^2+v_y^2 = v_{\perp}^2\)였었다. 이를 만족하는 해를 하나 선택해 보면

\[v_x = v_{\perp}\cos \omega_c t\]

\[v_y = -v_{\perp}\sin \omega_c t\]

를 생각해 볼 수 있다. 하지만 여전히 의문인 점은, 속도에 관한 이 식들은 전기장이 없고 자기장이 constant 크기로 주어질 때 유도된 식이었는데, 그대로 사용해도 되냐는 점이다.

