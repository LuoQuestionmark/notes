# Principes des moteurs de jeux : animation

Définition d'animation. 随*时间*变化。

- animations matricielles
  - vidéo
  - sprintes
- animations vectorielles
  - 2D
  - 3D

## animations matricielles

### vidéo vs. sprite

|            | vidéo                  | sprite                  |
| ---------- | ---------------------- | ----------------------- |
| forme      | rectangles[^1]         | arbitraire              |
| 透明度     | opaques                | transparence            |
| 循环       |                        | boucler (?)             |
| sauvegarde | compression[^2], H.264, [trame][####trame I, P, B] | feuille de sprite (PNG) |
| dimension  | fixe                   | variable |
| 帧率  | fixe | variable[^3]                           |

[^1]: 具体引擎实现可能和计划不同。
[^2]: format conteneur : .avi, .xvid .mov 其中集合了多种媒体。
[^3]: 一帧可以持续更长时间。

#### trame I, P, B

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/7/7b/IBBPBB_inter_frame_group_of_pictures.svg/1920px-IBBPBB_inter_frame_group_of_pictures.svg.png" alt="wi" style="zoom:50%;" />

I 关键帧；P 考虑“过去”的连续帧；B bidirectionnelle - 考虑“过去”和“未来”的连续帧。

例子：云游戏考虑到实时性，不使用未来帧信息。

#### sprite: u, v

精灵图具体使用部分部分的坐标。

#### sprite métadonnées

dimension sprites

animation (e.g. "idle")

- boucler
- sprites
  - [u, v][####sprite: u, v]
  - durée
- transitions

----

- "ligne de base" 精灵图位置的参考点
- dimension logique - 不让人物卡在墙内。额外的“碰撞块”。
- 额外的参考点以便额外特效：如“手”-可以操作工具、“烟囱”可以加烟雾特效。

## animations vectorielles

- points
  - position
  - couleur
  - rayon
- segments
  - extrémités
  - épaisseur
  - couleur
  - dégradé ?
  - continuité 虚实线
- courbes
  - point de contrôle
- forme fermée
  - côtés (segments)
  - texture

### interpolation

```diff
+ position
+ couleur
+ rayon
- extrémité
+ épaisseur
+ couleur
```

continue vs. discrète

再一次提到了之前的颜色过渡例子：RGB 不如 TSL。

"Le choix de fonction d'interpolation a un impact."

### 人物骨架？

有个中心点$M_0$ 之后其它点呈继承关系。
$$
\begin{array}{CCL}
M_0 & = & M_{Rotation_0} \ M_{translation_0} \\
M_1 & = & M_{Rotation_1} \ M_{translation_1} \ M_0 \\
M_2 & = & M_{Rotation_2} \ M_{translation_2} \ M_1
\end{array}
$$

### 权重

```c++
Vec4 pos = (in.pos * os[in.pos1] * in.pond1
         +  in.pos * os[in.pos2] * (1 - in.pond1));
out.pos = mul(pos, MVP);
```

计算骨架，之后通过骨架计算物理。
