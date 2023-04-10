# Apprentissage Profonde 6 autoencodeurs

## Introduction

Nous avons mentionné le fameux problème du "curse of dimensionality". Il existe différentes méthodes de réduction de la dimensionalité.

Principal Component Analysis (PCA) qui tente de modifier la représentation avec moins de dimensions. C'est une façon de compression de données.

## Autoencoder

Les autoencodeurs sont :

- spécifiques aux données
- avec pertes
- entraînés automatiquement

Un réseau de neurones à 3 couches ou plus. 对应以上的三层。

### Application des autoencodeurs

débruitage des données

réduction de dimensionalité

features extractions

### Autoencodeur avec Keras

Sur l'ensemble MNIST, couche cachée 32 untés (ratio de compression 24.5)

输入：像素矩阵

中间层：数据*

输出：像素矩阵

中间层的尺寸较小，即实现了“有损压缩”。

### Deep autencoder

avec une prodonde plus importante, la qualité est meilleure (?)

## Convolutional Autoencoder

卷积不具有可逆性，虽然如此，逆操作仍然可以恢复一定的信息。

Application : augmentation de résolution

### upsampling

复制值，bi-linear interpolation, bed of nails (加零)。

### un-pooling

将变换的数据放入原来最值所在的位置，其它地方填零（有损）。

## Variational Autoencoder

中间层是多个“分布”——decoder由分布重新生成个体。

VAE 的代码在 PPT 里面。

### Deep recurrent attentive writer

在以上网络基础上加入“时序”，第一个 decoder 的结果喂给第二个 encoder ……

