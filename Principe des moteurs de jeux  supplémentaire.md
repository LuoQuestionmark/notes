# Principe des moteurs de jeux : supplémentaire

这一节是我没有学到的（在我到校以前的内容）

## La boucle du jeu

système à temps réel

mis à jour des entrées

mis à jour de la logique

mis à jour des sorties

## Découplage des étapes

> les données écrites à une étape devraient être inaccessibles, ou en lecture seule, aux étapes subséquentes

## échanges symboliques

从“输入”到“意愿”的转换

## Graphe de tâches

> Les liens du graphe représentent les dépendances entre les diverses tâches.

## Coordonnées

### oblique

斜二测画法？

oblique -> cartésien
$$
\begin{bmatrix}
1 & s \\
0 & 1
\end{bmatrix}
$$

### isométrique

cartésien -> iso
$$
\begin{bmatrix}
1 & 1\\
-\frac{1}{2} & 1
\end{bmatrix}
$$

## caméra

on cherche la position relative entre les objets et la caméra

## projections

### en perspective

焦点投影（？）

### orthographiques

plateforme, 2D, UI

水平投影

### exotiques

“异国情调”——特殊的投影，举例为塞尔达，人物在斜着在世界移动以达到最好的三渲二效果

## ECS

Entités-Composants-Systèmes

- une entité est un regroupement de composantes
- les composants sont des structures variées attachées à une entité. 

> Les systèmes sont variés, mais leur rôle est principalement d’aller chercher les composants qui les intéresse, sur les différentes entités, et y appliquer des actions.

orienté données

## shader

### vertex

> d’appliquer au sommet les transformations nécessaires au rendu

### geometry

改变输出几何的类型

### fragment

> décider de la couleur finale du fragment, ou de rejeter celui-ci