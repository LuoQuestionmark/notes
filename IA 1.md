# IA

## Exploration Locale

- Hill Climbing
- Simulated annealing
- Genetic algorithms
- ~~Exploration locale dans les espaces continus~~

Bonne solution dans le temps raisonable.

### Algorithmes d'amélioration itérative

Dans de nombreux problèmes, le chemin n'est pas important

Dans ce cas, l'espace d'états = ensemble des configurations complètes

Dans ce cas, nous pouvons utiliser les algorithmes d'amlioration itérative

### Exploration local

- fonctionne pour les environnements non-déterministes ou partiellement observable

- utilise peu de mémoire

- trouve des solutions raisonnables rapidement

- fonctionne pour des problèmes d'explorations non-standards

#### exemple : 八皇后（n皇后）问题

### Hill-climbing 梯度下降/上升

- défis
  - les maximums locaux
  - ne sort pas d'un plateau
  - si le pas est trop grand
- escalade stochastique
- escalade du premier choix
- escalade avec reprise aléatoire
  - plusieurs HC avec un départ aléatoire différent à chaque fois.

与贪心算法的区别：不取消“更差状态”、不存储某些结果。

### Simulated annealing 退火算法

```python
for t = [1:inf]
	T = schedule[t]
	if T == 0:
		return current
    next = a randomly selected successor of current
    E = value[next] - value[current]
    if E > 0:
    	current = next
    elif if (e ** (E/T)):
    	current = next
```

### Local beam search

Idée : garder k états plutôt que 1 mieux exploiter la mémoire disponible

- choisir k états au hasard
- les k explorations roulent en parallèle
- sélectionne les k meilleurs états parmi tous les successeurs

LBS : les explorations s'échangent les informations.

### Genetic algorithms

*反正也做过项目了*

----

## Exploration Adverse

- modélisation de problèmes
- l'algorithme minmax
- élagage alpha-beta
- jeux stochastiques

*或许确实不该选这个，学过……*

### De simple agent à multiagent

les actions n'ont plis de résultats prévisibles

situation compétitive

espace d'états potentiellement beaucoup plus large

limite de temps

#### exemple : jeu partiel pour le Tic-Tac-Toe

### Que recherche t'on ?

- construire une stratégie ou un plan de contingence plutôt une séquence
- les mouvements de l'adversaire doivent être pris en compte
- représentation de la stratégie

### Minmax

Le processus d'étiquetage conduit à la décision qui garantit un gain maximal. 

假设对方最佳、假设对方理性。

#### évaluation de minmax

compmète : oui

optimal : oui

complexité : $O(b^m)$

complexité spatiale : $O(bm)$ (DFS)

#### problèmes

- 限制深度
- 剪枝
- assumer que l'heuristique représente la fonction de récompense

### Fonction d'évaluation

----

### Elagage Alpha-Beta

- objectif : calculer la valeur MinMax d'un arbre d'exploration
- sur le chemin courant, noter le meilleur choix pour alpha/beta

在遍历的同时剪枝、效率依赖于遍历顺序。

avec un ordre parfait, on peut doubler la profondeur de recherche maximal, branching factor $\sqrt{b}$.

## Jeu avec un élément de chance

### expectiminimax (!)

添加一个MAX一个MIN层，然后把随机过程放在中间。Max-Dice-Min-Dice-Max. 还有加权平均数。

【可能minmax在此不重要，只是决策的抽象。】

问题：数值对选择很重要，期望和方差--小概率得到极大值导致选择变化。

----

----

## chess project

http://www.playwitharena.de/ 参考？
