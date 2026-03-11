# 几何命题语法指南

## 概述

本项目定义了一套用于几何推理的形式化语言,包括几何谓词(谓词)、几何构造(构造)和演绎规则。本指南将帮助你理解如何编写符合本项目规范的几何命题。
如有任何不理解的地方,请参照alphageometry的几何命题.
(https://github.com/google-deepmind/alphageometry)
我们目前不支持坐标与部分构造谓词.所有支持的语法都已在下面列出.

---

## 一、基础元素

### 1.1 点(Point)

点是几何命题的基本元素,使用单字母表示:

- **小写字母**: `a, b, c, d, e, ...`
- **大写字母**: `A, B, C, D, E, ...`

> 示例: `A`, `B`, `C`, `M`, `O` 等都是合法的点名称

### 1.2 命题(Proposition)格式

命题是描述几何关系的基本语句,格式为:

```
谓词 参数1 参数2 ... 参数N
```

- **谓词**: 表示几何关系的关键字(如共线、垂直、平行等)
- **参数**: 通常是点,有些谓词需要更多参数

---

## 二、几何谓词(Predicates)

### 2.1 基本关系

| 谓词 | 参数数量 | 说明 | 示例 |
|------|---------|------|------|
| `coll` | 3 | 共线: 三点共线 | `coll A B C` 表示 A, B, C 三点共线 |
| `para` | 4 | 平行: 两直线平行 | `para A B C D` 表示 AB 平行于 CD |
| `perp` | 4 | 垂直: 两直线垂直 | `perp A B C D` 表示 AB 垂直于 CD |
| `cong` | 4 | 全等: 线段长度相等 | `cong A B C D` 表示 AB = CD |
| `midp` | 3 | 中点: 点是线段中点 | `midp M A B` 表示 M 是 AB 的中点 |
| `cyclic` | 4 | 共圆: 四点共圆 | `cyclic A B C D` 表示 A, B, C, D 四点共圆 |
| `circle` | 4 | 圆: 定义圆心 | `circle O A B C` 表示 O 是过 A, B, C 的圆心 |

### 2.2 角度关系

| 谓词 | 参数数量 | 说明 |
|------|---------|------|
| `eqangle` | 8 | 等角: 八点等角 |
| `eqangle6` | 6 | 六点等角 |
| `eqangle3` | 3 | 三点等角 |
| `eqangle2` | 4 | 二点等角 |

### 2.3 比例关系

| 谓词 | 参数数量 | 说明 |
|------|---------|------|
| `eqratio` | 8 | 等比: 八点等比 |
| `eqratio6` | 6 | 六点等比 |
| `eqratio3` | 3 | 三点等比 |

### 2.4 否定关系

| 谓词 | 参数数量 | 说明 |
|------|---------|------|
| `ncoll` | 3 | 不共线 |
| `npara` | 4 | 不平行 |
| `nperp` | 4 | 不垂直 |
| `diff` | 2 | 不同点(两点不重合) |

### 2.5 三角形关系

| 谓词 | 参数数量 | 说明 |
|------|---------|------|
| `contri` | 6 | 全等三角形 |
| `contri2` | 6 | 全等三角形2 |
| `simtri` | 6 | 相似三角形 |
| `simtri2` | 6 | 相似三角形2 |
| `contri*` | 6 | 全等三角形* |
| `simtri*` | 6 | 相似三角形* |

---

## 三、几何构造(Constructions)

构造用于定义几何图形,格式为:

```
输出点 = 构造名称 输入点
```

### 3.1 基础构造

| 构造名称 | 格式 | 说明 |
|---------|------|------|
| `free` | `a = free` | 创建自由点 A |
| `segment` | `a b = segment` | 创建线段 AB |
| `triangle` | `a b c = triangle` | 创建三角形 ABC |

### 3.2 点构造

| 构造名称 | 格式 | 说明 |
|---------|------|------|
| `midpoint` | `m = midpoint a b` | M 是 AB 的中点 |
| `foot` | `x = foot a b c` | X 是 A 到 BC 的垂足 |
| `on_line` | `x = on_line a b` | X 在直线 AB 上 |
| `on_tline` | `x = on_tline a b c` | X 在过 A 垂直于 BC 的直线上 |
| `on_pline` | `x = on_pline a b c` | X 在过 A 平行于 BC 的直线上 |
| `on_circle` | `x = on_circle o a` | X 在以 O 为圆心过 A 的圆上 |
| `on_circum` | `x = on_circum a b c` | X 在三角形 ABC 的外接圆上 |
| `intersection_ll` | `x = intersection_ll a b c d` | X 是直线 AB 和 CD 的交点 |
| `angle_bisector` | `x = angle_bisector a b c` | AX 是角 BAC 的角平分线 |

### 3.3 特殊点构造

| 构造名称 | 格式 | 说明 |
|---------|------|------|
| `orthocenter` | `h = orthocenter a b c` | H 是三角形 ABC 的垂心 |
| `circumcenter` | `o = circumcenter a b c` | O 是三角形 ABC 的外心 |
| `incenter` | `i = incenter a b c` | I 是三角形 ABC 的内心 |
| `centroid` | `g = centroid a b c` | G 是三角形 ABC 的重心 |

### 3.4 特殊三角形

| 构造名称 | 格式 | 说明 |
|---------|------|------|
| `r_triangle` | `a b c = r_triangle` | 直角三角形 ABC(A 为直角) |
| `iso_triangle` | `a b c = iso_triangle` | 等腰三角形 ABC |

### 3.5 四边形

| 构造名称 | 格式 | 说明 |
|---------|------|------|
| `parallelogram` | `a b c d = parallelogram` | 平行四边形 ABCD |
| `rectangle` | `a b c d = rectangle` | 矩形 ABCD |
| `square` | `a b c d = square` | 正方形 ABCD |
| `trapezoid` | `a b c d = trapezoid` | 梯形 ABCD |

---

## 四、完整问题格式

一个完整的几何问题由**构造列表**和**目标命题**组成,中间用 `?` 分隔:

```
构造1; 构造2; ... ? 目标命题
```

### 4.1 格式示例

```
# 简单示例
a b c = triangle ? midp m a b

# 多个构造
a b c = triangle; h = orthocenter h a b c ? perp h a b c

# 完整问题示例
a b c = triangle; m = midpoint m b c; n = midpoint n a c ? para m n a b
```

### 4.2 语法规则

1. **构造之间**: 用分号 `;` 分隔
2. **构造与目标**: 用问号 `?` 分隔
3. **每行结尾**: 不需要标点符号
4. **注释**: 使用 `#` 开头编写注释

---

## 五、命题列表格式

多个命题可以用逗号分隔:

```
coll A B C, perp A B C D, para A B C D
```

---

## 六、编写指南

### 6.1 编写命题的注意事项

1. **参数顺序**: 某些谓词(如 `coll`, `cyclic`)的参数顺序可以交换(系统会自动规范化),但大多数谓词(如 `perp`, `para`, `cong`)参数顺序有特定含义

2. **参数数量**: 必须严格遵守每个谓词的参数数量要求:
   - `coll` 需要 3 个点
   - `perp` 需要 4 个点(两条直线)
   - `midp` 需要 3 个点

3. **点命名**: 使用有意义的点名称,通常:
   - 大写字母表示主要点
   - 小写字母表示辅助点

### 6.2 编写构造的注意事项

1. **依赖关系**: 某些构造依赖于其他构造:
   - `midpoint` 依赖于 `triangle`
   - `on_circum` 依赖于 `triangle`
   - 编写时需要确保先有基础构造

2. **输入输出**: 
   - 左侧是输出点(新产生的点)
   - 右侧是构造名称和输入点

3. **构造条件**: 构造本身隐含了某些谓词:
   - `midpoint m a b` 隐含 `midp m a b`, `coll m a b`, `cong m a m b`

### 6.3 编写问题的建议

1. **从简单开始**: 先写基础构造,再逐步添加复杂构造

2. **明确目标**: 目标命题应该清晰明确

3. **检查可行性**: 确保构造能够推导出目标

---

## 七、示例

### 示例1: 证明中点与平行

**问题**:
```
a b c = triangle; m = midpoint m b c; n = midpoint n a c ? para m n a b
```

**解释**:
1. 构造三角形 ABC
2. M 是 BC 的中点
3. N 是 AC 的中点
4. **目标**: 证明 MN 平行于 AB

### 示例2: 证明垂心性质

**问题**:
```
a b c = triangle; h = orthocenter h a b c ? perp h a b c
```

**解释**:
1. 构造三角形 ABC
2. H 是三角形 ABC 的垂心
3. **目标**: 证明 AH 垂直于 BC

### 示例3: 证明圆的性质

**问题**:
```
a b c = triangle; o = circumcenter o a b c ? cong o a o b
```

**解释**:
1. 构造三角形 ABC
2. O 是三角形 ABC 的外心
3. **目标**: 证明 OA = OB(圆心到圆上任意点距离相等)

---
