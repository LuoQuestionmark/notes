# Mathématique et Physique pour le jeu vidéo

## Ajout de forces

### Contraint

例子：前后车轮由弹簧维系。

若无最小距离，则前后轮可以粘在一起。解决方法：加限制。

例子：简谐函数。

那个关于采样频率的定理：[采样定理 - 维基百科，自由的百科全书 (wikipedia.org)](https://zh.m.wikipedia.org/zh/采样定理)

例子：碰撞。

Force de collision 模拟碰撞。（说还是用impulsion）

## Gestion des contacts

### Résolution e collision simple

Deux objets : leur mouvement après collision peut être calculé en fonction du mouvement avant collision.

Comme une collision arrive dans un très petit lapse de temps, nous manipulerons directement la vitesse et la position des objets.

重叠：直接改位置。

### Normal au point de contact

Dans le cas d'un contact entre deux particules, la direction du contact peut être extraite de leur position.

Normale entre particules :
$$
\hat{n} = (p_a - p_b)
$$
Normal avec du sol :
$$
0 \\1\\ 0
$$

### Vélocité d'approche et d'éloignement

- vitesse d'approche
  $$
  v_c = p_a \cdot (p_b - p_a) + p_b \cdot (p_a - p_b)\\
  v_c = -(p_a - p_b) \cdot (p_a - p_b)
  $$
  
- vitesse d'éloignement 反过来

### Collision élastique

*弹性碰撞*

#### coefficient de restitution

$$
v'_s = - e v_s
$$

### Impulsion

$$
g = m \dot{p}
$$

$$
\dot{p'} = \dot{p} + \sum{g}
$$

单位（g）：$N \cdot s$，与动量单位相同。

### Impulsion due à la collision

$$
m \vec{v'} = m \vec{v} - k \vec{n}
$$

$$
k = \frac{(e+1) v_{rel} \cdot n}{((1/m_1) + (1/m_2))n^2}
$$

### Interpénétration

En fonction de l'algorithme de détection, la collision pet être détectée trop tard, quand deux objets se sont déjà interpénétrés.

Le changement de vélocité suite à une collision n'est souvent pas suffisant pour résoudre ce problème. surtout dans le cas de petite vitesse.

解决方法之一：靠质量加权移动（分离）物体。

#### Contact au repos

solutions :

- anticiper le contact pour empêcher l'interpénétration ;
- détecter si la vélocité est due à la gravité sur 1 frame.
  速度非零时先计算对地面的分量。

- appliquer la troisième loi de Newton
- simuler le contact à l'aide d'un ressort raide
- détecter la vibration

## Résolveur de contact

### Algo : résolveur de contact

- entrée : liste de contacts
- algo : 
  - application de l'impulsion
  - résolution des interpénétrations
  - gestion des contacts au repos
- sortie :
  - modification de la vitesse
  - modification de la position

### ordre de résolution

résoudre les contacts les plus importants d'abord. 

### pseudo contact entre particule

回到前文例子：模拟车轮靠一段刚体+一个加了绳子的弹簧。

绳子弹簧是一般“接触”的继承。

----

## Rotations et Orientation

### Rotations et Orientation

- la simulation de corps rigides implique d'aoir des objets qui peuvent tourner en plus de se déplacer
- tout comme c'est le cas pour la position, l'orientation d'un objet sera modifiée par le processus d'intégration

| 动量     | 角动量            |
| -------- | ----------------- |
| position | orientation       |
| vitesse  | vitesse angulaire |
| $\vdots$ | $\vdots$          |

#### cas 2D

- rotation en 2D

- orientation en 2D
  - 单位圆
  - $\theta = [cos \theta \ sin \theta]^T$

##### vitesse angulaire

e.g. $2\pi \frac{rad}{s}$

##### origine d'un objet

- la position d'un objet est représentée par la position de son origine

- on peut toujours déduire la position d'un morceau de l'objet par rapport à son origine
- l'origine peut être hors de l'objet

##### transformation d'un objet

transformation linéaire + translation = transformation affine

matrice de rotation $\Theta$ ... *反正会推导的*

$q = \Theta q_b + p$ *两行之前*

##### centre de masse

##### centre de masse comme origine

### orientation 3D

#### angles d'Euler

- lacet
- tangage
- roulis

问题：操作顺序对结果有影响

#### axes-angles

- axe de rotation $\vec n$
- angle de rotation $[-\pi, \pi]$

#### matrice de rotation

#### quaternions 那个3B1B视频

> [Visualizing quaternions (4d numbers) with stereographic projection - YouTube](https://www.youtube.com/watch?v=d4EgbgTm0Bg)

$[w \ \vec v] = [cos(\theta/2) \ sin(\theta/2)\hat n]$ 

##### multiplication de quaternion

##### unicité des quaterions

$\sqrt{w^2 + x^2 + y^2 + z^2} = 1$

- l'algorithme slerp permet d'obtenir une interpolation fluide entre deux angles
- concaténation et inversion rapide des déplacements angulaires
- conversion rapide à la forme matricielle et vice-versa
- seulement quatre valeurs à conserver
- représentation compact et pratique pour les jeux en réseaux

