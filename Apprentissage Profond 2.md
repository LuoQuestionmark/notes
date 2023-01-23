# Apprentissage Profond 2 neurone 神经元

## un bref historique du ml

1943, 神经节原理……

## perceptron

1953, Z est l'entrée nette composé d'une combinaison linéaire d'entrées $x$ et de poids $w$.
$$
z = \sum_{i} w_i x_i \\
\phi(z) = (z > 0)
$$
on ajoute également $x_0 = 1$ et $w_0 = \theta$, $\theta$ est le *biais*. 

*换言之是单层的神经网络， 用一个超平面分割数据集*

### fonctionnement de l'apprentissage

1. initialisation des poids à 0 ;
2. pour chaque exemple d'entraînement $x^{(i)}$:
   1. calculer la sortie estimée
   2. mettre à jour les poids

$$
\Delta w_j = \eta \ (y^{(i)} - \hat y^{(i)}) \ x_j^{(i)}
$$

le poids ne changera pas si la prédiction est correcte

il varie automatiquement en fonction de la valeur de $x_j^{(i)}$ dans le vecteur d'entraînement $i$. 

### bilan

si pas séparable linéairement, perceptron Maj à l'infini. (il faut donc d'autres algo, ou changer les data)

## classification

### one-vs-all

*每次分出一个种类的二分法？*

### one-vs-one

## adaptive linear neurons

### adaline

$$
\phi = id_E
$$

Les sorties sont des valeurs continues.

Un élément "Quantizer" permet d'interpréter le résultat final.

### fonction de coûts

l'erreur sur l'ensemble de données.

pour adaline,
$$
J(w) = \frac 12 \sum_i {(y^{(i)} - \phi(z^{(i)})) ^ 2}
$$

### algorithme du gradient

$$
\Delta w_j = - \eta \frac {\partial J} {\partial w_j}
$$

## vocabulaire

### hyperparamètres

$\eta$, le "learning rate" et le nombre d'"epohs" sont ce qu'on appel des hyperparamètres.

des méthodes existent pour automatiquement calibrer les hyperparamètres.

### epochs / batch / iteration

epochs :
passage entier d'un ensemble de données une fois.

batch:
一部分的数据

itération:
nombre de batches nécessaire pour compléter 1 epoch.

## stochastic gradient descent

*随机梯度下降*