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

\[\begin{split}\vec{v}_c & = v_c(\hat{x}\cos\omega_c t - \hat{y} \sin \omega_c t)\\\\ r_c & = \frac{v_c}{\omega_c}(\hat{x}\sin\omega_c t + \hat{y}\cos \omega_c t)\end{split}\]

이를 grad-B force 에 대입해 보면 아래와 같이 전개할 수 있다. 

\[\begin{split}\vec{F}_{\nabla B} &= q\lt v_c\times (r_c\cdot \nabla B_g)\gt\\\\ &= \frac{qv_c^2}{2\omega_c}(\hat{x} \times \frac{\partial B}{\partial x}- \hat{y}\times \frac{\partial B}{\partial y})\\\\& = \frac{qv_c^2}{2\omega_c}(\hat{z}(\frac{\partial B_y}{\partial y}+\frac{\partial B_x}{\partial x}) - \hat{y}\frac{\partial B_z}{\partial y} - \hat{x}\frac{\partial B_z}{\partial x})\\\\&=-\frac{qv_c^2}{2\omega_c}(\hat{z}\frac{\partial B_z}{\partial z} + \hat{y}\frac{\partial B_z}{\partial y} + \hat{x}\frac{\partial B_z}{\partial x}) = -\frac{qv_c^2}{2\omega_c}\nabla B_z \\\\\ & \approx-\frac{qv_c^2}{2\omega_c}\nabla B = -\frac{mv_c^2}{2B}\nabla B\end{split}\]