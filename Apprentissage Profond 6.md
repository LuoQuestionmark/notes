# Apprentissage Profond 6

## Introduction

NLP, en machine learning, il s'agit de :

- nettroyer et préparer les données 准备数据
- construire une représentation viable de textes pour le ML 统一尺寸
- entraîner un modèle afin de classer les textes
- travailler avec de larges textes

## Nettroyage du texte

神经网络“不是很需要”清洗数据——可以在内部完成。

Stemming：去掉标点符号、去掉复数，变形、去掉 mot vide （无关紧要的词）。

## Bag o words

Convertir les données textuelles ou catégoriques en termes numériques.

**Bag-of-words** : permettre la conversion e texte en vecteurs de caractéristiques. 将词汇转化为向量。一个词换成一个列表中的一个元素；之后对每个句子创造一个对照表，表示其中出现的词汇（及数目）。
如：对一个句子的演绎为——其中出现了三次“太阳”、两次“照耀”、零次“月亮”……

Les valeurs de nos vecteurs sont appelées "raw term freauencies" `tf(t, d)` -- nombre de fois où un terme $t$ apparait dans un document $d$.

Ce type de séquence est aussi appelée un 1-gram ou unigram.

### fréquence des termes

dans la fréquence pure des termes n'est souvent pas très utile. 可能会出现量词什么的，没用。

la pertinence n'augmente pas proportionnellement avec la fréquence. 以及出现频率和重要性不一定呈比例关系。

### pondération avec `tf-idf`

$$
tf-idf(t,d) = tf(t,d) \times idf(t,d)
$$

$$
idf(t,d) = \log \frac {1 + n_d} {1 + df(d,t)}
$$

（有多种变种，用于解决[上文](### fréquence des termes)提出的问题）

## Représentation one-hot

méthode d'implémentation la plus simple, pas de fréquence prise en considération, encodage est énorme.

这一次与上面的区别在于顺序得到了保存——尺寸更大。

## Word Embedding

Une représentation apprise

Nécessitedes tonnes de données d'entrainement et énormément de temps.

Chaque mot va être représenté par un vecteur de nombres réels

Conceptuellement, cela implique un *embedding* mathématique d'un espace avec de nombreuses dimensions par mot à un espace vectoriel. 将词汇与数学空间联系起来，可以比较比如词汇间的距离。

### skip-gram

失记

总体来说 embedding 固定了尺寸。

## Réseau de neurones récurents RNN

aka *Recurrent Neural Network*

Une famille de réseaux de neurones qui sert aux données séquentielles.

灵活：单个或多个输入、单个或多个输出、不确定的隐藏层

### intuition

partage de paramètres à travers différentes parties du modèle comme avec les CNN

si nous devions utiliser des paramètres différents pour chaque valeur de temps, nous ne pourrions pas généraliser

de plus, nous ne pourrions reléter l'importance d'une sous séquence

### récurrence

$$
s^{(t)} = f(s^{(t - 1)}, x^{(t)}, \theta)
$$

$x^{(t)}$: 外部变量

$\theta$: （超）参数
$$
h^{(t)} = g^{(t)}(x^t, x^{t-1}, \cdots, x^!)
= f(h^{(t-1)}, x^{(t)}, \theta)
$$
$h^{(t)}$ est la variable qui représente l'état

en langage naturel, par exemple, le RNN peut servir à prédire le mot suivant selon le mot déjà lu.

on associe une séquence de taille arbitraire de $x$ par une taille fixe de $h$
$$
h^{(t)} = \tanh (Ux^{(t)} + Wh^{(t-1)})
$$
既考虑输入，又考虑时间上的“过去”。

$W$ 是一个矩阵。

## Entraînement

### séquence cible

somme de l'erreur :
$$
E = \sum_{t=0}^\tau {E(t) (y^{(t)}), x^{(t)}})
$$
propagation :
$$
\frac {\partial E^{(2)}} {\partial U} = \frac {\partial E^{(2)}} {\partial h^{(2)}} (x^{2}) = \cdots
$$
挺复杂的计算，有两个方向的偏微分（输入、之前的输出）

## Exemple : Reconnaissance Genre Musical

类似的处理：先把输入数字化，变成矩阵。

之后放到 RNN 网络中训练——分辨音乐的流派。

ReLU doesn't work very well with this system.

## Exemples : Machine Translation

输入（某一语言）—— RNN —— encoded sentence —— RNN ——输出（另一语言）
