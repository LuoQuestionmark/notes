# Apprentissage Profond 3 tour des algorithmes

## Algorithme de classification

un très grand nombre d'algorithmes de classification

aucun algorithme n'est parfait.

## Introduction à Scikit Learn

simple and efficient tools, build on `numpy `, `matplotlib`, etc...

éviter utiliser la fonction `fit` sur le modèle

plusieurs classeur...

## Tour des algorithmes

### paramétrique ou non ?

paramétrique : simple, apprentissage rapide, peu de données requises, etc.

non-paramétrique : flexible, puissant, performant pour la prédiction, surapprentissage, plus lent, etc.

“深度学习除外”

### Logistic Regression

Fonction de coûts pour Logistic Regression

$L$: loss function

($log L$): Les $log$ permettent d'éviter les *underflow*.

### SVM

dans SVM, maximiser la marge entre les classes

切分空间使其到每个类的距离最远。

#### SVM VS Logistic

donnent des résultats similaires en pratique

#### Kernelisation

Le SVM est populaire parce qu'on peut facilement faire de la kernalisation.

改变样本空间，classeur linéaire vers non-linéaire

----

SVC, NuSVC, LinearSVC, SVR, NuSVR, LinearSVR

### KNN

choisir un nombre de voisins $k$ et une mesure de distance

trouver kes $k$ voisins les plus proches de l'exemple à classer

faire un vote

### Arbre de décision

nous commençons d'une racine et séparons les données sur l'attribut qui perlet d'obtenir le plus grand **gain d'information**.

avantage : l'explicabilité et la transparence des modèles.

- Classification and Regresion Trees
- Iterative Dichotomiser
- C4.5
- Very Fast Decision Trees
- etc.

## Surapprentissage

深度学习：即使有大量参数仍然可能欠学习。

## Biais, Variance

定义：已知。

bias-variance tradeoff

Le compromis se situe au niveau de la configuration des algorithmes. 如KNN的$k$值。

## Régularisation L2

idée : introduire un nouveau biais pour péaliser les valeurs extrêmes de poids.
$$
\frac \lambda 2 || w || ^ 2 = \frac \lambda 2 \sum_{j=1}^m {w^2_j}
$$
减少极值，降低误差，增加方差？

L1 又名 LASSO。

## Ensemble learning

使用多个系统，“投票”。

### bagging

sous-ensemble du dataset pour l'entraînement

- boostrap
- généralement un arbre non-élagué

principaux algorithmes : 

- random forest
- extremely randomized trees
- wagging

### stacking

```pseudocode
for t = 1 ... T
	h_t = L_1(D)
end

D2 = \emptyset
for i = 1 ... m
	for t = 1 ... t
		z_it = h_t(x_i)
	end
end

// then train on the dataset D2
```

### boosting

1. maximisation de la fonction de coûts ;
2. on ajoute les poids, on entraîne un second classeur ;
3. on ajoute les poids, on entraîne un troisième classeur ;
4. on combine les classeurs par vote.

### adaboost

1. le vecteur de poids $w$ est initialisé : somme = 1;
2. pour $j$ dans m cycles de boosting, faire :
   1. entraîner un classeur faible $C_j = train(X, y, w)$;
   2. prédire les classes
   3. calculer le taux pondéré d'erreurs
   4. calculer un coefficient $\alpha_j = 0.5 log \frac {1 - \epsilon} \epsilon$

...

#### variantes

real adaboost

gentle adaboost

softboost, interactive...

### gradient boosting

https://en.wikipedia.org/wiki/Gradient_boosting
$$
\hat y^{(0)} = 0 \\
\hat y^{(1)} = y^{(0)} + f_1(x_i) \\
\hat y^{(2)} = y^{(1)} + f_2(x_i) \\
\vdots
$$
