# 基础知识
## 数组创建
```
import numpy as np

# 基础创建
np.array([1, 2, 3])           # 从列表创建
np.zeros((3, 4))              # 全0数组
np.ones((2, 3))               # 全1数组
np.full((2, 2), 7)            # 填充指定值
np.empty((2, 2))              # 未初始化（值随机）

# 序列生成
np.arange(0, 10, 2)           # [0, 2, 4, 6, 8]，步长2
np.linspace(0, 1, 5)          # [0, 0.25, 0.5, 0.75, 1]，等分5份
np.logspace(0, 2, 3)          # [1, 10, 100]，对数刻度

# 特殊矩阵
np.eye(3)                     # 3x3 单位矩阵
np.identity(3)                # 同上
np.diag([1, 2, 3])            # 对角矩阵

# 随机数组
np.random.rand(3, 3)          # [0,1) 均匀分布
np.random.randn(3, 3)         # 标准正态分布
np.random.randint(0, 10, (3, 3))  # 整数随机
np.random.choice([1,2,3], 5)  # 有放回抽样

# 拷贝相关
np.array(a)                   # 深拷贝（默认）
np.copy(a)                    # 深拷贝
np.asarray(a)                 # 浅拷贝（若a已是ndarray则不复制）
```
## 数组属性
```
a = np.array([[1, 2, 3], [4, 5, 6]])

a.ndim          # 维度数：2
a.shape         # 形状：(2, 3)
a.size          # 元素总数：6
a.dtype         # 数据类型：int64（或int32）
a.itemsize      # 每个元素字节数：8
a.nbytes        # 总字节数：48
a.T             # 转置视图（不复制数据）
```
## 基本运算（元素级）
### 算术运算
```
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])

a + b           # [5, 7, 9]    逐元素相加
a - b           # [-3, -3, -3]
a * b           # [4, 10, 18]  逐元素相乘（不是矩阵乘！）
a / b           # [0.25, 0.4, 0.5]
a // b          # [0, 0, 0]    整除
a % b           # [1, 2, 3]    取模
a ** b          # [1, 32, 729] 幂运算
-a              # [-1, -2, -3] 取反

# 等价函数形式
np.add(a, b)
np.subtract(a, b)
np.multiply(a, b)
np.divide(a, b)
np.power(a, b)
np.mod(a, b)
```
## 标量运算
```
a + 10          # [11, 12, 13]  每个元素加10
a * 2           # [2, 4, 6]     每个元素乘2
a > 2           # [False, False, True]
```
## 复合赋值
```
a += 1          # a 变为 [2, 3, 4]，不创建新数组
a *= 2          # a 变为 [4, 6, 8]
```
### 比较运算（返回布尔数组）
```
a = np.array([1, 2, 3])
b = np.array([2, 2, 2])

a == b          # [False, True, False]
a != b          # [True, False, True]
a > b           # [False, False, True]
a >= b          # [False, True, True]

np.equal(a, b)
np.greater(a, b)
np.less_equal(a, b)
```
### 逻辑运算
```
x = np.array([True, False, True])
y = np.array([False, False, True])

np.logical_and(x, y)   # [False, False, True]
np.logical_or(x, y)    # [True, False, True]
np.logical_not(x)      # [False, True, False]
np.logical_xor(x, y)   # [True, False, False]异或，相同为0，不同为1

# 对数值数组（非0为True）
a = np.array([0, 1, 2])
b = np.array([0, 0, 3])
np.logical_and(a, b)   # [False, False, True]
```
### 位运算
```
np.bitwise_and(a, b)
np.bitwise_or(a, b)
np.bitwise_xor(a, b)
np.invert(a)           # 按位取反
np.left_shift(a, 2)    # 左移
np.right_shift(a, 2)   # 右移
```

## 索引与切片
### 基础索引
```
a = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

a[0, 1]         # 2          单个元素
a[0]            # [1, 2, 3]  第0行
a[:, 1]         # [2, 5, 8]  第1列
a[0:2, 1:3]     # [[2, 3],   子数组（切片）
                #  [5, 6]]
a[::2, ::2]     # [[1, 3],   步长为2
                #  [7, 9]]
a[::-1]         # 行逆序
a[:, ::-1]      # 列逆序
```
### np.where---条件选择
```
a = np.array([1, 2, 3, 4, 5])

# 三元表达式：满足条件取a*10，否则取0
np.where(a > 3, a * 10, 0)   # [0, 0, 0, 40, 50]

# 只传条件，返回满足条件的索引
np.where(a > 3)              # (array([3, 4]),)

# 多维
b = np.array([[1, 2], [3, 4]])
np.where(b > 2)              # (array([1, 1]), array([0, 1]))
```










