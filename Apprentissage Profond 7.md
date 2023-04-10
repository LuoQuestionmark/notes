# Apprentissage Profond 7 architectures et applications avancées

## Problème de l'apprentissage

Trois grands types d'apprentissage. 有监督、无监督、强化学习。Est-ce qie l'apprentissage humain correspond réellement à ces types d'apprentissage ?

Auto-apprentissage "self-supervised".

## Mécanisme d'`attention`

Ils sont particulièrement efficaces lorsqu'on traite de séquences et séries temporelles.

Le mécanisme se décrit comme étant le mapping entre :

- une requête
- un semble de paires clé-valeur à une sortie

（每个元素会关联另一个域中的某个子集。）

### version originale

有一个 encoder/decoder 组，每个隐藏状态被用于一个 RNN （注意力）的学习。这个网络用于给训练的主要的 RNN 额外的数据（赋予注意力）。新的机制使得网络可以“专注于”整个数列。

## Transformers

- non séquentiel
- auto-attention
- embeddings positionnels

### encoder

- 整体输入
- 加入对“位置”的信息
- multi-head attention
- encoder + lien résiduel

（多层）

#### multi-head attention

8 models d'attention - fait attention sur différentes choses.

## 其它

### ELMO 2018

双向的 propagation 。Le modèle à deux blocs de Bi-LSTM 4096 unités (4 couches de LSTM).

### GPT

### BERT

Bidirectional Encoder Representations from Transformers.

### Stable diffusion 2022

Auto-encoder, attention, encoder, decoder, etc. 

训练：正常的输入，添加多层的“添加噪音”，直到完全随机。与此同时训练相反的模型，即从白噪音生成图片。

### DALL-E
