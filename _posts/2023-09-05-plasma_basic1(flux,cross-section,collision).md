---
layout: post
title: "플라즈마 기초 공부 1"
date: 2023-09-05
---

# 플라즈마 기초 공부

- flux, cross-section, collision frequency, mean-free path

# 배운 내용 정리

- ‘teneus’ plasma assumpation : 한번에 한 입자 field particle 가 다른 한 입자 test particle 과 충돌한다는 가정. many-body collosion은 다루지 않을 예정
- Flux (\(\Gamma\)) : the number of field particles (\(\Delta N\)) passing through unit area (\(\Delta A\)) per unit time (\(\Delta t\))
    
    \[\begin{equation}\Gamma\equiv \frac{\Delta N}{\Delta t\Delta A}= n_F v_0\end{equation}\]
    
    where \(n_F\) is the density of the field particles and \(v_0\) is the average “relative” velocity.
    
- “Collision” event : change of a certain physical state of the field (test) particle due to the interaction with the test particle.
→ We can quantify the cross-section only when the ‘event’ is exactly defined.
- Cross-section (\(\sigma\)): The total effective area of the test particle
- Collision frequency (\(\nu\))  = \(\frac{1}{\text{mean time between collisions}}\) = \(\frac{1}{\tau}\) = \(\text{(the rate of collisions)}\) = \(\text{(the number of field particles per unit)}\) time going through the cross section.
    
    \[
    \nu = \frac{1}{\tau} = \sigma \Gamma
    \]
    
    → This relation indicates that the cross-section $\sigma$ can be determined by ‘measuring’ the collision frequency $\nu$ while ‘controlling’ the flux $\Gamma$.
    
- Mean-free path (\(l_{mlp}\)) : the distance travelled by the field particle during $\tau$.

출처: 윤건수 교수님 플라즈마물리 수업 강의자료

# ChatGPT(4.0) Q&A Result

## $\Gamma = n_F v_0$ 가 성립하는 이유

> $n_F$는 입자 밀도이므로 “입자의 개수/ 단위체적”이다. $\Delta A$는 단위 면적이고, $\Delta t$는 단위 시간이다. $v_0$는 평균 상대 속도이다.

단위 면적 $\Delta A$를 통과하는 입자의 수 $\Delta N$을 구할 때 고려해야 할 것은 그 단위면적을 통과하는 “체적” $\Delta A \times v_0\times \Delta t$ 가 된다. 왜냐하면 $v_0\times \Delta t$는 $\Delta t$동안 이동한 거리이고, 이 거리에 단위면적 $\Delta A$를 곱하면 통과하는 체적이 되기 때문이다.

그래서 $\Delta N$은 다음과 같이 표현될 수 있다.
> 
> 
> \[
> \Delta N = n_F\times(\Delta A\times v_0 \times \Delta t) = n_F\times v_0 \times \Delta A \times \Delta t
> \]
> 
> 이를 $\Gamma$의 정의에 대입하면: 
> 
> \[
> \Gamma = \frac{\Delta N}{\Delta A\times \Delta t} = n_F \times v_0
> \]
> 
> 이렇게 $\Gamma = n_F\times v_0$가 된다. 이는 입자 밀도와 평균 상대 속도를 곱한 값으로, 단위 시간 단위 면적 당 통과하는 입자의 수를 나타낸다.
> 

## 충돌 빈도 $\nu$에 대하여 $\nu = \sigma \times \Gamma$인 이유

> 직관적으로 충돌 빈도 $\nu$는 cross-section $\sigma$가 클 수록, 단위 시간 단위 면적 당 충돌 입자 개수 $\Gamma$가 클수록 더 많아지므로 사실 정확히 등호는 아닐 수 있지만 근사치로서 이렇게 정의한다고 한다.
> 

## 각 물리량에 대한 단위 분석

> 1.  $n_F$ (입자 밀도) : 단위는 $m^{-3}$ 또는 $cm^{-3}$ 등으로, “입자의 개수 / 단위체적” 을 나타낸다.
2. $v_0$ (평균 상대 속도) : 단위는 $m/s$ 또는 $cm/s$ 등으로, 속도를 나타낸다.
3. $\Gamma$ (플럭스, 또는 선속) : $n_F\times v_0$이므로 단위는 $(m^{-3})\times(m/s) = m^{-2}s^{-1}$가 된다. “단위 시간, 단위 면적 당 통과하는 입자의 수”를 나타낸다.
4. $\sigma$ (충돌 단면적): 단위는 $m^2$ 또는 $cm^2$ 등으로, 면적을 나타낸다. 
5. $\nu$ (충돌 빈도 또는 충돌률) : 단위는 $s^{-1}$로, “단위 시간 당 출돌의 수”를 나타낸다.

이를 바탕으로 $\nu = \sigma \times \Gamma$식의 양변의 단위를 확인해 보자:
> 
> - 좌변: $\nu$ 이므로 $s^{-1}$
> - 우변: $\sigma \times \Gamma$  이므로 $(m^2)\times(m^{-2}s^{-1}) = s^{-1}$
> 
> 두 양변의 단위가 같으므로, 이 수식은 단위 측면에서도 물리적으로 일관된다고 할 수 있다. 
> 

# 귀여운 연습 문제

Consider a situation that you are walking on a busy street. The average number of people moving in one direction is five (5) per meter per second. You are annoyed only by strong body contacts and are not concerned with minor body contacts. Suppose that you experience such annoying body contacts (’events’) in the frequency of two (2) in every second. 

풀이 : flux $\Gamma$는 5이고 충돌 빈도 $\nu$는 2인 것으로 보아 $\sigma = \frac{\Gamma}{\nu} = 2.5$인 것 같다.

---