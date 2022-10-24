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

![](/home/wluo/Documents/CS-ca/notes/note-img.png)

*d for dimension*

- 1d : tableau de valeurs

- 2d : texture 2D

- 3d : cube

- pas plus de 4 canaux.

----

1 canal: 32bits entier

2 canaux : floattants

3 canaux : + transparance ....

----

type de val

- $\mathbb{Z}$
- $\mathbb{R}$

précision : nb. bits

### fonction d'échantillonage (sampling)

*显示和模型之间的区别。*

将矩阵的数据映射到$[0, 1]^2$之间。Coordonnées u,v. (u, v, w for three dim.)

低于材质：采样-如选择左边最近的像素点；平均值。

高于材质：摩尔纹 https://zh.wikipedia.org/zh-cn/%E8%8E%AB%E5%88%97%E6%B3%A2%E7%B4%8B

### Optimisation

*接上文*

texture et couleur : 开发过程中运用不同的色彩探究是否使用了足够分辨率的材质。

----

不同信息：

- 景深
- 法线方向
- 反射效果
- Power (?)
- 2D 移动信息
- 颜色贴图 Albeto

----

### Appel de rendu

精灵图；所有的shade放在一张图上……

VBO: -soleil-arbre1-arbre2-…-

un seul appel de rendu.

----

----

## Optimisation

- CPU
  - threads
  - nb. instructions
- GPU
  - mémoire
  - complexité
  - nb. pixels
- RAM
  - quantité utilisée
  - nb. accès
- Stockage
  - temps accès
  - débit
- ~~E/S~~
- Réseau
  - latence
  - débit

----

例子：stockage 的 temps d'accès

由于磁盘的特性[^3]，顺序访问比乱序访问快。

[^3]: 机械硬盘

例子：stockage : débit de la (dé)compression

- LZMA

https://en.wikipedia.org/wiki/Lempel%E2%80%93Ziv%E2%80%93Markov_chain_algorithm

- LZ4

----

CPU: CPU framegraphes

CPU 算法：

| pile   | tas    |
| ------ | ------ |
| print  | string |
| struct | clss   |

CPU concat 操作

一次 join 操作嗯个优于多次+操作。

GC 垃圾处理

*“基于引用的”*

weakref *嗯这个我也知道*

```c#
weakRef img;
Image i = i.Target;
if (i == null) {
	i = Download(...);
	img.Target = i;
}
i.Display();
```

```c
// 脏字节
struct Vec2 {
	float x, y;
    // float len;
    // boolean dirty;
}

float genLen() {
    if (dirty) {
        len = sqrt(...);
        dirty = false;
    }
    return len;
}

Vec2 normalized() {
	float len = sqrt(pow(x,2) + pow(y,2));
	return Vec2{x * len, y * len};
}

```

```c++
// c++
auto * obj = new Objet();
delete(obj);
```

```pseudocode
// do it once per frame
// so when the next frame comes it won't be used
// actually pretty cool
struct Allocator {
	char buffer[64 Mo];
	int offset = 0;
	void * Alloc (int size) {
		char * ptr = buffer + offset;
		offset += size;
		return ptr;
	}
	void Free (void * ptr) {
		// empty
	}
	void Reset() {
		offset = 0;
	}
}
```

## Plugin & Middleware

插件：层次在“程序”之上

Middleware: 帮助程序构成（？）

### middleware example

+ `Speed Tree`，创造游戏中的树
+ `Havok`
+ `PhysiX`
+ `Wwise`

### compilateur

`.cpp`, `.h` -compilateur-> `.obj` -liaison-> `.exe`

连接：定位外部符号。

问题：若 middleware 不支持某个系统（如缺乏对应编译器），则无法使用编译的`.obj`文件，无法使用静态连接库。

### middleware which want to communicate directly with others

----

### plugin: 动态连接库

*当时做项目是王哲写的这部分*

comp -> liaison -> `.dll`

> Dependency Walker

```c++
HMODULE * malib = LoadLibrary("malib.dll");
using FnAType = void (*) (void);
FnAType FnA = (FnAType) GetProcAddr(malib, "FnA");
FnA();
```

问题：如果函数类型不对则存在堆被炸掉的可能性。

### QueryInterface

```c++
struct IUnknown {}

struct IPatate {
    void (*boil) (int temp);
    void (*frite) ();
    int (*good) (bool salt);
};
PATATE_UUID = ...;

QueryInterface(IUnknown ** i, UUID id) {
	if (id == PATATE_UUID) {
        IPatate* patate = (Ipatate*) *i;
        patate->boil = &BoilPatate;
        return true;
    }
    return false;
}

IPatate patate;
QueryInterface(&patate, PATATE_UUID)
```

## 一些关于工具自动化的思考

比方说做个热点图观察人死在哪了。
