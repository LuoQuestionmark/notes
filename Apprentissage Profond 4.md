# Apprentissage Profond 4 Fonctions d'activation, évaluation et tests

## Fonctions d'activation

偏好非线性单调函数。可微。非单调的表现可能会“奇怪”，但是有应用。

### `sigmoid` et `tanh`

过去常用的函数，单调可微。

### Rectified Linear Unit `RELU`

Moins de problème de gradients, les opérations sont plus simples.

Beaucoup de valeurs d'unités `ReLU` est à 0. Peut être trop simplifié. "Dead ReLU".

#### `Leaky ReLU`

$$
\begin{array}
& f(x) = x & if & x > 0 \\
f(x) = \alpha x & if & x < 0
\end{array}
$$

当 $\alpha = 0$, 退化到 `Relu`。

#### `Relu` 和稀疏矩阵

由于其中有很多零值，可以用稀疏矩阵节省空间。

### Exponential Linear Unit

$$
\begin{array}{cccc}
f & = & x & x > 0\\
f & = & \alpha(e^x - 1) & x \leq 0
\end{array}
$$

### Scaled ELU

$$
f(x) = \lambda x \\
f(x) = \lambda \alpha(e^x - 1)
$$

固定的 $\alpha, \gamma$ 数值。

平均值0，方差1。

### SWISH

Développé par Google Brain et basé sur PFLU.
$$
f(x) = x * \frac 1 {1 + e^{-x}}
$$
当有一个较小的负值时仍然有更新。

### Softmax

La somme de probablités devient égale à 1. Chaque classe vaut entre 0 et 1.

直接完成了对结果的演绎。

指数运算、正则化。之后用 $-log$ 求 perte.



## Evaluation et tests

一些学过的定义，true positive, false positive, etc.

### F-score

$$
F_{\beta} = (1 + \beta ^ 2) * \frac {Precision + Recall} {(\beta ^ 2 * Precision) + recall}
$$

衡量 precision 和 accuracy 关系。“不平衡”的数据集可能导致较大区别。

### Kappa

另一个衡量的工具，更 robust，但是对多个类效果不佳。

### Matrice de confusion

### Receiver operator curve (ROC)

选择好的门槛（theshold）。

https://en.wikipedia.org/wiki/Receiver_operating_characteristic

### Others (multiclass)

`micro`, `samples`, `macro`, `weighted`, `None`.

## Notes sur l'optimisation du modèle

Il est important que les données de test ne soient utilisées en aucune façon pour créer le classeur.

Certains programmes fonctionnent en deux étapes : construire la strcuture de base ; optimiser les réglages des hyperparamètres.
所以可以有三个数据集: train, test, validation. Validation 用于选择合适的模型。

Si le modèle fonctionne bien, on peut re-entraîner le modèle pour toutes les données.

### K-Fold cross validation

拆开数据集，如三分之一测试，三分之二作训练。重复三次。

## La fonction de coûts

La fonction de coûts dans un réseau de neurones sert principalement à mesurer l'erreur de chaque unité à chaque couche.

### fonctions simples

一范数、二范数。

### cross entropy

$$
H(p, q) = \sum_{x \in X} p(x) \log q(x)
$$

CE 和 NLLL 的输出格式不同，但是计算近似。

### hinge loss

$$
J(W) = \frac 1 n \sum max(0, 1 - y * \hat y)
$$

Principalement utilisée dans les SVM.

### Kullback-Leibler

$$
D_{KL}(p, q) = \sum_{x \in X} {p(x)(\log p(x) -\log q(x))}
$$

KL vaplus loin que l'entropie en calculant comment compresser de façon à s'aooriher de l'encodage optimal.

较小的结果代表较少的信息丢失。

### similarité cosines

$$
cos \theta = \frac {\vec a \cdot \vec b} {||\vec a|| \ ||\vec b||}
$$

“相似程度”。