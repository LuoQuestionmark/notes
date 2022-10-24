# IA 3 Système expert

[TOC]

## Système expert

*Système à base de règles de production*

专家给规则 (mémoire à long terme)

用户出点子 (modèle de dialogue avec l'usager + mémoire de travail)

系统作推断 (moteur d'inférence)

intelligence explicable 

但是据说不好用……

## Connaissances assertionnelles

Les connaissances assertionnelles décrivent des situations considérées comme établies ou à établir.

事实和假设

## Connaissances opérationnelles

règles de production

- déclencheur (si)
- corps (alors)

## Fonctionnement d'un moteur d'inférence

un moteur d'inférence est un composant logiciel qui correspond à un algorithme de simulation du raisonnement déductif.

*从逻辑学来*

一阶逻辑、二阶逻辑……

### moteur d'inférence vs algo classique

les règles de raisonnement sont séparées de leur mécanismes

le chemin de résolution de problème n'est pas bâti à l'avance

les systèmes basés sur la programmation logique offrent :

- facilité de modifier les connaissances du système
- des opportunités d'apprentissage

### types de règles d'inférence

*童年的味道*

Modus ponens 肯定前件

Modus tollens 否定后件

### cycle d'un moteur d'inférence

- filtrage
- choix d'une règle
- appliquer la règle

### chaînage

*应用事实的不同顺序*

#### chaînage avant

#### chaînage arrière

反向；把结论放在栈里面，之后反推希望的事实。

## Stratégies de recherche

> 之前说过了，不讲了

### choix d'une règle à une étape

- par simplicité
- par complexité
- par priorité
- autre

## Facteurs de certitude

## Avantages des systèmes experts

- Représentation de connaissances naturelle
- Structure uniforme

## Inconvénients

- Relation opaque entre les règles
- Stratégie de recherche inefficace

### Inapte à apprendre

- un système expert ne peut pas apprendre à partir de son expérience
- ne peut pas ajouter/modifier des règles   

----

# Incertitude

## Incertitude

- l'information peut être incomplète, inconsistante et incertaine.
- l'incertitude se définit comme le manque de connaissance qui pourraient nous permettre d'atteindre une conclusion parfaite fiable.

### source

incertitude, langage imprécis

## Règles avec cf

1 确信有， -1 确信无。

```pseudocode
IF		A is X
THEN	B is Y {cf 0.7} // possibilities
		B is Z {cf 0.2}
```

```pseudocode
cf(H, E) = cf(E) * cf(H)

IF		sky is clear
THEN	the forecast is sunny {cf 0.8}

cf(H, E) = 0.5 * 0.8 = 0.4
```

### 多条证言

$$
cf(H, E_1 \cup E_2) = max[cf(E_1), cf(E_2)] \times cf
$$

*相当不严谨呵*

### 组合

$$
cf(cf_1, cf_2) =
\left\{
\begin{array}{**lr**}
	cf_1 + cf_2 \times (1 - cf_1) & cf_1 > 0 \land cf_2 > 0 \\
	\frac{cf_1 + cf_2}{1 - min[cf_1, cf_2]} & cf_1 < 0 \lor cf_2 < 0 \\
	cf_1 + cf_2 \times (1 + cf_1) & cf_1 < 0 \land cf_2 < 0 \\
\end{array}
\right.
$$

## Environnements de développements

+ Jess
+ CLIPS
+ Expert System Shell
+ TMYCIN
+ Experta

```CLIPS
(assert (monFait))
(assert (monFait))
(facts)
(initial-fact)
(reset)

(assert(a)(b)(c)(d))
(clear)

(assert(animal-est canard))
; comment
(run) ;
```

