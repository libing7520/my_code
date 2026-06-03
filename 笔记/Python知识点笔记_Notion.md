# Python 知识点笔记

根据所有 ipynb 文件的内容整理，涵盖 Python 基础语法、数据结构、控制流程、函数、面向对象、异常处理和数据可视化等核心内容。

---

## 一、Python 基础语法

### 1.1 变量与赋值

| 类型 | 示例 | 说明 |
|------|------|------|
| 普通赋值 | `a = 3` | 基本变量赋值 |
| 常量 | `PI = 3.14` | 约定常量名大写 |
| 链式赋值 | `a = b = c = 3` | 多个变量赋同一值 |
| 系列解包 | `a, b = 1, 2` | 同时赋值多个变量 |
| 交换变量 | `a, b = b, a` | 无需临时变量 |

### 1.2 内置数据类型

```python
a = 5          # int 整数
b = 5.2        # float 浮点数
c = True       # bool 布尔值
d = 3 + 4j     # complex 复数
e = "Hello"    # str 字符串
```

### 1.3 基本运算

| 运算符 | 功能 | 示例 |
|--------|------|------|
| `+` | 加法 | `5 + 2 = 7` |
| `-` | 减法 | `5 - 2 = 3` |
| `*` | 乘法 | `5 * 2 = 10` |
| `/` | 除法 | `5 / 2 = 2.5` |
| `//` | 整数除法 | `5 // 2 = 2` |
| `%` | 取模 | `5 % 2 = 1` |
| `**` | 幂运算 | `5 ** 2 = 25` |

### 1.4 进制表示

```python
a = 0b1010   # 二进制 → 10
b = 0o12     # 八进制 → 10
c = 0xA      # 十六进制 → 10
```

### 1.5 时间处理

```python
import time
print(time.time())                    # 时间戳
print(time.localtime())               # 本地时间对象
print(time.strftime("%Y-%m-%d %H:%M:%S", time.localtime()))  # 格式化时间
```

---

## 二、运算符

### 2.1 比较运算符

```python
a = 5
b = 2
print(a == b)   # 相等 → False
print(a != b)   # 不相等 → True
print(a > b)    # 大于 → True
print(a < b)    # 小于 → False
```

### 2.2 逻辑运算符

```python
a = True
b = False
print(a and b)  # 逻辑与 → False
print(a or b)   # 逻辑或 → True
print(not a)    # 逻辑非 → False
```

### 2.3 位运算符

```python
a = 5  # 二进制：0101
b = 3  # 二进制：0011
print(a & b)   # 按位与 → 1
print(a | b)   # 按位或 → 7
print(a ^ b)   # 按位异或 → 6
print(~a)      # 按位取反 → -6
print(a << 1)  # 左移 → 10
print(a >> 1)  # 右移 → 2
```

### 2.4 成员运算符

```python
a = [1, 2, 3, 4, 5]
print(3 in a)      # True
print(6 not in a)  # True
```

---

## 三、字符串操作

### 3.1 基本操作

```python
a = 'Hello World'
print(len(a))           # 长度 → 11
print(a + '!')          # 拼接
print(a.replace('World', 'Python'))  # 替换
```

### 3.2 字符串切片

```python
a = 'Hello World'
print(a[0])       # 第一个字符 → 'H'
print(a[-1])      # 最后一个字符 → 'd'
print(a[0:5])     # 前5个字符 → 'Hello'
print(a[6:])      # 从第6个到末尾 → 'World'
print(a[::-1])    # 反转 → 'dlroW olleH'
```

### 3.3 分割与连接

```python
a = 'Hello World'
b = a.split()           # 分割 → ['Hello', 'World']
c = '-'.join(b)         # 连接 → 'Hello-World'
```

### 3.4 字符串格式化

```python
name = 'Alice'
age = 30
greeting = 'My name is {} and I am {} years old.'.format(name, age)

pi = 3.141592653589793
print('Pi is approximately {:.2f}'.format(pi))  # 保留两位小数
```

---

## 四、列表（List）

### 4.1 创建列表

```python
a = [1, 2, 'True', 3.14]  # 混合类型
b = list(range(10))        # 0-9的整数序列
```

### 4.2 列表推导式

```python
a = [x * 2 for x in range(5)]                 # [0, 2, 4, 6, 8]
b = [x * 2 for x in range(100) if x % 9 == 0] # 带条件过滤
```

### 4.3 列表操作

| 操作 | 方法 | 说明 |
|------|------|------|
| 添加 | `append()` | 在末尾添加元素 |
| 插入 | `insert()` | 在指定位置插入 |
| 扩展 | `extend()` | 添加多个元素 |
| 删除 | `del` / `remove()` / `pop()` | 删除元素 |
| 清空 | `clear()` | 清空列表 |

### 4.4 列表排序

```python
a = [50, 40, 30, 20, 10]
a.sort()                    # 升序
a.sort(reverse=True)        # 降序

import random
random.shuffle(a)           # 随机打乱
```

---

## 五、元组（Tuple）

### 5.1 特点与创建

```python
a = (10, 20, 30, 40, 50)
print(a[0])       # 访问 → 10
print(a[1:4])     # 切片 → (20, 30, 40)
# a[0] = 100     # 错误！元组元素不可修改
```

