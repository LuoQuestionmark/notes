# Principes des moteurs de jeux

## 系统的拓扑结构

电源－显示－显卡－主板－CPU和内存－输入

- alimentation : AC / DC, A
- écran : résolution, ratio, définition, fréquence, couleur, balayage(?)
- cable : HDMI, DP, VGA, SCART, WIFI, COAX
- carte graphique : NVIDIA, AMD, INTEL, etc.
- PCI-E, PCI, AGI, thunder bolt, etc.
- RAM : DDRAM
- CPU : x64, ARM, MIPS(?), POWERPC, SPARC
- API : D3D, OpenGL, Vulkan DDRAM, Metal

----

### 硬件对游戏的影响

例子一：某个游戏欧版美版刷新率不同、人物速度不同以补偿。

例子二：虚幻竞技场最低配置->最高帧率。

例子三：数字或模拟传输。数字：部分错误＝全部错误；颜色精度受限于位数。模拟：信号反射（电磁学）。

例子四：

| Windows         | Mac   | Linux      | PS4  | XBox | Switch |
| --------------- | ----- | ---------- | ---- | ---- | ------ |
| OpenGL, VK, D3D | Metal | OpenGL, VK | VK   | D3D  | VK     |

----

## 色彩

- 红橙黄绿青蓝紫红外紫外

- 纯色和组合色：“没有粉紫色的激光”

- 不同视锥细胞对不同频率的敏感性
  结果：用“并非完全正确”的频率直接刺激对应的视锥细胞
- 四色印刷
- 从红色到绿色的过渡

|      | R     | $\to$  | V       |
| ---- | ----- | ------ | ------- |
| R    | 100%  | 50%    | 100%    |
| V    | 0%    | 50%    | 100%    |
| B    | 0     | 0      | 0       |
|      |       |        |         |
| T    | 0 deg | 60 deg | 120 deg |
| S    | 100%  | 100%   | 100%    |
| V    | 50%   | 50%    | 50%     |

TSV：色相饱和度亮度。此处优于RGB，因为中间黄色的亮度不同。

- 像素点
  - 三角形排列
  - RGB
  - BGR
  - 七巧板（双倍绿色双倍快乐）
  - https://en.wikipedia.org/wiki/Pixel_geometry
  - 四色（那个夏普广告）

### 亮度计算,或信号传输

$L = \frac{R + G + B}{3}$ 或 $R \times 0.2 + V \times 0.7 + B \times 0.1$

|      | 16bits | 8 bits | 8 bits |
| ---- | ------ | ------ | ------ |
| R    | 5      | 3      | 4      |
| V    | 6      | 3      | 2      |
| B    | 5      | 2      | 2      |

颜色准确性和分辨率。

## 3D 画图（？）

```c++
// 第一代
glBegin(GL_TRIANGLE);
glVertex3F(1.0f, 10.0f, 7.0f);
...
glEnd();
```

```c++
// 第二代：放在内存（缓存？）里面
int table = glGeneList(1);
glBeginList(table);
...
glEndList();

glTranslate(10, 30, 30);
glCallList(table);
```

```c++
// 第三代：直接访问内存
// VBO : 1, 10, 3, 7, 14, 6, 8, ...
//       \   |  /  \   |  /
//        triangle  triangle

glDrawElements(VBO, index, 17);
```

### pipeline d'affichage

"input assembly" $\to$ VS (vertex shader) $\to$ Appliquer matrices MUP

​					$\downarrow$ pixels à rendre

​					FS (fragment shader) $\to$ Couleur du fragment (pixel)

----

"input assembly" $\to$ VS (vertex shader)

​					$\downarrow$						$\searrow$

​					GS (geometry shader[^1])	TS (triangulation[^2])

​					$\downarrow$							$\downarrow$

​					FS						DS（调整上一步）

----

*去码头整点代码*

```c++
// VBO
struct {
	float x, y, z;
	float u, v;
	int temp;
};
```

```c++
// VS
struct in {
	Vec3 pos, sv_position;
    Vec2 uv;
    int temp;
}

Matrix44 MUP;
Sampler2D nuage;
```

```c++
struct V2F {
	Vec3 pos;
	Vec2 uv;
};

V2F vect(vin in) {
    V2F out;
    out.pos = mul(in.pos, MUP);
    out.uv = in.uv;
    return out;
}
```

```c++
// FS
Vec4 Frag(V2F in) {
	Vec4 col  tex2D(nuage, in.uv);
	float l = col.r * 0.2 + col.g * 0.7 + col.b * 0.1;
    return Vec4(l, l, l, col.a);
} 
```

----

[^1]: 点到多边形。
[^2]: 大切小。

----

![](/home/wluo/Documents/CS-ca/note-img.png)

1d : tableau de valeurs

2d : texture 2D

3d : cube

----

1 canal: 32bits entier

2 canaux : floattants

3 canaux : + transparance ....