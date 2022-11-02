# IA 4 : Incertitude

(et la probabilité)

## Incertitude

假设 $A_t$ 为飞机提前 $t$ 分钟入库事件。

Problèmes : 

- partiellement observable
- bruits dans les capteurs
- incertitude dans la réalisation des actions
- complexité importante en ce qui attrait à la modélisation et à la prédiction de trafic

### Méthodes pour gérer l'incertitude

- logique non monotone

- difficile de déterminer quelles hypothèses sont raisonnables et comment gérer les contradictions

- règles avec facteurs arbitraire
  $$
  A_{25} \implies _{0.3} AtAirPortOnTime \\
  Sprinkler \to _{0.99} WetGrass \\
  WetGrass \to _{0.7} Rain
  $$

- problème avec les combinaisons

## Probabilité

- Les assertions probabilistes résumes les effets de
  - la paresse
  - l'ignorance
- Probabilités bayésienne :
  - mes probabilités s'appliquent sur les connaissances d'une personne sur les connaissances

*条件概率，后验概率*

## Prendre décisions dans l'incertitude

Supposons que :
$$
P(A_{25}) = 0.04 \\
P(A_{90}) = 0.7 \\
P(A_{120}) = 0.95 \\
\vdots
$$
**Decision theory = utility theory + probability theory**

## Bases

*复习数学，懒得抄。*

### Proposition

将逻辑命题转换为概率判断
$$
(a \lor b) \implies P(a \land b) + P(a \land \lnot b) + \cdots
$$

## Syntaxe et sémantique

## Inférence

“推断”：其实指求某个事件概率的方法。

### inférence par l'énumération

（画表）穷举。

## Indépendance et règle de Bayes

*not fucking again...*

### indépendance

$$
P(A \land B) = P(A)P(B)
$$

----

### Exercice indépendance

#### Question 1

$$
P(int \land etudie) & = & 0.432 + 0.048 = 0.48 \\
P(int) & = & 0.48 + 0.32 = 0.8 \\
P(etudie) & = & 0.48 + 0.084 + 0.036 = 0.6
$$

$$
\because P(int \land etudie) = P(int)P(etudie) \\
\therefore independent
$$

----

### indépendance conditionnelle

那个链状的公式：
$$
P(A \land B \land C) = P(A|B \land C)P(B \land C) = \cdots
$$

### Règle de Bayes

$$
P(B|A) = \frac{P(A|B) P(B)}{P(A)}
$$

## Naive Bayes Classifier

$$
P(Cause, Effet_1, \cdots, Effet_n) = P(Cause) \prod_I Effet_i
$$

## Réseau bayésien

Une table TPI décrivant la probabilité initiale des noeuds racines ;

Une table TPC décrivant la probabilité ...

### Exemple de reconnqissqnce d'AVQ

待查

## Définir la reconnaissance en termes de processus de décision bayésien

不同的“假设”互相竞争，根据“观察”选择最可能的。

