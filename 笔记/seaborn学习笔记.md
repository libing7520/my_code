# Seaborn 数据可视化学习笔记

> 基于 seaborn 实验文件夹整理 | 从基础语法到高级进阶
  
---

## 目录

- [第一章 基础语法与环境配置](#第一章-基础语法与环境配置)
  - [1.1 导入 Seaborn 库](#11-导入-seaborn-库)
  - [1.2 加载内置数据集](#12-加载内置数据集)
  - [1.3 设置图表风格](#13-设置图表风格)
  - [1.4 调色板配置](#14-调色板配置)
- [第二章 关系型图表](#第二章-关系型图表)
  - [2.1 散点图](#21-散点图)
  - [2.2 折线图](#22-折线图)
  - [2.3 通用关系图函数](#23-通用关系图函数)
- [第三章 分布型图表](#第三章-分布型图表)
  - [3.1 直方图](#31-直方图)
  - [3.2 核密度图](#32-核密度图)
- [第四章 分类图表](#第四章-分类图表)
  - [4.1 条形图](#41-条形图)
  - [4.2 计数图](#42-计数图)
  - [4.3 盒图（箱线图）](#43-盒图箱线图)
  - [4.4 小提琴图](#44-小提琴图)
  - [4.5 分类散点图](#45-分类散点图)
  - [4.6 点图](#46-点图)
  - [4.7 通用分类图函数](#47-通用分类图函数)
- [第五章 高级进阶](#第五章-高级进阶)
  - [5.1 回归图](#51-回归图)
  - [5.2 热力图](#52-热力图)
  - [5.3 联合图](#53-联合图)
  - [5.4 成对绘图](#54-成对绘图)
  - [5.5 子图布局](#55-子图布局)
  - [5.6 常用参数速查](#56-常用参数速查)

---

## 第一章 基础语法与环境配置

### 1.1 导入 Seaborn 库

Seaborn 是基于 Matplotlib 的高级可视化库，通常配合使用：

```python
import seaborn as sns
from matplotlib import pyplot as plt
```

- `plt.show()`：显示图表（每个绘图代码后必须调用）。

### 1.2 加载内置数据集

Seaborn 内置了多个经典数据集，方便练习使用。

| 函数 | 用途 |
|------|------|
| `sns.load_dataset('tips')` | 加载内置数据集，返回 pandas DataFrame |
| `sns.get_data_home()` | 查看数据集的本地缓存路径 |

**常用内置数据集：**
- `tips` — 餐厅小费数据（244行×7列）：total_bill, tip, sex, smoker, day, time, size
- `flights` — 航班乘客数据（时间序列）

示例代码：

```python
tip = sns.load_dataset('tips')
print(tip.head())
```

### 1.3 设置图表风格

**`sns.axes_style()`** — 设置 Axes 的样式风格。

Seaborn 提供了 5 种预设风格：`darkgrid`、`whitegrid`、`dark`、`white`、`ticks`。

有两种使用方式：

- **临时设置**（上下文管理器）：

  ```python
  with sns.axes_style('white'):
      plt.plot([1, 2, 3], [4, 5, 6])
      plt.show()
  ```

- **全局设置**：

  ```python
  sns.set_style('whitegrid')
  ```

### 1.4 调色板配置

**`sns.color_palette()`** — 返回一组颜色的 RGB 值列表，控制图表的配色方案。

| 参数 / 用法 | 说明 |
|-------------|------|
| `sns.color_palette()` | 返回默认调色板（10 色） |
| `sns.color_palette("deep")` | deep 主题，色调深沉、饱和度高 |
| `sns.color_palette("muted")` | muted 主题，色调柔和 |
| `sns.color_palette("bright")` | bright 主题，色调鲜亮 |
| `sns.color_palette("bright", 9)` | 第二个参数指定颜色数量（如 9 色） |

**在图表中使用调色板颜色：**

```python
plt.plot([1, 2, 3], color=sns.color_palette("deep")[3])
plt.bar([1, 2, 3], [1, 2, 3], color=sns.color_palette("muted"))
```

---

## 第二章 关系型图表

关系型图表用于展示两个数值变量之间的关系。

### 2.1 散点图

**`sns.scatterplot()`** — 绘制散点图，显示两个连续变量之间的关系。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | x 轴数据列名 |
| `y` | y 轴数据列名 |
| `data` | 数据来源 DataFrame |
| `hue` | 按某列的类别分组着色 |
| `size` | 按某列的数值大小控制点的大小 |
| `style` | 按某列的类别分组控制点样式 |

示例代码：

```python
tip = sns.load_dataset('tips')
sns.scatterplot(x='total_bill', y='tip', data=tip)
plt.show()
```

### 2.2 折线图

**`sns.lineplot()`** — 绘制折线图，适合展示趋势变化。

核心参数与 `scatterplot` 基本一致。

示例代码：

```python
sns.lineplot(x='total_bill', y='tip', data=tip)
plt.show()
```

### 2.3 通用关系图函数

**`sns.relplot()`** — 关系图的高级封装函数，是 `scatterplot` 和 `lineplot` 的图级别（figure-level）接口。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `kind` | 图表类型，`'scatter'`（默认，散点图）或 `'line'`（折线图） |
| `col` | 按某列分面，生成多个子图（列方向） |
| `row` | 按某列分面，生成多个子图（行方向） |
| `hue` | 分组着色 |
| `x` / `y` | 数据列 |
| `data` | 数据来源 |

示例代码：

```python
# 按性别分列显示折线图，按是否吸烟着色
sns.relplot(x='total_bill', y='tip', data=tip, kind='line', col='sex', hue='smoker')
plt.show()
```

> **`scatterplot` / `lineplot` vs `relplot`：**
>
> - `scatterplot` 和 `lineplot` 是**轴级别（axes-level）**函数，在单个子图上绘制
> - `relplot` 是**图级别（figure-level）**函数，支持 `col`/`row` 分面，适合创建多子图布局

---

## 第三章 分布型图表

分布型图表用于展示数据的分布特征。

### 3.1 直方图

Seaborn 提供两个直方图函数：

| 函数 | 级别 | 说明 |
|------|------|------|
| `sns.histplot()` | 轴级别 | 单图直方图 |
| `sns.displot()` | 图级别 | 支持分面的直方图 |

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | 数据列 |
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `kde` | 是否叠加核密度估计曲线（`True`/`False`） |
| `multiple` | 多组显示方式：`'layer'`（层叠）、`'dodge'`（并列）、`'stack'`（堆叠）、`'fill'`（百分比堆叠） |
| `color` | 统一颜色（如 `'skyblue'`） |
| `edgecolor` | 边框颜色（如 `'black'`） |
| `linewidth` | 边框线宽 |
| `col` | `displot` 专用，按类分面 |

示例代码：

```python
# 基础直方图
sns.displot(data=tip, x='total_bill')

# 带核密度曲线的并列直方图
sns.displot(data=tip, x='total_bill', hue='sex', kde=True, multiple='dodge',
            color='skyblue', edgecolor='black', linewidth=1)

# 按 time（午餐/晚餐）分面
sns.displot(data=tip, x='total_bill', hue='sex', kde=True, multiple='dodge',
            color='skyblue', edgecolor='black', linewidth=1, col='time')
```

### 3.2 核密度图

**`sns.kdeplot()`** — 绘制核密度估计图，展示数据分布的平滑曲线。

可以绘制**一维**核密度（单变量）或**二维**核密度（双变量等高线/填充图）。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | x 轴数据 |
| `y` | y 轴数据（指定则绘制二维核密度） |
| `data` | 数据来源 |
| `hue` | 分组 |
| `fill` | 是否填充区域 |
| `multiple` | 多组显示方式：`'layer'`、`'stack'`、`'fill'` |
| `alpha` | 透明度 |

也可通过 `displot` 配合 `kind='kde'` 实现分面核密度图。

示例代码：

```python
# 二维核密度图（同时指定 x 和 y）
sns.kdeplot(data=tips, x='total_bill', y='tip', hue='time',
            fill=True, multiple='stack', alpha=0.5)
plt.show()

# 通过 displot 分面绘制
sns.displot(data=tips, x='total_bill', y='tip', col='time',
            kind='kde', fill=True, alpha=0.5)
plt.show()
```

---

## 第四章 分类图表

分类图表用于展示分类变量与数值变量之间的关系。本章函数均可通过 `hue`、`col`、`row` 等参数进行分组和分面。

### 4.1 条形图

**`sns.barplot()`** — 柱状条形图，默认显示均值及置信区间（误差线）。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | 分类变量（x 轴） |
| `y` | 数值变量（y 轴） |
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `color` | 指定颜色 |

示例代码：

```python
sns.barplot(x='day', y='total_bill', data=sns.load_dataset('tips'))
sns.barplot(x='day', y='tip', data=sns.load_dataset('tips'), hue='sex', color='salmon')
```

### 4.2 计数图

**`sns.countplot()`** — 统计每个类别的出现频次并绘制条形图。

| 参数 | 说明 |
|------|------|
| `x` | 分类列 |
| `data` | 数据来源 |

示例代码：

```python
sns.countplot(x='day', data=sns.load_dataset('tips'))
```

### 4.3 盒图（箱线图）

**`sns.boxplot()`** — 绘制箱线图，展示数据的五数概括（最小值、Q1、中位数、Q3、最大值）及离群点。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | 分类变量 |
| `y` | 数值变量 |
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `fill` | 是否填充（`True`/`False`） |

示例代码：

```python
tips = sns.load_dataset('tips')

# 基础盒图
sns.boxplot(x='day', y='total_bill', data=tips)
plt.show()

# 带分组色、不填充
sns.boxplot(x='day', y='total_bill', data=tips, hue='sex', fill=False)
```

### 4.4 小提琴图

**`sns.violinplot()`** — 小提琴图结合了箱线图和核密度估计，同时展示数据的分布形状和统计摘要。

示例代码：

```python
sns.violinplot(x='day', y='total_bill', data=tips)
```

> **盒图 vs 小提琴图：** 盒图简洁、强调统计量；小提琴图丰富、展示完整分布形态。

### 4.5 分类散点图

Seaborn 提供两种分类散点图：

| 函数 | 说明 |
|------|------|
| `sns.stripplot()` | 分类散点图，数据点沿分类轴分布，可能重叠 |
| `sns.swarmplot()` | 蜂群图，数据点自动分散排列，避免重叠 |

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | 分类变量 |
| `y` | 数值变量 |
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `dodge` | 分组时是否分开排列（`True`/`False`） |

示例代码：

```python
# stripplot
sns.stripplot(x='day', y='total_bill', data=tip)

# stripplot 分组
sns.stripplot(x='day', y='total_bill', data=tip, hue='sex', dodge=True)

# swarmplot 分组
sns.swarmplot(x='day', y='total_bill', data=tip, hue='sex', dodge=True)
```

### 4.6 点图

**`sns.pointplot()`** — 绘制点估计及置信区间，并用连线连接同一分组的点，适合展示趋势。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` | 分类变量 |
| `y` | 数值变量 |
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `markers` | 分组标记样式，如 `['o', 'x']` |
| `linestyles` | 分组线型样式，如 `['-', '--']` |
| `dodge` | 分组间距 |

示例代码：

```python
sns.pointplot(x='day', y='total_bill', data=tips, hue='sex',
              markers=['o', 'x'], linestyles=['-', '--'], dodge=0.3)
plt.show()
```

> **`hue='sex'`** 表示按性别分组；`markers=['o','x']` 表示男性用圆点，女性用叉号；`linestyles=['-','--']` 表示男性用实线，女性用虚线；`dodge=0.3` 表示分组之间的间距。

### 4.7 通用分类图函数

**`sns.catplot()`** — 分类图的高级封装，是图级别函数，通过 `kind` 参数切换图表类型。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `kind` | 图表类型：`'bar'`、`'count'`、`'box'`、`'violin'`、`'strip'`、`'swarm'`、`'point'` |
| `col` / `row` | 分面变量 |
| 其他 | 透传对应底层函数的参数 |

示例代码：

```python
# 条形图（图级别）
sns.catplot(x='day', y='total_bill', data=sns.load_dataset('tips'), kind='bar')

# 点图（带分面）
sns.catplot(x='day', y='total_bill', data=tips, hue='sex', kind='point',
            markers=['o', 'x'], linestyles=['-', '--'], dodge=0.3, col='smoker')
plt.show()
```

---

## 第五章 高级进阶

### 5.1 回归图

**`sns.lmplot()`** — 绘制散点图并叠加线性回归拟合线，同时展示置信区间。

**核心参数：**

| 参数 | 说明 |
|------|------|
| `x` / `y` | 数据列 |
| `data` | 数据来源 |
| `scatter_kws` | 散点样式字典，如 `{"s": 30, "color": "g", "alpha": 0.5}` |
| `line_kws` | 回归线样式字典，如 `{"color": "r", "alpha": 0.8}` |
| `lowess` | 是否使用局部加权回归（`True`/`False`） |
| `robust` | 是否使用稳健回归（`True`/`False`） |

示例代码：

```python
sns.lmplot(x='total_bill', y='tip', data=tips,
           scatter_kws={"s": 30, "color": "g", "alpha": 0.5},
           line_kws={"color": "r", "alpha": 0.8})
plt.title("回归图")
plt.show()
```

### 5.2 热力图

**`sns.heatmap()`** — 用颜色矩阵展示数据的大小关系，适合展示矩阵或交叉表数据。

**数据准备：** 通常需要先用 `pivot` 将数据透视为矩阵形式：
```python
data = flights.pivot(index='month', columns='year', values='passengers')
```

**核心参数：**

| 参数 | 说明 |
|------|------|
| `data` | 二维数据矩阵 |
| `annot` | 是否在单元格中显示数值（`True`/`False`） |
| `fmt` | 数值格式，如 `'d'` 表示整数，`'.1f'` 表示一位小数 |
| `cmap` | 颜色映射，如 `'Reds'`、`'Blues'`、`'coolwarm'` 等 |
| `cbar` | 是否显示颜色条（`True`/`False`） |
| `vmin` / `vmax` | 颜色映射的最小/最大值范围 |
| `linewidths` | 单元格之间的线宽 |
| `linecolor` | 单元格之间的线颜色 |

示例代码：

```python
flights = sns.load_dataset('flights')
data = flights.pivot(index='month', columns='year', values='passengers')
sns.heatmap(data, annot=True, fmt='d', cmap='Reds', cbar=True,
            vmin=100, vmax=600, linewidths=0.5, linecolor='white')
plt.show()
```

### 5.3 联合图

**`sns.jointplot()`** — 同时展示双变量关系图和两个单变量分布图，是"三合一"复合图表。

| 参数 | 说明 |
|------|------|
| `x` / `y` | 数据列 |
| `data` | 数据来源 |
| `kind` | 中心图类型：`'scatter'`（散点，默认）、`'reg'`（回归）、`'kde'`（核密度）、`'hist'`（直方图）、`'hex'`（六边形分箱） |

> 图表结构：中心是双变量图（如散点图），上下边缘分别是 x 和 y 的单变量分布图。

示例代码：

```python
sns.jointplot(x='total_bill', y='tip', data=tips, kind='reg')
plt.show()
```

### 5.4 成对绘图

**`sns.pairplot()`** — 对 DataFrame 中所有数值列两两配对绘制散点图矩阵，对角线显示单变量分布。

| 参数 | 说明 |
|------|------|
| `data` | 数据来源 |
| `hue` | 分组着色 |
| `diag_kind` | 对角线图表类型：`'auto'`、`'hist'`（直方图）、`'kde'`（核密度） |

> 这是**探索性数据分析（EDA）**中非常有用的工具，可以快速发现变量之间的关系。

示例代码：

```python
sns.pairplot(tips)
plt.show()
```

### 5.5 子图布局

使用 Matplotlib 的 `plt.subplot()` 创建子图，再将 Seaborn 图表绘制到指定子图上。

| 函数 | 用途 |
|------|------|
| `plt.subplot(rows, cols, index)` | 创建子图网格并选择位置 |
| `ax` 参数 | 将 Seaborn 图表绘制到指定的 Axes 对象上 |

示例代码：

```python
ax1 = plt.subplot(1, 2, 1)
sns.scatterplot(x='total_bill', y='tip', data=tips, ax=ax1)

ax2 = plt.subplot(1, 2, 2)
sns.scatterplot(x='total_bill', y='tip', data=tips, ax=ax2)

plt.show()
```

> 大部分 Seaborn **轴级别**函数都支持 `ax` 参数，可以灵活地嵌入到自定义布局中。

### 5.6 常用参数速查

下表汇总了贯穿所有图表函数的通用参数：

| 参数 | 说明 | 适用函数 |
|------|------|----------|
| `x` / `y` | 指定数据列 | 通用 |
| `data` | 数据来源 DataFrame | 通用 |
| `hue` | 按类别分组着色 | 通用 |
| `col` / `row` | 按类别分面（多子图） | `relplot`、`displot`、`catplot` |
| `kind` | 子图类型 | `relplot`、`catplot`、`jointplot` |
| `palette` | 调色板名称 | 通用 |
| `alpha` | 透明度（0~1） | 通用 |
| `size` | 点大小 / 线宽 | `scatterplot`、`lineplot` |
| `style` | 分组样式 | `scatterplot`、`lineplot` |
| `multiple` | 多组分布显示方式 | `histplot`、`kdeplot` |
| `ax` | 指定目标 Axes 对象 | 轴级别函数 |

---

## 附录：函数分类总览

### 按级别分类

**轴级别函数（axes-level，可使用 `ax` 参数嵌入子图）：**

`scatterplot`、`lineplot`、`histplot`、`kdeplot`、`barplot`、`countplot`、`boxplot`、`violinplot`、`stripplot`、`swarmplot`、`pointplot`、`heatmap`

**图级别函数（figure-level，支持 `col`/`row` 分面）：**

`relplot`、`displot`、`catplot`、`lmplot`、`jointplot`、`pairplot`

### 按图表类型分类

| 类型 | 轴级别函数 | 图级别函数 |
|------|-----------|-----------|
| 关系图 | `scatterplot`、`lineplot` | `relplot` |
| 分布图 | `histplot`、`kdeplot` | `displot` |
| 分类图 | `barplot`、`countplot`、`boxplot`、`violinplot`、`stripplot`、`swarmplot`、`pointplot` | `catplot` |
| 回归图 | — | `lmplot` |
| 矩阵图 | `heatmap` | — |
| 复合图 | — | `jointplot`、`pairplot` |

---

> 以上笔记基于 seaborn 文件夹中的 17 个实验文件整理，涵盖了从数据加载、风格配置到各类图表绘制的完整学习路径。建议配合实际的 Jupyter Notebook 实验进行复习和练习。