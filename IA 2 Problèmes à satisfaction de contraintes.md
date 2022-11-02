# IA 2 ：Problèmes à satisfaction de contraintes

## Introduction

- problème d'exploration standard

- constraint satisfaction problems (CSP)
  - un état est défini par des variables X, avec des valeurs dans un domaine D

- exemple simple de langage de représentation formelle
- permet l'utilisation d'algorithmes à des fins générales plus puissants que les algorithmes d'exploration standards

### Exemple : Map-Coloring

|             |                     |
| ----------- | ------------------- |
| variables   | {WA, NT, Q, ...}    |
| domaines    | $D_i = \{r, g, b\}$ |
| contraintes | 相邻颜色不同        |

### Assignement

Les solutions sont des assignements complets...

### Graphe de contraintes

- CSP binaire ： 限制存在与两两变量之间
- Graphe de contraintes : 节点为变量、关系为限制

### Variété des CSP

- var discrètes
  - domaines finis
  - domaines infinis
- var continues

### Variétés des contraintes

一元 二元 多元 “偏好”[^1] 

[^1]: “红色好于绿色。”

### Exemple de cryptarithmétique

对字母赋值使得等式成立。

种种限制可以转化为一个图问题。

### CSP dans le monde réel

- problème d'assignements
- assignements temporel
- configuration matériel 

## Résolution de CSP

### formulation standard d'exploration

- commencer par l'approche directe, puis l'améliorer
- les états sont définis par les valeurs assignées jusqu'à présent

### backtracking

- 解法（赋值）的可交换性
- 递归调用，子代（完全）失败则父代失败。

### augmenter l'efficacité du backtracking

- quelle var devrait être assignée ensuite ?
- dans quel ordre les valeurs devraiment-elles êtres testeés ?
- ...

#### minimum remaining valus

- valeurs minimales restants : 从最少选择的变量开始。

#### degree heuristic

- choisir la var avec le plus grand nombre de contraintes sur les var restants

#### least constraining value

优先选择“最不受限”的变量。

#### forward checking

garder une trace d'un vlaeurs légales

## Algo de CSP

- propagation des contraintes
- arc consistency

例子：数独

### Structure du problème

#### CSP en structure d'arbre

改变结构。conditionnement

### Exploration locale pour CSP.

hill climbling, le recuit simulé, ...

### Performance de CSP
