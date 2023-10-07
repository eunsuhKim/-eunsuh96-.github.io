---
layout: single # post
title: "플라즈마 기초 공부 7"
date: 2023-10-02
categories: [plasma]
toc: true
toc_sticky: true

---

Elementary collision processes

# 배운 내용 정리 
## Overview

Plasma collision은 크게 다음과 같이 분류할 수 있다. 

- Electron collisions
- Neutral collisions
- Ion collisions
- Photon collosions

![](../images/power_absorption_schematic.png)

이 그림이 보여주는 것은 플라즈마 Chamber 내에서 일어나는 현상들과 그에 따른 에너지의 flow$($or transport$)$이다.

먼저 전자들에게 power$($보통 power density -- $kW/m^3)$가 주입되면 에너지가 높아진 전자들이 벽에 충돌하기도 하고, subtrate $($반도체 웨이퍼$)$ 과 충돌하여 반응 물질들을 만들어내기도 하며, 플라즈마 공간 안에 채워져 있는 gas 와 충돌하기도 한다. gas는 전자들의 에너지를 받아 excited state $($들뜬 상태 $)$가 되거나, ion이 되거나, 혹은 radical, molecular fragments가 되기도 한다. 특히나 무거운 이온이 반도체 웨이퍼와 충돌하면 거기에 살고 있던 자유 전자들이 다량 방출되는데, 이 현상에 의해 공급된 전자들을 secondary electron이라고 부른다. 

![](../images/elementary_collisions.png)

위 다섯가지 반응이 대표적이라고 할 수 있다. 

$(a)$ 전자가 원자에게 충돌하여 양이온과 두 개의 전자로 나뉘어지는 과정이다. 

$(b)$ 전자가 원자에게 충돌했을 때, 그 에너지가 전자를 탈출시키기에는 부족해서, 들뜬 상태의 원자와 운동에너지를 약간 잃은 전자가 되는 과정이다.

$(c)$ 원자가 원자에게 충동했을 때, 원자 하나와 양이온 하나, 그리고 자유 전자가 되는 과정이다. 

$(d)$ 전자가 들뜬 상태의 원자에게 충돌했을 때, 원자가 원래 상태가 되고 전자는 운동에너지를 얻어 빠른 전자가 되는 과정이다.

$(e)$ Penning ionization이라는 이름까지 붙을 정도로 중요한 과정이다. 두 개의 들뜬 상태의 원자가 충돌했을 때, 한 원자는 원래의 바닥 상태가 되고 빠른 전자와 빠른 양이온이 만들어지는 과정이다. heating 과정에 많이 쓰인다고 한다. 

## Electron collisions

여러 electron collision 상황을 묘사하는 식을 배웠는데, 그 중에서 위의 카테고리에 들어가지 않는다고 느꼈던 두 가지만 다루려고 한다. 

**Radiative attachment**
\[e+A \to A^-+h\nu\]

전자를 좋아하는 원자 \(A\)라면 전자를 붙여서 음이온 \(A^-\)이 되고, 대신에 자유 전자가 가지고 있던 위치 에너지때문에 빛 \(h\nu\)이 방출되는 현상이다.

**Recombination**
\[e+A^+ + M \to A^* + M\]

여기서 \(M\)은 three body로, 반응 전 후 변화는 없지만, 이 \(M\) 없이는 반응이 일어나지 않는다는 것이 특징이다. 그냥 생각해 보았을 때, 자유 전자와 양이온이 결합하여 들뜬 상태의 원자가 될 수 있지 않을까 싶지만, 에너지와 모멘텀의 보존 법칙 때문에 그러한 상황은 제 3의 존재 없이는 일어날 수 없다고 한다. 여기서 \(M\)은 다른 원자나 이온일 수도 있고 벽$($Wall$)$일 수도 있다. 

구체적으로 자유 전자와 양이온이 결합하여 들뜬 상태의 원자가 되는 것이 왜 불가능한지 알아보자. 먼저 이러한 반응이 일어났다고 했을 때 에너지와 모멘텀의 전, 후를 등식으로 써 보면 다음과 같다. 

\[\begin{equation}\begin{aligned}mv&=(m+M)v^\prime&\text{(momentum)}\\\\ \frac{1}{2} mv^2 &= \frac{1}{2}(m+M) {v^\prime}^2+\varepsilon_{excited}&\text{(energy)} \end{aligned}\end{equation}\]

- \(v\)는 자유전자의 속도이고, \(v^\prime\) 은 반응 후 들뜬 상태의 원자의 속도이다. 
- \(m\)은 전자의 질량, \(M\)은 양이온의 질량이다.
- \(\varepsilon_{excited}\)은 들뜬 상태의 bound electron이 가지는 에너지이다.

\(M^\prime:=m+M\)이라고 약속하면 에너지 식을 모멘텀 식을 활용하여 다음과 같이 전개할 수 있다. 

\[\begin{equation}\begin{aligned}&=\frac{1}{2}\frac{(M^\prime v^\prime)^2}{M^\prime} +\varepsilon_{excited}\\\\ & = \frac{1}{2}\frac{(mv)^2}{M^\prime}+\varepsilon_{excited}\\\\& = \frac{1}{2}mv^2\cdot \frac{m}{M^\prime}+\varepsilon_{excited}\end{aligned}\end{equation}\]

마지막 줄을 정리하면 다음과 같다.\[\begin{equation}\frac{1}{2}mv^2\cdot (1-\frac{m}{M^\prime}) = \varepsilon_{excited}\end{equation}\] 

여기서 \(m\)과 \(M^\prime\)의 값은 정해져 있고, 좌변의 값은 자유 전자가 가지고 있던 속도 \(v\)에 따라서 continuous한 값을 가질 수 있다. 반면 우변은 bound electron의 excited state이기 때문에 discrete한 값만을 가질 수 있다. 따라서 임의의 속도 \(v\)에 대해 이런 등식이 성립할 수 없으므로 자유전자와 이온이 둘만 합쳐지는 것은 불가능하다. 대신 third body인 \(M\)도 함께 충돌해야지만 이런 현상이 설명 가능하게 된다.


---