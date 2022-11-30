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

问题：

- 操作顺序对结果有影响

- gimnal lock

#### axes-angles

- axe de rotation $\vec n$
- angle de rotation $[-\pi, \pi]$

#### matrice de rotation

#### quaternions 四元数 

那个3B1B视频:

> [Visualizing quaternions (4d numbers) with stereographic projection - YouTube](https://www.youtube.com/watch?v=d4EgbgTm0Bg)

$[w \ \vec v] = [cos(\theta/2) \ sin(\theta/2)\hat n]$ 
$$
[w (x, y, z)] = [cos(\theta/2) (sin(\theta/2)\vec x \ \cdots)]
$$

##### multiplication de quaternion

##### unicité des quaterions

$\sqrt{w^2 + x^2 + y^2 + z^2} = 1$

- l'algorithme slerp permet d'obtenir une interpolation fluide entre deux angles
- concaténation et inversion rapide des déplacements angulaires
- conversion rapide à la forme matricielle et vice-versa
- seulement quatre valeurs à conserver
- représentation compact et pratique pour les jeux en réseaux

### vélocité et accélération angulaire

la vélocité angulaire
$$
\dot \theta = r \hat a
$$

$$
{\dot \theta}' = ...
$$

$$
p' = p + \dot pt
$$

$$
\theta' = \theta + \frac{\Delta t}{2}\omega\theta \\
\omega = \begin{bmatrix} 0 \\x\\y\\z \end{bmatrix}
$$

### Vélocité d'un point d'un objet

$$
\dot q = \dot \theta \times (q - p) + \dot p
$$

#### matrices

#### matrices en tant que transformation

#### produit de matrices de transformation

#### matrice 3D avec translation

$$
\begin{matrix}x \\ y \\ z\end{matrix} \to \begin{matrix}x \\ y \\ z \\ 1\end{matrix} 
$$

$$
\begin{bmatrix}M & \vec v \\ 0 & 1\end{bmatrix}
$$

##### matrix $3 \times 4$

平移放在第四列，然后位置向量尾巴上加个一。

#### matrix transposé

注意到对于旋转变换矩阵，其逆矩阵等于其转置。

#### conversion de quaternion en matrice

*用的时候再查，懒得抄了。*

#### transformation de direction

- la transformation d'un vecteur de direction ne deverait pas être affectée par les translations
- la solution consiste à ignorer le dernier élément

#### changement de base

非坐标系原点的物体的旋转

那个从来记不清顺序的$PBP^{-1}$

## Couple et moment d'intertie

### 牛二

$$
\ddot p = m^{-1}f
$$

pour les rotations,
$$
\tau = I \ddot \theta \implies \ddot \theta = I^{-1} \tau
$$

- $\tau$ le **couple**
- $I$ le **moment d'inertie**

### Couple (moment de force)

$$
\tau = p_f \times f
$$

$f$ est la force, $P_f$ le point où la force est appliquée et $\tau$ est le couple.

### Le moment d'inertie

$$
I_a = \sum {m_i}d^2_{p_i \to a}
$$

$d^2_{p_i \to a}$ est la distance entre le point et l'axe de rotation.

### Tenseur d'inertie

$$
I = \begin{bmatrix}
I_x & -I_{xy} & -I_{xz} \\
	& I_y & -I_{yz} \\
    &	& I_z
\end{bmatrix}
$$

有些计算好的样例。

### Inverse du tenseur d'inertie

$$
\ddot \theta = I^{-1} \tau
$$

### 世界-本地变换

同前文：本地坐标系和世界的变换。

### 可加性

$\tau$ 是可加的。

## Détection de collision

### Physique et détection de collsion

Le système de détection de collsision n'est pas utilse que pour la physique.

- le rendu graphique peut également utiliser les mêmes principes de détection pour savoir quoi rendre à l'écran ;
- le gameplay peut utiliser la détection de collsion mêmes si cela n'est pas directement reliée à la physique
  - détection un objet dans une zone
  - détecter si un objet est dans le champ de vision

### Problèmes de la détection de collisions

Chaque objet peut entrer en collision avec n'importe quel autre, $O(n^2)$

Chaque collision est géométriquement complexe.

### Propriété de la Board-Phase

- toutes les collisions de la simulation doivent être contenues dans la liste potentielles

- la liste doit être plus petite possible

### volume englobant

sphère, AABB alix-alignes bounding box, OBB oriented bounding box, 8-DOP discrete-oriented plotopes, convex Hull

从左到右逐渐精确，但是增加复杂度。

### méthodes pour réduire le nombre de test de collisions

### hiérarchie de volumes englobants (BVH)

arbre (binaire) dont les noeuds correspondent au volume englobant de ses enfants

将整体的碰撞块再细分。逐步检测。适用于静态物体。

#### construction d'un BVH

- top-down
- bottom-up
- insertion

### grilles

on utilise une grille contenant des cellules de taille uniforme

- facile à implémenter
- chaque cellule est accessible de manière constante, il est donc facile de placer les objets dans la grille
- difficile de choisir la taille de grille

#### grilles hiérarchiques (multi-resolution maps)

- utilise plusieurs grilles de cellules de taille différentes
- convient à des scènes qui ont des objets de tailles différents

#### quad-tree / oct-tree

### arbre BSP binary binary space partitioning

utilisation d'un plan

```c
struct {
	Vect position;
	Vect direction;
}
```

### critère de sélection des algorithmes

la taille de objets, la complexité des objets

la taille de la scène

la quantité d'objet dans la scènes

le type d'objet

## Génération de contacts

- broad phase
- narrow phase
- génération du collision

### Géométrie de collision

rendu (polugon meshs) 显示的模型

collisions (primitives) 碰撞块

volume englobant (BV) 包裹的区域

### 6 types de contacts en 3D

$$
x \in \{point, face, edge\} \\
(x_1, x_2) \coloneqq collision
$$

détection des contacts par priorité :

- point-face, edge-edge
- edge-face, face-face
- ...

### données de collisions

- pointe de contact
- normal de contact
- pénétration
- corps rigides concernées
- coefficient de restitution
- friction

(一些细节，如某种碰撞下法线的计算，参见课件)

### algo de collision simple

```cpp
void generateContacts(const Primitive &first, const Primitive &second, CollisionData* data);

class Primitive {
	public:
    RigidBody* body;
    Matrix4 offset;
};
```

### Sphère

```cpp
class Sphere: public Primitive {
    
};
```

### Plan

```cpp
class Plane: public Primitive {
public:
    Vector3 normal;
    real offset;
};
```

### Boîte

```cpp
class Box: public Primitive {
	public:
    Vector3 halfSize;
};
```

test every point of the 8 vertex of box.

### Boîte-Sphère

```cpp
dist = realEnter.x;
if (dist > box.halfSize.x) dist = box.halfSize.x;
if (dist < - box.halfSize.x) dist = -box.halfSize.x;
closestPt.x = dist;

// same for y, z
```

“最大化碰撞”

### collisions entre polyèdres convexes

- Separating Axis Tests
- Gilbert-Johnson-Keerthi
- Voronoi-Clip

#### GJK

Let $a_i$ every vertex of $A$, $b_i$ every vertex of B, then $\{a_i-b_j\}$ is a polygone, if which covers the origin point, then $A$ $B$ collide.

闵可夫斯基和

#### SAT

S'il existe un axe selon lequel deux objets sont séparés, alors les objets ne sont pas en contact ;

pour un polyèdre convexe, les axes à tester sont :

- la normal de tous les faces des deux objets
- l'angle d'angle droites à tous les paris d'arêtes des différents objets
- les axes similaires ou de direction ...
