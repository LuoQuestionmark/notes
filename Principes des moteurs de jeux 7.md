# Principes des moteurs de jeux 7 : audio

## audio

ambiance, tuto, SFX, discussions

période, amplitude

20Hz-20000Hz

频响曲线，在大概某个频率听力最好……

## musique

“十二平均律”

中央C，$^{12}\sqrt{2}$

基音，泛音

## pipeline audio

听小骨、鼓膜…… $\larr$ 音源 $\larr$ 声卡 $\larr$ CPU

DAC: numérique vers analogue

ADC: 反向。即麦克风。根据 précision 需要作一定量的运算计算精确的电压。

## 音频位数、采样率

8 bits $\rarr$ 256, 16 bits $\rarr$ 65536

44 kHz, 2 canaux, 74 minutes $\approx$ 800 Mo

### 无损、有损

FLAC, MP3

## MIDI

由于本身不包括乐器信息，需要电脑自带音源。

musique ambiance : envoyer les événements, moduler ces sons. (analogue de midi ; séquençage)

## Génération onde

[chiptune](https://fr.wikipedia.org/wiki/Chiptune)

正弦波、方波、三角波……

## Audio 3D

- Mono
- Stéréo
- Ambio

[Binaural](https://en.wikipedia.org/wiki/Binaural_recording) 人头麦克风。

7.1.2

7 普通

1 低音

2 “高”，高音喇叭 - 放在高处

根据波长计算证明人无法分辨高音低音方向。

----

计算远处音源

auditeur + position de l'auditeur

position de la source

[多普勒效应](https://zh.wikipedia.org/wiki/%E5%A4%9A%E6%99%AE%E5%8B%92%E6%95%88%E5%BA%94) : vitesse relative

混响 : matériaux acoustiques

（低通滤波器处理“墙后声音”）

光追计算声音