# IA 5 Vision Artificielle

## Introduction

### Image informatique

简介：三通道等等……

介绍open cv库，例如python的应用。

```python
import cv2
cv2.VideoCapture(0)  # for example
```

### Formation des images

- Les images déforment la géométrie
- Les capteurs captures la lumière relétée par les objets et construisent l'image 2D

### Pinhole camera

### Lentilles

## Traitement des images

### Conversion en niveaux de gris 灰度转化

$$
Y = \frac{R + G + B}{3}
$$

或者换个比例：
$$
Y = 0.2 R + 0.7 G + 0.1 B
$$
$Y$ : clarité.

### Convolutions

$$
\begin{bmatrix}
-1 & 0 & 1 \\
-1 & 0 & 1 \\
-1 & 0 & 1
\end{bmatrix}
*
Y
$$

学过了。

例子：平均、高斯模糊、[梯度](###Gradiant et détection de bords)。

### Transformation de Fourier

用途：如卷积的态射（morphisme），方便计算。

### Gradiant et détection de bords

同上，学过了。

### Filtre de Canny

[wiki](https://en.wikipedia.org/wiki/Canny_edge_detector)

- suppression non-maximale
- ...

### Caractéristiques

Les caractéristiques sont des morceaux d'image facilement identifiable.

Considérons de nouveau nos nos images comme étant des fonctions. Observons les pixels dans une fenêtre.

#### Déplacement

$$
f(x + \Delta x, y + \Delta y) \approx f(x, y) + \frac{\partial f(x, y)}{\partial x} \Delta x + \frac{\partial f(x, y)}{\partial y} \Delta y
$$

#### Morceaux d'image

$$
E_W(\Delta x, \Delta y) \approx [\Delta x \ \Delta y] \cdots
$$

```python
cv2.goodFeaturesToTrack(...)
```

#### SIFT features

Scale Invariant feature Transform

相似但尺寸不同的物件。

#### Suivre les caractéristiques dans le temps

$$
f(x + \Delta x, y + \Delta y, t + \Delta t)
$$

#### Flot optique de Lucas-Kanade

$$
minimize_{u,v} \sum(\frac{\partial f(x, y, t)}{\partial})
$$

脱记，太快了……

[wiki](https://en.wikipedia.org/wiki/Lucas%E2%80%93Kanade_method)

### Détection de visages

- collection un grand nombre d'images
- mettons les à une petite échelle
- utilisation l'apprentissage pour apprendre un classeur

### Détection d'objets Viola-Jones

Seulement un ensemble de bonnes caacérisitiques et quelques trucs pour augmenter la vitesse

### Caractérisitiques de Haar

l'idée est de calculer la somme des pixels dans la zone blanche d'y soustraire la somme des pixels en zone noire

- bords
- lignes
- rectangles

### Classification rapide

L'extraction résulte en 180000+ caracéristiques de Haar pour chaque image. 5000 plus pertinentes. Avec une cascade de classeurs. 每次二分法去除。
