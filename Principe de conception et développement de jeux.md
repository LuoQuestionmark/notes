# Principe de conception et développement de jeux

*欠的先欠着，平台叫moodle。*

[TOC]



## Gameplay

- terme oniprésent
- empiriquement rattaché à la qualité d'un jeu
- ...

(def from wikipedia) the specifique way in which players interact with the game

interface - règles - monde/univers - interface sortie

### une approche du gameplay

- un semble des règles
- des modes de commande
- organisation spatial
- ... temporarie

### coeur de jeu

Le coeur de jeu est le mécanisme de jeu central. A partir duquel l'eesentiel du gameplay va se construire. “核心玩法”

gestion de ressource

#### exemple : jeu de course

Le coeur de jeu est le pilotage.

La qualité du pilotage affecte la qualité du plaisir.

----

le coeur représente 90% de jeu.

#### exemple : fps

#### exemple : plateforme

----

jeu bicoeur/multcoeur

### trouver des coeurs

“艺术源于生活”

### briques de gameplay

#### exemple : mario

- la topologie

- la plateforme
- la plateforme mobile
- la plateforme rotative

### Game design vs. Level design

### boucle de jeu

objective $\to$ challenge $\to$ récompense

#### boucles de jeu

*“大循环里小循环”*

### implémentation du gameplay

*un jeu est une suite de choix intéressants*

#### problème : stratégie dominante

*“最优套牌”*

#### stratégie quasi-dominante

#### les contre stratégie

“猜拳”（其实用例街霸升龙拳）

### options stratégies

长期效益－短期效益

#### exemple : starcraft

- moderniser les fusils des marines
- impact tactique contre les ennemis forts mais lents

----

#### investissements de soutien

第一目标－第二目标

#### option polyvalentes

#### facteurs de compensation

#### fugacuté 短期buff

#### synergies

----

### équilibre et balance de éléments

- équilibre pvp
- équilibre joueur/gameplay　《血源》
- équilibre gameplay/gameplay

#### joueur/joueur

un jeu doit éviter les éléments aléatoire qui favorisent un joueur ou dont les effets s'amplifient au cours de la partie

...

la symétrie *CS 1.6* *国际象棋*

#### joueur/gameplay

难度曲线，动态难度

#### gameplay/gameplay

机制平衡性　擒抱／轻击／重击

## le flow

### la notion du flow 心流

难度机制：Karby v.s. Dark Souls

### élément du "flow"

简单一般困难。动态难度。

----

document de désign : 精确详细。

那个马里奥设计原则：介绍机制、使用机制。

----



## Ergonomie

> La compréhension fondamentale des interactions entre les être humains et les autres composantes d'un système.

### Interface de jeux ergonomique

- efficase
  - permet d'accimplir les poches réguilières de façon efficase
  - réduit les erruers et le temps
- intuitive

#### critères de succès

- réduit l'énergie nécessaire
- contiens toute l'information nécessaire
- facile à apprendre, prévient les erreurs

### Principaux éléments d'ergonomie

- interaction
- densité d'information
- ...

### Interaction homme-jeu

temps de traitement

limite de la mémoire

objectifs

#### limites congnitives

- attention visuelle
  - 5 deg
  - quatre éléments perçus simutanément
  - fixation : 10s pour une recherche non structuré
- mémoire court terme : $7 \pm 2$

#### densité de l'information

Performation humaine pour les tâches de recherche est optimale entre 25 et 40% de densité.

----

présentation seulement l'information nécessaire

- tâches fréquentes

- menu secondaire
- default value

retirer l'information inutile

#### groupement

délimiter les groupes

- espaces entre les groupes, symétrie
- format...
- couleurs

#### organisation des éléments

例：按频率排列。

#### compatibilité : collocation

信息与目标排在一起、或连上线。

#### rédaction et lisibilité : texte

police sans serif, 非大写等等。

#### uniformité et standards

名字菜单风格

#### rétroaction au joueur 反馈

#### gestion des erreurs

prévenir, empêcher, détecter, recouvrir, messages d'erreur simples et explicites

### Evaluer l'ergonomie d'une interface

准备场景、准备人、准备例子。