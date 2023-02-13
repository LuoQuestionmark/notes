# Apprentissage Profond 3

## Introduction

il s'agit d'un ensemble d'algorithmes développés pour l'entraînement de réseau  de neurones artificiels à plusieurs couches.

1986, backpropagation.

### retour sur les NN simples

A chaque epoch, on mettait à jour les poids :
$$
w = w + \Delta w \\
\Delta w = - \eta \ \nabla J(w)
$$
Le `grad` était calculé sur l'ensemble de données

La fonction objectif à optimiser était la *Sum of Squared Errors* (SSE), ou encore *Log-Likelihood*(NLLL).

### multiples couches

si plus d'un niveau caché, alors besoin des techniques du deep learning.

### multi-classe

将特征表示为一个向量；每个可能的选项占一位。如对于一个三个类的数据，分类为
$$
\vec {v1} = [1 \ 0 \ 0]\\
\vec {v2} = [0 \ 1 \ 0]\\
\vec {v3} = [0 \ 0 \ 1]
$$

### perceptron multicouche

一些关于写法的小提示，没什么特别的。

matrice $W^{(l)} \in \mathbb{R}^{j \times [k+1]}$ pour représenter les poids de la couche $l$

## Propagation avant

l'entrée :
$$
z_1^{(2)} = \sum_i^m a_i^{(1)} w_{1,i}^{(1)}
$$
$z_1^{(2)}$ est l'entrée nette et $\phi$ la fonction. on va utiliser `sigmoids`.

**注意：**单向传播，无循环。

拓展到向量（一次计算所有特征）
$$
z^{(2)} = W^{(1)}a^{(1)}
\\
a^{(2)} = \phi(z^{(2)})
$$
拓展到矩阵（一次计算所有样本的所有特征）
$$
Z^{(l+1)} = W^{(l)} \ {^{t}A^{(l)}}
$$
注意到在拓展过程中 $W$ 和 $A$ 顺序的交换，导致数值计算写起来不直观……（也有可能是抄错了，反正不影响实际编程）

## Classification de chiffres

`MNIST.py`

给了个示例程序。

----

### 额外参数

$\alpha$: momentum
$$
\Delta W_t = \eta \nabla J( W_{t-1} ) + \alpha \Delta W_{t-1}
$$
d: decrease reduce the leanring rate
$$
\eta /(1 + t \cdot d)
$$

## Entraînement

### fonction de coûts

$$
J(w) = \sum_{i = 1}^n {y^{(i)} log(a^{(i)}) + (1 - y^{(i)}) \cdots}
$$

加正减负。

## Backpropagation

Nous commençons donc par trouver le vecteur d'erreur
$$
\delta^{(3)} = a^{(3)} - y
\\
\delta^{(2)} = (W^{(2)})^T (\delta^{(3)} * \frac {\partial \phi (z^{(2)})}{\partial z^{(2)}})
$$

$$
\frac {\partial}{\partial w^l_{i, j}} J(W) = a_j^{(i)} \delta^{(l+1)}
$$

（换ppt太快，失记）