### 5.2 zip 函数

```python
a = [1, 2, 3]
b = ['a', 'b', 'c']
c = zip(a, b)
print(list(c))    # [(1, 'a'), (2, 'b'), (3, 'c')]
```

---

## 六、字典（Dictionary）

### 6.1 创建字典

```python
a = {'name': 'Alice', 'age': 30}
b = dict(name='Bob', age=25)
c = dict([('name', 'Charlie'), ('age', 35)])
```

### 6.2 访问字典

```python
a = {'name': 'Alice', 'age': 30}
print(a['name'])              # 通过键访问
print(a.get('age'))           # get方法
print(a.get('country', 'USA')) # 键不存在时返回默认值
print(a.keys())               # 获取所有键
print(a.values())             # 获取所有值
print(a.items())              # 获取所有键值对
```

### 6.3 遍历字典

```python
a = {'name': 'Alice', 'age': 30}
for key, value in a.items():
    print(key, value)
```

---

## 七、控制流程

### 7.1 条件判断

```python
score = int(input('请输入成绩：'))
if 90 <= score <= 100:
    print('成绩为A')
elif 80 <= score < 90:
    print('成绩为B')
else:
    print('成绩为E')
```

### 7.2 while 循环

```python
num = 0
while num < 10:
    print(num)
    num += 1
```

### 7.3 for 循环

```python
for x in range(1, 10):
    print(x)

# 九九乘法表
for x in range(1, 10):
    for y in range(1, x+1):
        print('{0}*{1}={2}'.format(y, x, x*y), end='\t')
    print()
```

### 7.4 break 与 continue

```python
# break：终止循环
while True:
    a = input('请输入一个数：')
    if a == 'exit':
        break

# continue：跳过当前迭代
for x in range(1, 10):
    if x % 2 == 0:
        continue
    print(x)
```

---

## 八、函数

### 8.1 函数定义与调用

```python
def add(a, b):
    return a + b

result = add(3, 5)
print(result)  # 8
```

### 8.2 全局变量与局部变量

```python
x = 10  # 全局变量

def foo():
    x = 5  # 局部变量（遮蔽全局变量）
    print("Inside foo, x =", x)

foo()
print("Outside foo, x =", x)
```

---

## 九、面向对象编程

### 9.1 类的定义

```python
class Student:
    def __init__(self, name, score):
        self.name = name
        self.score = score
    
    def say_score(self):
        print("{0}的分数是{1}".format(self.name, self.score))

s1 = Student("张三", 80)
s1.say_score()
```

### 9.2 实例属性 vs 类属性

```python
class Student:
    school = "ABC University"  # 类属性
    
    def __init__(self, name, age):
        self.name = name        # 实例属性
        self.age = age          # 实例属性
```

### 9.3 三种方法类型

```python
class Student:
    def instance_method(self):
        print(f"实例方法：{self.name}")
    
    @classmethod
    def class_method(cls):
        print(f"类方法：{cls.school}")
    
    @staticmethod
    def static_method():
        print("静态方法")
```

---

## 十、异常处理

### 10.1 try-except 基础结构

```python
try:
    a = 5 / 0
except ZeroDivisionError as e:
    print(e)
```

### 10.2 try-except-else-finally

```python
try:
    a = float(input("被除数："))
    b = float(input("除数："))
    c = a / b
except BaseException as e:
    print(e)
else:
    print("结果：", c)
finally:
    print("无论如何都执行")
```

---

## 十一、Matplotlib 数据可视化

### 11.1 基础折线图

```python
from matplotlib import pyplot as plt
plt.rcParams['font.sans-serif'] = ['SimHei']  # 中文字体

x = [1, 2, 3, 4, 5]
y = [2, 3, 4, 5, 6]
plt.plot(x, y)
plt.xlabel('x轴')
plt.ylabel('y轴')
plt.title('折线图')
plt.show()
```

### 11.2 子图设置

```python
plt.subplot(1, 2, 1)  # 1行2列，第1个子图
plt.plot(x, y1)

plt.subplot(1, 2, 2)  # 1行2列，第2个子图
plt.plot(x, y2, color='orange')

plt.show()
```

### 11.3 双轴图

```python
fig, ax1 = plt.subplots(figsize=(10, 5))
ax1.plot(days, max_temp, color='red', marker='o')
ax2 = ax1.twinx()
ax2.plot(days, min_temp, color='blue', marker='o')
plt.show()
```

### 11.4 条形图

```python
categories = ['A', 'B', 'C', 'D', 'E']
values = [10, 15, 7, 12, 20]
plt.bar(categories, values)
plt.show()
```

---

## 总结

这份笔记涵盖了从 Python 基础语法到数据可视化的完整知识体系：

1. **基础语法**：变量、数据类型、运算符、字符串操作
2. **数据结构**：列表、元组、字典及其操作方法
3. **控制流程**：条件判断、循环结构、跳转语句
4. **函数**：定义、调用、参数、作用域
5. **面向对象**：类、属性、方法类型
6. **异常处理**：try-except-else-finally 结构
7. **数据可视化**：Matplotlib 绘图基础
