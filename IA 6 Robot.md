# IA 6 Robot

## Cinématique

La cinématique réfère généralement à l'étude de la géométrie du robot.

### robot planaire à deux liens

两个关节对应$\theta_1, \theta_2$，臂长$l_1, l_2$。

cinématique : comment présenter les mouvements.

-  cinématique directe : $\theta, l \mapsto x, y$

$$
x = l \cos \theta \\
y = l \sin \theta
$$

- cinématique inverse
  $$
  \theta = \pm \arctan (y / x) - \arcsin (l_2 \sin (\theta_2)/(x^2+y^2))
  $$
  

### Jacobien

$$
J =
\begin{bmatrix}
\frac {\partial x}{\partial \theta} & \cdots \\
\vdots & \ddots
\end{bmatrix}
$$

### Manipulateurs généraux

en 3D

La cinématique directe est facile à résoudre, l'inverse est plus compliquée.

## ...

### Obstacles

L'ensemble des espaces sans collision est l'espace libre.

(e.g. un sous-espace de $\Theta^2$ si on a $\theta_1, \theta_2$ comme var.)

### Planification par échantillonnage

#### probabilistic road maps (PRMs)

空间中取数个点，观察两两之间的连线，是否被障碍阻隔。

#### défis de PRMs

- comment savoir si un chemin cause une collision ?
- des goulots d’étranglement 瓶颈

### Rapidly-exploring random trees

在领域中选择点观察是否有碰撞，重复此过程。
