# Matplotlib 数据可视化学习笔记

> 基于 matplotlib 实验文件夹整理 | 从基础语法到高级进阶

---

## 目录

- [第一章 基础语法与环境配置](#第一章-基础语法与环境配置)
  - [1.1 导入 Matplotlib 库](#11-导入-matplotlib-库)
  - [1.2 绘制第一条折线图](#12-绘制第一条折线图)
  - [1.3 中文字体设置](#13-中文字体设置)
  - [1.4 设置图表风格](#14-设置图表风格)
- [第二章 图表元素与美化](#第二章-图表元素与美化)
  - [2.1 线条属性](#21-线条属性)
  - [2.2 图例](#22-图例)
  - [2.3 网格](#23-网格)
  - [2.4 文本标注](#24-文本标注)
  - [2.5 坐标轴定制](#25-坐标轴定制)
- [第三章 子图与多轴布局](#第三章-子图与多轴布局)
  - [3.1 子图布局](#31-子图布局)
  - [3.2 面向对象方式创建子图](#32-面向对象方式创建子图)
  - [3.3 双轴图](#33-双轴图)
- [第四章 基础图表类型](#第四章-基础图表类型)
  - [4.1 折线图](#41-折线图)
  - [4.2 散点图](#42-散点图)
  - [4.3 条形图](#43-条形图)
  - [4.4 直方图](#44-直方图)
  - [4.5 饼图](#45-饼图)
  - [4.6 箱线图](#46-箱线图)
- [第五章 高级进阶](#第五章-高级进阶)
  - [5.1 热力图](#51-热力图)
  - [5.2 3D 图表](#52-3d-图表)
  - [5.3 保存图表](#53-保存图表)
  - [5.4 常用参数速查](#54-常用参数速查)

---

## 第一章 基础语法与环境配置

### 1.1 导入 Matplotlib 库

Matplotlib 是 Python 最基础、最强大的数据可视化库，`pyplot` 模块提供了类似 MATLAB 的绘图 API。

```python
from matplotlib import pyplot as plt
import numpy as np
```

> **关键约定**：`plt` 是 `matplotlib.pyplot` 的通用别名，全社区统一使用。

### 1.2 绘制第一条折线图

**`plt.plot(x, y)`** — Matplotlib 最核心的绘图函数，用于绘制折线图。

```python
x = [1, 2, 3, 4, 5]
y = [2, 3, 4, 5, 6]
plt.plot(x, y)
plt.xlabel('x-axis')
plt.ylabel('y-axis')
plt.title('Line Graph')
plt.show()
```

**核心显示函数：**

| 函数 | 用途 |
|------|------|
| `plt.plot(x, y)` | 绘制折线图 |
| `plt.xlabel('标签')` | 设置 x 轴标签 |
| `plt.ylabel('标签')` | 设置 y 轴标签 |
| `plt.title('标题')` | 设置图表标题 |
| `plt.show()` | 显示图表（每个绘图代码后必须调用） |

### 1.3 中文字体设置

默认情况下 Matplotlib 不支持中文显示，需要手动设置字体。

**`plt.rcParams['font.sans-serif'] = ['SimHei']`** — 设置全局中文字体为黑体（SimHei）。

```python
plt.rcParams['font.sans-serif'] = ['SimHei']
```

> **注意**：此设置必须在绘图之前执行。其他可选字体包括 `'Microsoft YaHei'`（微软雅黑）、`'KaiTi'`（楷体）等。

### 1.4 设置图表风格

**`plt.style.use('style_name')`** — 切换 Matplotlib 内置的图表风格主题。

```python
plt.style.use('ggplot')  # 使用类似 R 语言 ggplot2 的风格
```

**常用内置风格：**

| 风格名称 | 说明 |
|----------|------|
| `'ggplot'` | 模仿 R 语言 ggplot2 风格，灰底白网格线 |
| `'seaborn-v0_8'` | Seaborn 风格，简洁美观 |
| `'fivethirtyeight'` | 模仿 FiveThirtyEight 网站风格 |
| `'dark_background'` | 深色背景风格 |
| `'classic'` | Matplotlib 经典默认风格 |

---

## 第二章 图表元素与美化

### 2.1 线条属性

在 `plt.plot()` 中可以通过参数自定义线条的**颜色**、**标记样式**和**线型**。

| 参数 | 说明 | 示例值 |
|------|------|--------|
| `color` | 线条颜色 | `'red'`、`'blue'`、`'#FF0000'` |
| `marker` | 数据点标记样式 | `'o'`（圆点）、`'s'`（方形）、`'^'`（三角） |
| `label` | 图例标签文字 | `'最高温度'` |

```python
days = [1, 2, 3, 4, 5, 6, 7]
max_temperatures = [22, 24, 19, 25, 27, 23, 26]
min_temperatures = [15, 17, 12, 18, 20, 16, 19]

plt.plot(days, max_temperatures, label='最高温度', marker='o')
plt.plot(days, min_temperatures, label='最低温度', marker='o')
```

### 2.2 图例

**`plt.legend()`** — 显示图例，使读者能够区分图表中的不同数据系列。

```python
plt.legend()
```

**`fig.legend()`** — 在图级别（Figure）添加图例，可通过 `loc` 和 `bbox_to_anchor` 精确控制位置。

```python
fig.legend(loc='upper left', bbox_to_anchor=(0.1, 0.9))
```

| `loc` 参数值 | 说明 |
|-------------|------|
| `'upper left'` | 左上角 |
| `'upper right'` | 右上角 |
| `'lower left'` | 左下角 |
| `'lower right'` | 右下角 |
| `'best'` | 自动选择最佳位置（默认） |

### 2.3 网格

**`plt.grid()`** — 为图表添加网格线，增强可读性。

```python
plt.grid()                              # 默认网格
plt.grid(axis='y', ls='--', c='r', alpha=0.8)  # 仅 y 轴、虚线、红色、透明度0.8
```

| 参数 | 说明 |
|------|------|
| `axis` | 网格方向：`'x'`、`'y'`、`'both'` |
| `ls` 或 `linestyle` | 线型：`'-'`（实线）、`'--'`（虚线）、`':'`（点线） |
| `c` 或 `color` | 网格线颜色 |
| `alpha` | 透明度，取值范围 0（全透明）~ 1（不透明） |

### 2.4 文本标注

**`ax.text(x, y, text, ...)`** — 在图表指定坐标位置添加文本标注，常用于标记数据点的具体数值。

```python
for i, temp in enumerate(max_temperatures):
    ax.text(days[i], temp + 0.5, f'{temp}°C', ha='center', va='bottom', fontsize=9, color='red')
```

| 参数 | 说明 |
|------|------|
| `x, y` | 文本放置的坐标位置 |
| `text` | 文本内容字符串 |
| `ha` | 水平对齐：`'center'`、`'left'`、`'right'` |
| `va` | 垂直对齐：`'center'`、`'top'`、`'bottom'` |
| `fontsize` | 字体大小 |
| `color` | 文字颜色 |

### 2.5 坐标轴定制

通过 Axes 对象的专用方法可以精细控制坐标轴的**刻度位置**、**刻度标签**和**样式**。

| 方法 | 用途 |
|------|------|
| `ax.set_xticks(positions)` | 设置 x 轴刻度位置 |
| `ax.set_xticklabels(labels)` | 设置 x 轴刻度标签文本 |
| `ax.tick_params(axis, labelrotation)` | 设置刻度标签旋转角度 |
| `ax.tick_params(axis, labelcolor)` | 设置刻度标签颜色 |

```python
x_names = ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
ax.set_xticks(days)                   # 设置刻度位置
ax.set_xticklabels(x_names)           # 替换为中文标签
ax.tick_params(axis='x', labelrotation=45)  # x轴标签旋转45°, 防止重叠
ax.tick_params(axis='y', labelcolor='red')  # y轴刻度颜色
```

---

## 第三章 子图与多轴布局

### 3.1 子图布局

**`plt.subplot(rows, cols, index)`** — 创建子图网格并选择当前位置（非面向对象方式）。

参数按顺序分别表示：**行数**、**列数**、**当前子图序号**。

```python
plt.subplot(1, 2, 1)  # 1行2列布局中的第1个子图
plt.plot(x, y1)
plt.title('Line Graph 1')

plt.subplot(1, 2, 2)  # 1行2列布局中的第2个子图
plt.plot(x, y2, color='orange')
plt.title('Line Graph 2')
plt.show()
```

### 3.2 面向对象方式创建子图

**`fig, ax = plt.subplots(figsize=(width, height))`** — 推荐使用此方式，返回 Figure 和 Axes 对象，便于后续精细控制。

```python
fig, ax = plt.subplots(figsize=(10, 5))  # 创建单个子图，宽10英寸，高5英寸
ax.plot(days, max_temperatures, label='最高温度', color='red', marker='o')
ax.set_xlabel('日期')
ax.set_ylabel('最高温度 (°C)', color='red')
```

> **两种方式的区别：**
>
> - `plt.subplot()` 是 **pyplot 方式**，适合快速绘制简单图表
> - `fig, ax = plt.subplots()` 是**面向对象方式**，适合精细控制每个图表元素

### 3.3 双轴图

**`ax2 = ax1.twinx()`** — 创建一个与 `ax1` 共享 x 轴但拥有独立 y 轴的新 Axes 对象。适用于在同一图中展示**量纲不同**的两组数据。

```python
fig, ax1 = plt.subplots(figsize=(10, 5))

# 左侧 y 轴：最高温度
ax1.plot(days, max_temperatures, label='最高温度', color='red', marker='o')
ax1.set_xlabel('日期')
ax1.set_ylabel('最高温度 (°C)', color='red')
ax1.tick_params(axis='y', labelcolor='red')

# 右侧 y 轴：最低温度
ax2 = ax1.twinx()
ax2.plot(days, min_temperatures, label='最低温度', color='blue', marker='o')
ax2.set_ylabel('最低温度 (°C)', color='blue')
ax2.tick_params(axis='y', labelcolor='blue')

fig.legend(loc='upper left', bbox_to_anchor=(0.1, 0.9))
plt.show()
```

> **`twinx()` vs 两个 `subplot`：** `twinx()` 是在同一位置叠加两个坐标轴，共享 x 轴，适合对比两组不同量级的数据；而 `subplot` 是并列放置多个独立的子图。

---

## 第四章 基础图表类型

### 4.1 折线图

**`plt.plot(x, y)`** — 用线段连接相邻数据点，适合展示数据的**变化趋势**。

```python
plt.plot(days, max_temperatures, label='最高温度', marker='o')
plt.xlabel('日期')
plt.ylabel('温度 (°C)')
plt.title('一周内的气温变化')
plt.legend()
plt.grid()
plt.show()
```

> **适用场景**：时间序列数据、函数曲线、趋势分析。

### 4.2 散点图

**`plt.scatter(x, y, color='color')`** — 用点表示两个数值变量之间的关系，适合展示数据的**分布和聚类**。

| 参数 | 说明 |
|------|------|
| `x` | x 轴数据数组 |
| `y` | y 轴数据数组 |
| `color` | 点的颜色 |
| `alpha` | 点的透明度 |
| `s` | 点的大小 |

```python
import numpy as np
data1 = np.random.randint(0, 100, 100)
data2 = np.random.randint(0, 100, 100)
plt.scatter(data1, data2, color='red')
plt.show()
```

> **适用场景**：相关性分析、聚类可视化、数据分布探索。

### 4.3 条形图

#### 4.3.1 垂直条形图

**`plt.bar(x, height)`** — 绘制垂直条形图，适合比较**不同类别的数据大小**。

```python
categories = ['A', 'B', 'C', 'D', 'E']
values = [10, 15, 7, 12, 20]
table_color = ['skyblue', 'orange', 'green', 'red', 'purple']

plt.bar(categories, values, color=table_color)
plt.title('条形图示例')
plt.grid(axis='y', ls='--', alpha=0.7)
plt.show()
```

#### 4.3.2 水平条形图

**`plt.barh(y, width)`** — 绘制水平条形图，与 `plt.bar` 类似但方向为水平。

```python
plt.barh(categories, values, color=table_color)
plt.legend()
plt.show()
```

#### 4.3.3 分组条形图

将多组数据并列放置，便于对比。

```python
species = ("苹果", "蓝莓", "橘子")
weight_counts = {
    "第1季度": [70, 39, 58],
    "第2季度": [82, 37, 66],
}
width = 0.2
x = range(len(species))
x1 = [_ + width for _ in x]

container = plt.bar(x, weight_counts["第1季度"], color='tab:red', label='第1季度', width=width)
plt.bar_label(container)   # 在柱子上显示数值
container2 = plt.bar(x1, weight_counts["第2季度"], color='tab:blue', label='第2季度', width=width)
plt.bar_label(container2)

plt.xticks([_ + width / 2 for _ in x], species)
plt.legend()
```

> **`plt.bar_label(container)`** — 自动在柱子上方（或指定位置）显示对应的数值。

#### 4.3.4 堆叠条形图

通过 `bottom` 参数将柱子堆叠在已有柱子上方。

```python
container = plt.bar(x, weight_counts["第1季度"], color='tab:red', label='第1季度')
plt.bar_label(container, label_type='center')

container2 = plt.bar(x, weight_counts["第2季度"], color='tab:blue', label='第2季度',
                     bottom=weight_counts["第1季度"])   # 堆叠在第一季度上方
plt.bar_label(container2, label_type='center')
```

| `label_type` 参数 | 说明 |
|-------------------|------|
| `'edge'` | 标签显示在柱子边缘（默认） |
| `'center'` | 标签显示在柱子中心 |

### 4.4 直方图

**`plt.hist(data, bins, edgecolor)`** — 将数据分组并统计各组的频数，用矩形高度表示频率分布。

| 参数 | 说明 |
|------|------|
| `data` | 原始数据数组 |
| `bins` | 分组数量（组数） |
| `edgecolor` | 柱子边缘颜色，常用于区分相邻柱子 |
| `color` | 柱子填充颜色 |
| `alpha` | 透明度 |

```python
data = np.random.randint(0, 100, size=1000)
plt.hist(data, bins=50, edgecolor='white')
plt.show()
```

> **适用场景**：查看数据分布形态（正态、偏态、双峰等）、识别异常值。

### 4.5 饼图

**`plt.pie(data, labels, explode, autopct)`** — 用扇形的大小表示各部分在总体中的占比。

| 参数 | 说明 |
|------|------|
| `data` | 各部分数值列表 |
| `labels` | 各部分标签 |
| `explode` | 扇形分离程度，列表长度与 data 相同 |
| `autopct` | 百分比显示格式，如 `'%1.1f%%'` 表示一位小数 |
| `colors` | 各部分颜色列表 |
| `shadow` | 是否添加阴影 |

```python
data = [10, 20, 30, 40]
explode = [0.1, 0.1, 0.1, 0.1]   # 各部分分离0.1半径
plt.pie(data,
        labels=['A', 'B', 'C', 'D'],
        explode=explode,
        autopct='%1.1f%%')
plt.title('饼图示例')
plt.show()
```

> **适用场景**：展示各部分占整体的比例关系，适合少量类别（3~7个）。

### 4.6 箱线图

**`plt.boxplot(data, labels)`** — 用箱体展示数据的**五数概括**（最小值、第一四分位数、中位数、第三四分位数、最大值）及离群点。

```python
data1 = np.random.randint(1, 100, size=100)
data2 = np.random.randint(1, 100, size=100)
data = [data1, data2]

plt.boxplot(data, labels=['1', '2'])
```

**箱线图解读：**

| 元素 | 含义 |
|------|------|
| 箱体 | 数据的中间 50%（从 Q1 到 Q3） |
| 箱内横线 | 中位数（50% 分位数） |
| 上下须线 | 正常数据范围（通常为 Q1-1.5×IQR 到 Q3+1.5×IQR） |
| 离群点 | 超出须线范围的异常值（显示为独立圆点） |

> **适用场景**：多组数据分布对比、异常值检测。

---

## 第五章 高级进阶

### 5.1 热力图

**`plt.imshow(data, cmap, interpolation)`** — 用颜色深浅表示矩阵中数值的大小关系，适合展示二维矩阵数据。

**`plt.colorbar()`** — 在图表旁添加颜色条（色阶对照表）。

| 参数 | 说明 |
|------|------|
| `data` | 二维数组/矩阵 |
| `cmap` | 颜色映射方案：`'hot'`、`'coolwarm'`、`'Blues'`、`'viridis'` 等 |
| `interpolation` | 插值方式：`'nearest'`（锐利边缘）、`'bilinear'`（平滑过渡） |

```python
days = ['Mon', 'Tue', 'Wed', 'Thu', 'Fri']
time = ['Morning', 'Afternoon', 'Evening']
data = np.random.rand(5, 3)

plt.imshow(data, cmap='hot', interpolation='nearest')
plt.xticks(np.arange(len(time)), time)
plt.yticks(np.arange(len(days)), days)
plt.colorbar()
plt.title('Heatmap Example')

# 在每个单元格内显示数值
for i in range(len(days)):
    for j in range(len(time)):
        plt.text(j, i, f'{data[i, j]:.2f}', ha='center', va='center', color='white')
plt.show()
```

> **`plt.text()` 在热力图中的作用**：在每个色块内标注具体数值，使图表既直观又精确。

### 5.2 3D 图表

创建 3D 图表需要使用 `projection='3d'` 参数将 Axes 设置为三维空间。

```python
fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
```

#### 5.2.1 3D 散点图

**`ax.scatter(x, y, z)`** — 在三维空间中绘制散点。

```python
x = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
y = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
z = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

fig = plt.figure()
ax = fig.add_subplot(111, projection='3d')
ax.scatter(x, y, z)
ax.set_xlabel('X Label')
ax.set_ylabel('Y Label')
ax.set_zlabel('Z Label')
plt.show()
```

#### 5.2.2 3D 条形图

**`ax.bar(x, y, zs, zdir, alpha, color)`** — 在三维空间中绘制条形图。

| 参数 | 说明 |
|------|------|
| `x, y` | 坐标位置 |
| `zs` | 柱子起始基准面的 z 坐标 |
| `zdir` | 柱子的延伸方向：`'x'`、`'y'`、`'z'` |

```python
ax.bar(x, y, zs=0, zdir='x', alpha=0.8, color='b')
```

### 5.3 保存图表

**`plt.savefig(filename, dpi)`** — 将当前图表保存为图像文件，支持 PNG、JPG、SVG、PDF 等格式。

| 参数 | 说明 |
|------|------|
| `filename` | 文件名（含扩展名），如 `'chart.png'` |
| `dpi` | 分辨率（每英寸点数），`300` 适合印刷，`100` 适合网页 |
| `bbox_inches` | `'tight'` 表示自动裁剪多余空白边缘 |
| `transparent` | `True` 可生成透明背景 |

```python
plt.savefig('temperature_plot.png', dpi=300)
```

> **注意**：`plt.savefig()` 必须在 `plt.show()` **之前**调用，否则保存的将是空白图像。

### 5.4 常用参数速查

下表汇总了贯穿所有图表函数的通用参数：

| 参数 | 说明 | 适用函数 |
|------|------|----------|
| `color` / `c` | 线条或填充颜色 | 通用 |
| `label` | 图例标签 | 通用（含 `plot`、`bar`、`scatter` 等） |
| `alpha` | 透明度（0~1） | 通用 |
| `marker` | 数据点标记样式 | `plot`、`scatter` |
| `linewidth` / `lw` | 线条宽度 | `plot` 及其衍生 |
| `linestyle` / `ls` | 线条样式 | `plot`、`grid` |
| `bins` | 分箱数 | `hist` |
| `cmap` | 颜色映射 | `imshow`、`scatter` |
| `figsize` | 图表尺寸（英寸） | `subplots`、`figure` |
| `dpi` | 分辨率 | `savefig`、`subplots` |

---

## 附录：函数分类总览

### 按功能分类

| 功能 | 核心函数 |
|------|----------|
| 基础绘图 | `plt.plot()`、`plt.scatter()` |
| 统计图表 | `plt.hist()`、`plt.boxplot()`、`plt.pie()` |
| 分类对比 | `plt.bar()`、`plt.barh()` |
| 矩阵可视化 | `plt.imshow()` + `plt.colorbar()` |
| 3D 图表 | `fig.add_subplot(111, projection='3d')` |
| 图表装饰 | `plt.xlabel()`、`plt.ylabel()`、`plt.title()`、`plt.legend()`、`plt.grid()` |
| 文本标注 | `ax.text()`、`plt.bar_label()` |
| 布局管理 | `plt.subplot()`、`plt.subplots()`、`ax.twinx()` |
| 样式设置 | `plt.style.use()`、`plt.rcParams` |
| 输出保存 | `plt.show()`、`plt.savefig()` |

### 按绘制方式分类

| 方式 | 函数 | 说明 |
|------|------|------|
| pyplot 方式（快速） | `plt.plot()`、`plt.bar()`、`plt.hist()` 等 | 自动管理 Figure 和 Axes，适合简单图表 |
| 面向对象方式（精细） | `fig, ax = plt.subplots()` + `ax.plot()` 等 | 可精确控制每个图表元素，推荐用于复杂图表 |

### 两大子图创建方式对比

| 特性 | `plt.subplot(rows, cols, idx)` | `fig, ax = plt.subplots()` |
|------|-------------------------------|---------------------------|
| 风格 | pyplot 状态机风格 | 面向对象风格 |
| 精细控制 | 较弱 | 强，每个子图都可独立操控 |
| 代码可读性 | 简单但子图多时混乱 | 清晰明了，推荐使用 |
| 推荐场景 | 1~2 个子图的简单布局 | 复杂多子图布局 |

---

> 以上笔记基于 matplotlib 文件夹中的 7 个实验文件整理，涵盖了从数据加载、图表绘制到美化和保存的完整学习路径。建议配合实际的 Jupyter Notebook 实验进行复习和练习。