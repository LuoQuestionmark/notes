# Principes des moteurs de jeux 4 : Texte & Régionalisation


## Encodage

comme ASCII, ISO 8859, GBK, utf-8.

### Unicode

各种语言符号、emoji。理论上可以有百万个符号。

utf-32 定长；

utf-8 变长代码。

```text
0xxxxxxx
10xxxxxx xxxxxxxx
110xxxxx xxxxxxxx xxxxxxxx
```

## Glyphe 字形

### Polices de caractères

- matricielle (bitmap) 位图 - 颜色（emoji）
- vectorielle 矢量图 - 占用空间较小

#### 游戏中的特殊字符

*“按下‘圆圈’继续”*

将一些字符替换：

```
§ <- "cercle"
print("push §")
```

#### 节省内存

只加载部分字符、分开内容（如字母和注音符号、部首（！））。

#### 一些细节

line de base, corps

> $1 \ pt = 1/72 \ pouce \approx 0.353 \ mm$

字间距离 crénage ([kerning](https://en.wikipedia.org/wiki/Kerning))

#### Rendu du text vectoriel

```python
# how to draw the peach color in the following graph
if (v > u ** 2):
	# noir
else:
	# white
```

![	](/home/wluo/Documents/CS-ca/notes/note-img4.svg)

## Régionlisation

- langue, dialectes
- sensibilité cultuelle, censure
- différence "sens"
- devises
- ZQSD/WASD
- sémiotique - PlayStation 的圈叉确定
- unité
- 读写顺序（左右、上下）[^1]
- 南北半球季节
- ……

[^1]: 微软测试日语德语翻译。

----

将设置放在`ini`文件中。

```ini
#! fr.ini
HELLO = Bonjour
PUB   = cafe.png
```

自定义显示。

```pseudocode
// fr: "Bonjour Bob, il fait -4C aujourdhui"
// en: "Hi Bob, it is 20F today"
// en-uk...

print("Hello {name}, it is {tmp:C} today")

// C: val
// F: val * 9 / 5 - 32
// cm: val
// m: val / 10
```

用散列表翻译。
