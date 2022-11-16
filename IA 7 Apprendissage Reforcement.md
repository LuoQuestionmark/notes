# IA 7 Apprentissage Par Renforcement

## Introduction

### type de apprentissage machine

- 有监督学习：任务导向
- 无监督学习：数据导向
- 强化学习：
  - 类似人类学习
  - agent 的选择对 env 有影响
  - env 对 agent 行为有所反馈


### agent

mathématiquement, un agent est complètement spécifié par une fonction d'agent

### environnement de renforcement

例如：电子游戏中人物应当尽快移动到终点——不移动时给予负反馈

## Élément de base

L'environnement peut être inconnu, stochastique, complexe. Il est cependant séquentiel.

Maximisation de la récompense dans le temps.

### Dilemme Explore vs Exploite

## Élément du RL

- police
  - association état/action
  - comportement de l'agent
- fonction de récompense
  - but dans le problème de RL
  - association état/action avec un nombre réel
  - ne change jamais, mais peut affecter la police

### Exemple

- La stratégie classique en exploration adverse : Min-Max
- ...

### Exemple : fonction de valeur

table de chiffres pour chaque états possibles

dernière estimation de la chance de l'état : gagner la partie

la table est donc la fonction de valeur apprise

si $A > B$, alors l'état $A$ est meilleur.

si $S_t$ l'état précédent et $S_{t+1}$ l'état courant, alors la valeur est :
$$
V(S_t) = V(S_t) + \alpha [V(S_{t+1} - V(S_t))]
$$
$\alpha$ 反馈常数。

### Interface Agent-Environnement

L'agent et l'env interagissent en temps discret.

### Tâche Associative ou non

- tâche associative
  - dépend de la situation
  - association de situations aux actions qui sont les plus capables
- tâche non-associative
  - ne dépend pas de la situation
  - pas d'associations d'actions qui diffèrent selon la situation
  - tâche stationnaire 最优解永远是最优解
  - tâche non stationnaire ……不一定，随时间变换

## N-Bandits

Chaque action a une récompense moyenne : 

- la valeur de cette action
- c'est une estimation maintenu, si nous la connaissions ; trivial

Posons la vraie valeur de l'action $a$ comme $Q^*(a)$

### Sample-Average method

取加权均值？

### Choix d'actions

En supposant $Q_t(a) \approx Q^*(a)$, l'action gloutonne au temps $t$ est :

...

### Sélection $\epsilon$ greedy

训练时随机选择。

Dans l'approche purement gloutonne, on ne fait qu'exploiter.

### Sélection Softmax

Notre sélection était aléatoire, mais uniforme.

Avec softmax: 
$$
\frac{e^{Q_t(a)/t}}{\sum_b {e^{Q_t(b)/t}}}
$$

#### maj incrémentale

$$
Q_n = \frac{R_1 + R_2 + \cdots + R_{n-1}}{n-1} \\
Q_{n+1} = Q_n + \frac{1}{n} [R_n - Q_n]
$$

有$\epsilon$ 机会选择随机行为，$1 - \epsilon$ 机会选择最佳解。

### Problème non-stationnaire

### Méthode Poursuite

On incrémente la probabilité $a_{t+1} = a^*_{t+1}$ de cette façon :
$$
\pi_{t+1} (a^*_{t+1}) = \pi_{t+1} (a^*_{t+1})  + \beta[1 - \pi_t(a^*_{t+1})]
$$
les autres son t décrémentés.

## Préférence d'action

Dans le RL, les actions qui mènent à de grandes récompenses devraient être sélectionnées plus souvent...

Référence reward : on peut calculer la moyenne des récompenses.

