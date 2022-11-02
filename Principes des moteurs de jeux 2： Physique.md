# Principes des moteurs de jeux 2： Physique

## Lois de Newton

- inertie
- dynamique de translation $\vec F = m \vec a$
- action/réaction

----

## Force

calcul discrète, approximation.

*其实最近做过*

```pseudocode
Simulate(dt, F) {
	a = F / m;    // acceleration, force, masse
	v += a * dt;
	p += v * dt;  // position
}
```

问题：依旧是力和时间非常数关系。将单位时间减半可以大幅增加精确性。

渲染频率和计算频率不一定相同。

### exemples

$$
F & = & \frac{Gm_1m_2}{r^2} \\
F & = & \frac{Kq_1q_2}{r^2} \\
F & = & (l - L) k_0 \\
& \vdots
$$

可以“创造”新的力。

新的力添加新的属性：电荷，静止长度……

#### analyse de $F = ma$

$$
\vec F = m \vec a
$$

- F : dynamique
- m : statique
- a : cinématique

#### sauter

跳跃全程：重力；

起跳：添加一个向上的速度；若选择添加力则需要一个极大的力；

垂直移动平台：受到向上向下的力……

垂直移动平台+碰撞（马里奥的箱子）：可能的平台倾覆。

## Collision (détection de collision)

Comparaison deux-à-deux donne une complexité de $O(n^2)$.

|      | AST  | JOU  | BAL  | HUD  |      |
| ---- | ---- | ---- | ---- | ---- | ---- |
| AST  | T    | T    | T    | F    | 1110 |
| JOU  | T    | F    | T    | F    | 1010 |
| BAL  | T    | T    | F    | F    | 1100 |
| HUD  | F    | F    | F    | F    | 0000 |

### pertinence

由左表产生右边的编码，之后以位比较判定是否可能碰撞。
$$
JOU \times JOU \\
0100 \ \& \ 1010 = 0000
$$

### subdivision spatiales

[四叉树](https://zh.wikipedia.org/wiki/%E5%9B%9B%E5%8F%89%E6%A0%91)（可能有跨区域的问题），复杂度$O(n \log{n})$。

### forme englobantes

*碰撞块*

#### 例子：球形碰撞块

$$
x^2 + y^2 \leq (r_1 + r_2)^2
$$

#### 例子：矩形碰撞块

假如物体无需旋转则可以选择。

### croisement de maillage

由一系列的封闭线段组成的碰撞块。

检查红色部分线段是否有碰撞。

<img src="/home/wluo/Documents/CS-ca/notes/note-img3.svg" alt="width=&quot;200px&quot;" style="zoom:50%;" />

### pixel pris

----

### 向量和物体碰撞检测

不同物体不同颜色，最后检测顶层的颜色。（利用GPU计算）

maillage de collision 不一定和实际物体一致：

- 更大
- 更小
- 填充物体上的洞

----

给碰撞块添加“触手[^1]”：e.g. 下方接触，上方不接触，物体旋转。

[^1]: 一定半径的圆/球。

----

穿模问题：

- 减少帧之间的时常
- 增大碰撞块的形状，关联上下帧（？）simulation continue
  上一帧、下一帧和两者间的连线

## Joindre

*汽车！*

### dégré de liberté

3D : 3 translation + 3 rotations

----

- rigide
- souple

----

- total
- partiel
- fixe

### joint

contraintes entre objets et un point d'attache

### cas où deux objets joints déplacent

supposons que $a$ et $b$ soit connecté par un joint :

- $a$ déplace ; joint est déplacé, $b$ déplace.

### cas où trois objets

顺序很复杂。

### masse ressort

一组由joint连接的物体。

