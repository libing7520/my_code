Numpy 学习笔记
=================

目标
----
本笔记以清晰的逻辑框架组织 Numpy 的核心概念与常用操作，结合你提供的两个笔记本示例（`numpy学习代码.ipynb` 与 `numpy练习代码.ipynb`），给出简洁示例、常见陷阱与练习题，方便复习与在 PyCharm 中阅读/运行。

目录
----
- [1. 简介与安装](#1-intro-install)
  - [1.1 安装与环境配置（虚拟环境、pip、常用包）](#1-1-install-env)
  - [1.2 推荐工具（JupyterLab、PyCharm Professional/Community）](#1-2-tools)

- [2. ndarray：概念与属性](#2-ndarray)
  - [2.1 ndarray 概念与特点（同质性、维度）](#2-1-concept)
  - [2.2 常用属性（ndim、shape、size、dtype）](#2-2-attributes)
  - [2.3 示例与常见陷阱（类型提升、标量 vs 向量）](#2-3-traps)

- [3. ndarray 的创建方法](#3-creation)
  - [3.1 从 Python 容器（list/tuple）创建](#3-1-from-python)
  - [3.2 预定义数组（zeros/ones/empty/full/eye/diag）](#3-2-predefined)
  - [3.3 数值序列（arange/linspace/logspace）](#3-3-sequences)
  - [3.4 随机数组（rand/uniform/randint/randn）](#3-4-random)
  - [3.5 复制与视图（copy, view, reshape 与 内存共享）](#3-5-copy-view)

- [4. 索引与切片（含布尔索引与高级索引）](#4-index-slicing)
  - [4.1 一维索引与切片（基本语法、步长）](#4-1-1d)
  - [4.2 二维及多维索引（行列选择、切片组合）](#4-2-multid)
  - [4.3 布尔索引（单条件与多条件、逻辑运算）](#4-3-boolean)
  - [4.4 花式索引（整数数组索引、索引广播）](#4-4-fancy)
  - [4.5 常见错误及性能建议（避免逐元素循环）](#4-5-errors)

- [5. 常用运算（算术、广播、矩阵运算）](#5-ops)
  - [5.1 元素级算术运算（+ - * /）](#5-1-elementwise)
  - [5.2 广播规则与案例（形状配对规则、扩展维度）](#5-2-broadcast)
  - [5.3 矩阵与线性代数（@ 矩阵乘、np.dot、转置、逆）](#5-3-linear)

- [6. 常用函数与工具箱](#6-functions)
  - [6.1 数学函数（sqrt/exp/log/sin/cos/power/round/ceil/floor）](#6-1-math)
  - [6.2 统计函数（sum/mean/median/var/std/max/min/arg*）](#6-2-stats)
  - [6.3 累计与计数（cumsum/cumprod/count_nonzero）](#6-3-cumcount)
  - [6.4 比较与逻辑（greater/less/equal/logical_*）](#6-4-logic)
  - [6.5 条件选择（where/select）](#6-5-where)
  - [6.6 排序与集合（sort/argsort/unique/concatenate/split/reshape）](#6-6-sort)

- [7. 实战练习（逐题详解）](#7-exercises)
  - [7.1 气温统计（最大/最小/均值/超过阈值计数）](#7-1-temp)
  - [7.2 成绩处理（平均/方差/中位数/刻度转换）](#7-2-grades)
  - [7.3 矩阵运算练习（元素乘、矩阵乘、转置）](#7-3-matrix)
  - [7.4 随机数组练习（按列/按行统计、条件替换）](#7-4-random)
  - [7.5 进阶练习（分组统计、向量化实现、性能对比）](#7-5-advanced)

- [8. 在 PyCharm 中的实用技巧（Community / Professional）](#8-pycharm)
  - [8.1 在 PyCharm Professional 中打开并查看 Notebook（Jupyter 编辑器、Structure）](#8-1-prof)
  - [8.2 在 Community 版中的替代方案（nbconvert → script、#%% 单元、region）](#8-2-community)
  - [8.3 配置建议（解释器、插件、虚拟环境）](#8-3-config)

- [9. 常见问题与调试提示](#9-troubleshoot)
  - [9.1 导览/Structure 为空的排查步骤](#9-1-structure)
  - [9.2 nbconvert/环境问题的解决（缺少包、路径、编码）](#9-2-nbconvert)
  - [9.3 性能问题诊断（向量化、内存/数据转换代价）](#9-3-performance)

- [10. 后续学习建议](#10-next)
  - [10.1 深入广播规则与向量化技巧](#10-1-broadcast)
  - [10.2 学习 Pandas 与数据清洗流程](#10-2-pandas)
  - [10.3 可选进阶：SciPy、scikit-learn、numba、并行化](#10-3-advanced)

<a id="1-intro-install"></a>
1. 简介与安装
----------------
<a id="1-1-install-env"></a>
### 1.1 安装与环境配置（虚拟环境、pip、常用包）
- Numpy 是用于数值计算的核心库，主要数据结构是 ndarray（多维数组）。
- 安装：建议在项目虚拟环境中安装：

  pip install numpy jupyterlab notebook

### <a id="1-2-tools"></a>1.2 推荐工具（JupyterLab、PyCharm Professional/Community）
- 推荐使用 JupyterLab 进行交互式练习，或 PyCharm Professional 直接打开 `.ipynb`。

<a id="2-ndarray"></a>
2. ndarray：概念与属性
---------------------
<a id="2-1-concept"></a>
### <a id="2-1-concept"></a>2.1 概念
- ndarray：N 维数组，存储相同数据类型的元素（同质）。
- 维度（ndim）、形状（shape）、元素个数（size）、数据类型（dtype）。

<a id="2-2-attributes"></a>
### <a id="2-2-attributes"></a>2.2 常用属性示例
- arr.ndim  # 维度
- arr.shape # 形状
- arr.size  # 元素个数
- arr.dtype # 数据类型

示例：

import numpy as np
arr = np.array([[1,2,3],[4,5,6]])
print(arr.ndim, arr.shape, arr.size, arr.dtype)

<a id="2-3-traps"></a>
### <a id="2-3-traps"></a>2.3 示例与常见陷阱（类型提升、标量 vs 向量）
- 注意类型提升（mixed types 会提升为更通用的类型，例如字符串）。
- 标量与向量在索引与形状方面的行为不同。

<a id="3-creation"></a>
3. ndarray 的创建方法
---------------------
<a id="3-1-from-python"></a>
<a id="3-2-predefined"></a>
<a id="3-3-sequences"></a>
<a id="3-4-random"></a>
<a id="3-5-copy-view"></a>
3.1 从 Python 列表/元组
- np.array([1,2,3])

3.2 预定义形状
- np.zeros((m,n))
- np.ones((m,n))
- np.empty((m,n))
- np.full((m,n), fill_value)
- np.eye(n)
- np.diag([...])

3.3 等差/等间隔/对数间隔
- np.arange(start, stop, step)
- np.linspace(start, stop, num)
- np.logspace(start, stop, num, base=10)

3.4 随机数组
- np.random.rand(m,n)       # [0,1) 均匀
- np.random.uniform(low, high, size=(m,n))
- np.random.randint(low, high, size=(m,n))
- np.random.randn(m,n)      # 标准正态
- np.random.seed(seed)      # 设置随机种子

示例：
arr = np.arange(1,10)
arr2 = np.linspace(1,10,5)
print(arr, arr2)

<a id="4-index-slicing"></a>
4. 索引与切片（含布尔索引）
---------------------------
<a id="4-1-1d"></a>
### 4.1 一维索引/切片
- arr[i], arr[start:stop:step], arr[:] 等

<a id="4-2-multid"></a>
### 4.2 二维及多维索引
- arr[i, j]
- arr[i, :], arr[:, j]
- arr[i, 1:3]

<a id="4-3-boolean"></a>
### 4.3 布尔索引
- arr[arr > 10]
- 布尔数组作为索引可以筛选元素
- 多条件用 &（and）、|（or），注意括号： (arr>1) & (arr<5)

示例：
arr = np.random.randint(1,100,20)
print(arr[arr>50])

<a id="4-4-fancy"></a>
### 4.4 花式索引
- 使用整数数组作为索引，例如 arr[[1,3,5]]
- 索引广播：较小的索引数组会在较大的维度上重复

<a id="4-5-errors"></a>
### 4.5 常见错误及性能建议
- 避免对大数组使用 Python 循环，尽量使用向量化操作
- 注意布尔索引的内存消耗，必要时使用 `np.where` 进行条件选择

<a id="5-ops"></a>
5. 常用运算（算术、广播、矩阵运算）
----------------------------------
<a id="5-1-elementwise"></a>
### 5.1 元素级算术
- a + b, a - b, a * b, a / b（需要相同形状或可广播）

<a id="5-2-broadcast"></a>
### 5.2 广播机制
- 小数组会在较大数组上广播以匹配形状（遵循广播规则）

<a id="5-3-linear"></a>
### 5.3 矩阵运算
- 矩阵乘法使用 @ 或 np.dot(a,b)

示例：
A = np.array([[1,2],[3,4]])
B = np.array([[5,6],[7,8]])
print(A+B)
print(A*B)   # 元素乘
print(A @ B)  # 矩阵乘

<a id="6-functions"></a>
6. 常用函数（数学/统计/比较/选择/排序）
------------------------------------
<a id="6-1-math"></a>
### 6.1 基本数学函数
- np.sqrt, np.exp, np.log, np.sin, np.cos, np.abs, np.power, np.round, np.ceil, np.floor

<a id="6-2-stats"></a>
### 6.2 统计函数
- np.sum, np.mean, np.median, np.var, np.std, np.max/np.argmax, np.min/np.argmin, np.percentile
- 累计和/积：np.cumsum, np.cumprod
- 计数：np.count_nonzero

<a id="6-3-cumcount"></a>
### 6.3 累计与计数
- cumsum：累计求和
- cumprod：累计求积
- count_nonzero：计数非零元素

<a id="6-4-logic"></a>
### 6.4 比较与逻辑
- np.greater, np.less, np.equal
- np.logical_and, np.logical_or, np.logical_not
- np.any, np.all

<a id="6-5-where"></a>
### 6.5 条件选择
- np.where(condition, x, y)
- np.select(conditions, choices, default=...)

<a id="6-6-sort"></a>
### 6.6 排序与集合操作
- np.sort, np.argsort, np.unique, np.concatenate, np.split, np.reshape

练习提示：
- 使用 np.where 将成绩分段（不及格/良好/优秀）
- 使用 np.unique 去重

<a id="7-exercises"></a>
7. 实战练习（摘自 `numpy练习代码.ipynb`）
---------------------------------------
<a id="7-1-temp"></a>
练习 1：气温数组统计
- 题目：已知 a = np.array([28,30,29,31,32,30,29])，计算最高/最低/均值/超过30度的天数。
- 参考解法：
  a = np.array([28,30,29,31,32,30,29])
  print(np.max(a), np.min(a), np.mean(a))
  print(np.count_nonzero(a>30))

<a id="7-2-grades"></a>
练习 2：成绩处理
- 题目：b = np.array([85,90,78,92,88])，计算平均/方差/中位数，并转换为 10 分制。
- 参考解法：
  b = np.array([85,90,78,92,88])
  print(np.mean(b), np.var(b), np.median(b))
  print(b / 10.0)

<a id="7-3-matrix"></a>
练习 3：矩阵运算
- 题目：计算 A、B 的和、元素乘、矩阵乘。
- 参考解法：见上文 5.3 示例。

<a id="7-4-random"></a>
练习 4：随机数组与条件替换
- 题目：生成 shape=(3,4) 的随机整数（1~9），计算每列最大，每行最小，把奇数替换为 -1。
- 参考解法：
  arr = np.random.randint(1,10,(3,4))
  print(np.max(arr, axis=0))
  print(np.min(arr, axis=1))
  print(np.where(arr%2==1, -1, arr))
  arr[arr%2==1] = -1

<a id="7-5-advanced"></a>
7.5 进阶练习
- 题目：对随机生成的二维数组，分别计算每行/列的均值与标准差，并找出异常值（超过 3 倍标准差）。
- 参考解法：
  arr = np.random.randn(5,5) * 10 + 50  # 均值为 50，标准差为 10
  row_means = np.mean(arr, axis=1)
  col_means = np.mean(arr, axis=0)
  row_stds = np.std(arr, axis=1)
  col_stds = np.std(arr, axis=0)
  print("每行均值：", row_means)
  print("每列均值：", col_means)
  print("每行标准差：", row_stds)
  print("每列标准差：", col_stds)
  # 找出异常值
  anomalies = arr[(arr < (col_means - 3 * col_stds)) | (arr > (col_means + 3 * col_stds))]
  print("异常值：", anomalies)

<a id="8-pycharm"></a>
8. 在 PyCharm 中的实用技巧（Community / Professional）
--------------------------------------------------
<a id="8-1-prof"></a>
### 8.1 打开 Notebook（Professional）
- 右键 `.ipynb` → Open With → Jupyter Notebook Editor（需 Professional）
- 若 Structure/导览为空，检查 Markdown 标题是否以 `# `（# 后有空格）开头，否则目录插件可能无法识别。你已修复了这种情况。

<a id="8-2-community"></a>
### 8.2 Community 版处理策略
- Community 不原生支持 Notebook 编辑。两种常用方案：
  1) 在浏览器中使用 JupyterLab（已在你的环境中安装并启动），使用 Table of Contents 查看目录。URL 例子：
     http://localhost:8888/?token=（你的 token）
  2) 将 notebook 转成脚本（含 `# %%` 单元分隔），在 PyCharm 中打开并使用 code folding/regions。示例命令：

  jupyter nbconvert --to script "numpy学习代码.ipynb"

- 我已为你生成 `numpy学习代码.py`，并把 Markdown 单元转换为 `# region` / `# endregion` 以便在 PyCharm 中折叠。

<a id="8-3-config"></a>
### 8.3 折叠与区域（region）
- 在脚本中使用：
  # region 标题
  # endregion
  PyCharm 会把 region 识别为可折叠区域（左侧出现折叠图标），便于浏览大笔记。

<a id="9-troubleshoot"></a>
9. 常见问题与调试提示
-----------------------
<a id="9-1-structure"></a>
### 9.1 导览为空？
  - 答：检查 Markdown 标题是否以 `# ` 开头；确认打开的是 Notebook 编辑器而不是文本编辑器；重启 IDE 或 Invalidate Caches 有时可以修复索引问题。
<a id="9-2-nbconvert"></a>
### 9.2 nbconvert/环境问题的解决
  - 答：确保虚拟环境安装了 `nbconvert` 与 `notebook`，并尽量在 notebook 所在目录运行转换命令。

<a id="9-3-performance"></a>
### 9.3 性能问题诊断
- 向量化操作通常比 Python 循环快，尽量使用 Numpy 提供的向量化函数
- 大数组的内存占用与拷贝代价较高，注意使用视图（view）而非副本（copy）

<a id="10-next"></a>
10. 后续学习建议
-----------------
<a id="10-1-broadcast"></a>
### 10.1 深入广播规则与向量化技巧
- 学习 Numpy 的广播机制，理解不同形状数组之间的运算规则
- 尝试用向量化方式重写常规 for 循环实现的算法

<a id="10-2-pandas"></a>
### 10.2 学习 Pandas 与数据清洗流程
- Pandas 是基于 Numpy 的数据分析库，提供更高层次的数据操作接口
- 学习使用 Pandas 进行数据清洗、转换与分析

<a id="10-3-advanced"></a>
### 10.3 可选进阶：SciPy、scikit-learn、numba、并行化
- SciPy：基于 Numpy 的科学计算库，提供优化、积分、插值等功能
- scikit-learn：机器学习库，提供常用的机器学习算法与工具
- numba：JIT 编译器，可以将 Python 函数编译为高效的机器码
- 并行化：学习如何利用多核 CPU 提高计算密集型任务的性能

附录：参考示例（可直接复制粘贴到 Jupyter 中运行）
--------------------------------------------------
# ndarray 示例
import numpy as np
arr = np.array([1,2,3])
print(arr.shape, arr.ndim)

# 随机矩阵示例
np.random.seed(20)
arr = np.random.randint(1,10,(3,4))
print(arr)

# where 示例
score = np.random.randint(0,100,10)
labels = np.where(score<60, '不及格', np.where(score<80, '良好', '优秀'))
print(score, labels)

-- 结束 --
