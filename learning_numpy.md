# 基础知识

## 术语

### 机器学习 (Machine Learning)分类

- 监督学习 supervised learning：有数据和标签
- 非监督学习 unsupervised learning：没有数据没有标签
- 半监督学习 semi-supervised learning：两者结合
- 强化学习 reinforcement learning：从经验中总结提升
- 遗传算法 genetic algorithm：与强化学习类似，适者生存优胜劣汰

### 样本、特征、张量

- 数据：二维的行
- 特征：二维的列
- 组合特征：列合并
- 组合样本：行合并
- 张量：即矩阵
- 激活函数：非线性函数
- 可以被训练，能够拟合数据的模型

### 前向传播、回归问题、分类问题

- 前向传播：计算最终结果
- 回归问题：预测事物的值
- 分类问题：预测事物的类别

### 元素数据类型 dtype

即元素的数据类型，可以创建时候指定，元素非简单类型则是object

```
raw_data = [
["Name", "StudentID", "Age", "AttendClass", "Score"],
["小明", 20131, 10, 1, 67],
["小花", 20132, 11, 1, 88],
["小菜", 20133, None, 1, "98"],
["小七", 20134, 8, 1, 110],
["花菜", 20134, 98, 0, None],
["刘欣", 20136, 12, 0, 12]
]
data = np.array(raw_data) # object
test1 = np.array([1,2,3]) # int32
test2 = np.array([1.1,2.3,3.4]) # float64
test3 = np.array([1,2,3], dtype=np.float64)
```

### a*=2(快)、b=2*b

```
# 这会产生新的 b
b = 2*b

# 这不会产生新的a, 和a[:] *= 2 一样
a *= 2    
```

## 创建与生成数据

### 一维二维三维

```
import numpy as np
cars = np.array([5, 10, 12, 6])
print("数据：", cars, "\n维度：", cars.ndim)
cars = np.array([
[5, 10, 12, 6],
[5.1, 8.2, 11, 6.3],
[4.4, 9.1, 10, 6.6]
])
print("数据：\n", cars, "\n维度：", cars.ndim)
cars = np.array([
[
    [5, 10, 12, 6],
    [5.1, 8.2, 11, 6.3],
    [4.4, 9.1, 10, 6.6]
],
[
    [6, 11, 13, 7],
    [6.1, 9.2, 12, 7.3],
    [5.4, 10.1, 11, 7.6]
],
])

print("总维度：", cars.ndim)
print("场地 1 数据：\n", cars[0], "\n场地 1 维度：", cars[0].ndim)
print("场地 2 数据：\n", cars[1], "\n场地 2 维度：", cars[1].ndim)
```

### empty、全0、全1、full全部相同，xxx_like

empty生成的内容垃圾值，非随机，仅仅占位而已

```
img = np.zeros((8,8),dtype="uint8")  二维8行8列
print(img)

zeros = np.zeros([2, 3])
print("zeros:\n", zeros)

ones = np.ones([3, 2])
print("\nones:\n", ones)

nines = np.full([2,3], 9)
print(nines)

print(np.empty([4,3]))

print(np.ones_like(nines))
print(np.zeros_like(nines))
print(np.empty_like(nines))
print(np.full_like(nines, 100))
```

### range序列

```
print(list(range(5))) # [0, 1, 2, 3, 4]
print(list(range(3, 10, 2))) # [3, 5, 7, 9]
print(np.arange(5)) # [0 1 2 3 4]
print(np.arange(3, 10, 2)) # [3 5 7 9]
```

### linspace 平均分布生成

可以指定不包含终点

```
print("linspace:", np.linspace(-1, 1, 5)) # [-1.  -0.5  0.   0.5  1. ]
print("5 segments:", np.linspace(-1, 1, 5, endpoint=False)) # 5 segments: [-1.  -0.6 -0.2  0.2  0.6]
```

### 正态分布、均匀分布

```
# (均值，方差，size)
print("正态分布：", np.random.normal(1, 0.2, 10))

# (最低，最高，size)
print("均匀分布：", np.random.uniform(-1, 1, 10))
```

### 随机生成

- seed：随机种子与以往不同，想要每次都相同才要设置...
- rand、random：默认生成0~1的浮点
- randn：标准正态分布
- randint：整数

```
np.random.seed(2)
print(np.random.rand(2,3))
print(np.random.random([2, 3]))

[[0.45146826 0.36094719 0.03049207]
 [0.89936196 0.55207281 0.59825998]]

print(np.random.randn(2,3))

print(np.random.randint(0, 10, (2, 3)))
[[9 4 7]
 [7 8 1]]
```

## 取值（用索引取值会深拷贝）

### 取一行、取一个、取多个、取矩形个

```
a = np.array([1, 2, 3])
print("a[0]:", a[0])
```

```
b = np.array([
[1,2,3,4],
[5,6,7,8],
[9,10,11,12]
])

# 取一行   选第 2 行所有数
print("b[1]:\n", b[1])   

# 取一个   选第 2 行，第 1 列的数
print("b[1,0]:\n", b[1,0])   

# 取多个，[1,0],[2,3]代表取第一行第二列，第0行第三列
# 其实就是多个二维坐标的行放一起、列放一起
print("b[[1,0],[2,3]]:\n", 
b[[1,0],[2,3]])


# 取矩形个元素
img=np.zeros((5,5),np.uint8)
img[1:4,1:4]=1
```

### 随机取

```
data = np.array([2,1,3,4,6])
print("选一个：", np.random.choice(data))
print("选多个：", np.random.choice(data, size=3))
print("不重复地选多个(不放回)：", np.random.choice(data, size=3, replace=False))
print("带权重地选择：", np.random.choice(data, size=10, p=[0,0,0,0.2,0.8]))
```

### take 按索引

- indices	索引序列，可以是列表或数组
- axis	沿哪个轴取值，默认展开成一维

```
arr = np.array([10, 20, 30, 40])
res = np.take(arr, [0, 2])
print(res) # [10 30]
arr2d = np.array([[1,2],[3,4],[5,6]])
res2d = np.take(arr2d, [0,2], axis=0)  # 取第0行和第2行
print(res2d)

[[1 2]
 [5 6]]
```

### compress 布尔筛选

类似掩码的作用

```
arr = np.array([10, 20, 30, 40])
mask = np.array([True, False, True, False])
res = np.compress(mask, arr)
print(res) # [10 30]


arr2d = np.array([[1,2],[3,4],[5,6]])
mask = np.array([True, False, True])
res2d = np.compress(mask, arr2d, axis=0)  # 选出第0轴中 True 的行
print(res2d)
[[1 2]
 [5 6]]
```

## 拷贝、洗牌

### copy、shuffle

```
data_copy = np.copy(data)
np.random.shuffle(data)
print("源数据：", data_copy)
print("shuffled:", data)
```

### 将序号洗牌 permutation

```
data = np.array([2,1,3,4,6])
print("直接出乱序序列：", np.random.permutation(10)) # [7 2 8 3 9 5 6 4 1 0]
# 多维数据在第一维度上乱序
arr2d = np.array([[1,2],[3,4],[5,6]])
shuffled2d = np.random.permutation(arr2d)
print(shuffled2d)

[[3 4]
 [5 6]
 [1 2]]
```

## 一维变二维、改变维度

### expand_dims、squeeze 添加去除维度

```
# 一维数组，6列
a = np.array([1,2,3,4,5,6])

# 二维数组，一行6列，
a_2d = a[np.newaxis, :]
a_expand = np.expand_dims(a, axis=0)

# 二维数组，6行1列
a_2d = a[:, np.newaxis]
a_none = a[:, None]
a_expand = np.expand_dims(a, axis=1)

# 默认去掉所有长度为 1 的维度，指定参数是维度的索引
_squeeze = np.squeeze(a_expand)
a_squeeze_axis = a_expand.squeeze(axis=1)
```

### reshape 变形

```
# 一行6列
a = np.array([1,2,3,4,5,6])
# 二行3列
a1 = a.reshape([2, 3])
# 三页一行2列
a2 = a.reshape([3,1,2])
```

### 转置

2维度是行列互换，多维度可以指定交换顺序

```
a = np.array([1,2,3,4,5,6]).reshape([2, 3])
aT1 = a.T
aT2 = np.transpose(a)
```

## 拼接合并（行变多、列变多）

- 行变多即叠加行
- 列变多即叠加列

### column_stack 叠加列, row_stack 叠加行

```
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
# 把每个数组竖着放一列
c = np.column_stack((a, b))

[[1 4]
 [2 5]
 [3 6]]
```

```
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
# 横着叠行
d = np.row_stack((a, b))
[[1 2 3]
 [4 5 6]]
```

### vstack 叠加行, hstack 叠加列

- V: 上下叠
- h: 左右拼

```
feature_a = np.array([1,2,3,4,5,6])[:, None]  # 6行1列
feature_b = np.array([11,22,33,44,55,66])[:, None]  # 6行1列
c_stack = np.hstack([feature_a, feature_b])  # 6行2列

sample_a = np.array([0, 1.1])[None, :] # 一行2列
sample_b = np.array([1, 2.2])[None, :] # 一行2列
c_stack = np.vstack([sample_a, sample_b]) # 2行2列
```

```
a = np.array([
[1,2],
[3,4]
])
b = np.array([
[5,6],
[7,8]
])
print("竖直合并\n", np.vstack([a, b]))
print("水平合并\n", np.hstack([a, b]))


竖直合并
 [[1 2]
 [3 4]
 [5 6]
 [7 8]]
水平合并
 [[1 2 5 6]
 [3 4 7 8]]

```

### concatenate 沿指定轴拼接

- 简单应用，在列表末尾追加列表

```
cars1 = np.array([5, 10, 12, 6])
cars2 = np.array([5.2, 4.2])
cars = np.concatenate([cars1, cars2])
```

- 高级效果

```
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
# 一维数组只能沿 axis=0 拼接
# 等价于 hstack，即列叠加，[1 2 3 4 5 6]
c = np.concatenate((a, b))

a2 = np.array([[1, 2],
               [3, 4]])
b2 = np.array([[5, 6],
               [7, 8]])
# 行数增加，列数保持不变，相当于 vstack
c2 = np.concatenate((a2, b2), axis=0)
#[[1 2]
# [3 4]
# [5 6]
# [7 8]]


# 列数增加，行数保持不变，相当于 hstack
# [[1 2 5 6]
#  [3 4 7 8]]
d2 = np.concatenate((a2, b2), axis=1)
```

```

test1 = np.array([5, 10, 12, 6,1])
test2 = np.array([5.1, 8.2, 11, 6.3, 1])

# 首先需要把它们都变成二维，下面这两种方法都可以加维度
test1 = np.expand_dims(test1, 0)
test2 = test2[np.newaxis, :]

print("test1加维度后 ", test1)
print("test2加维度后 ", test2)

# 然后再在第一个维度上叠加
all_tests = np.concatenate([test1, test2])
print("括展后\n", all_tests)


print("第一维度叠加：\n", np.concatenate([all_tests, all_tests], axis=0))
print("第二维度叠加：\n", np.concatenate([all_tests, all_tests], axis=1))




第一维度叠加：concatenate参数axis=0（默认）是将2行变为4行
 [[ 5.  10.  12.   6. ]
 [ 5.1  8.2 11.   6.3]
 [ 5.  10.  12.   6. ]
 [ 5.1  8.2 11.   6.3]]
第二维度叠加：concatenate参数axis=1，是将4列变为8列
 [[ 5.  10.  12.   6.   5.  10.  12.   6. ]
 [ 5.1  8.2 11.   6.3  5.1  8.2 11.   6.3]]

但要注意行列数要一致才可合并
```

## 拆分

- vsplit = “上下拆”
- hsplit = = “左右拆”
- split = 万用接口，可控制 axis

### split 一维数组拆分

```
a = np.array([0, 1, 2, 3, 4, 5])
# 返回列表，3个元素，元素是2列的数组
# [array([0, 1]), array([2, 3]), array([4, 5])]
subarrays = np.split(a, 3)


# 指定拆分位置[1, 4]，分三分
# 第一份 [0列]
# 第二份 [1,2，3列]
# 第三份 [4,5列]
# [array([0]), array([1, 2, 3]), array([4, 5])]
subarrays = np.split(a, [1, 4])
```

### split 多维数组拆分

```
a2 = np.arange(16).reshape(4,4)
print(a2)

cols = np.split(a2, [1,3], axis=1)
print(cols[0])
print(cols[1])
print(cols[2])

[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]
 [12 13 14 15]]
[[ 0]
 [ 4]
 [ 8]
 [12]]
[[ 1  2]
 [ 5  6]
 [ 9 10]
 [13 14]]
[[ 3]
 [ 7]
 [11]
 [15]]
```

### vsplit 横着切

本质上是 split 的快捷方式：axis=0

```
a2 = np.arange(16).reshape(4, 4)
parts = np.vsplit(a2, 2)  # 垂直拆成2份
print(parts[0])
print(parts[1])

[[0 1 2 3]
 [4 5 6 7]]
[[ 8  9 10 11]
 [12 13 14 15]]

```

### hsplit 竖着切

本质上是 split 的快捷方式：axis=1

```
a2 = np.arange(16).reshape(4, 4)
parts = np.hsplit(a2, 2)  # 垂直拆成2份
print(parts[0])
print(parts[1])

[[ 0  1]
 [ 4  5]
 [ 8  9]
 [12 13]]
[[ 2  3]
 [ 6  7]
 [10 11]
 [14 15]]
```

## 遍历、size、len、行列数

```
cars = np.array([
[5, 10, 12, 6],
[5.1, 8.2, 11, 6.3],
[4.4, 9.1, 10, 6.6]
])

count = 0
for i in range(len(cars)):
    for j in range(len(cars[i])):
        count += 1
print("总共多少测试数据：", count)

print("总共多少测试数据：", cars.size)
print("第一个维度：", cars.shape[0])
print("第二个维度：", cars.shape[1])
print("所有维度：", cars.shape)

总共多少测试数据： 12
总共多少测试数据： 12
第一个维度： 3
第二个维度： 4
所有维度： (3, 4)
```

## 切片

- 切片是引用，不会深拷贝
- 切片写法：[start : end : step]，从索引 start 开始，取到但不包括 end，每次跨 step 个。
- 二维写法: [行切片，列切片]

```
:	表示“从头到尾”
a:b	从第 a 行/列到第 b 行/列（不含 b）
-1	倒数第 1 个
:b	从开头到第 b 行/列（不含 b）
a:	从第 a 行/列到结尾
::2	每隔 2 个取 1 个（步长为 2）
[::-1] → 倒序切片，即反转元组
```

```
b = np.array([
[1,2,3,4],
[5,6,7,8],
[9,10,11,12]
])

print("b[:2]:\n", b[:2]) 前两行
print("b[:2, :3]:\n", b[:2, :3]) 左上角2x3
print("b[1:3, -2:]:\n", b[1:3, -2:]) 右下角2x2



b[:2]:
 [[1 2 3 4]
 [5 6 7 8]]
b[:2, :3]:
 [[1 2 3]
 [5 6 7]]
b[1:3, -2:]:
 [[ 7  8]
 [11 12]]

```

```
import numpy as np
list2d =np.arange(18).reshape(3,6)
print(list2d)
h,w=list2d.shape[::]
print(h,w)
w,h=list2d.shape[::-1]
print(w,h)

[[ 0  1  2  3  4  5]
 [ 6  7  8  9 10 11]
 [12 13 14 15 16 17]]
3 6
6 3
```

## 比较（返回布尔索引），where

### 一维数组

```
a = np.array([3,6,8,1,2,88])
b = np.where(a > 5)
print(b)


a > 5 会得到布尔数组：
[False, True, True, False, False, True]
np.where(a > 5) 会返回 符合条件元素的索引：
(array([1, 2, 5]),)
```

### 二维数组

```
a = np.array([
    [3, 6, 8, 77, 66],
    [1, 2, 88, 3, 98],
    [11, 2, 67, 5, 2]
])
print(a)
b = np.where(a > 5)
print(b)


a > 5 对每个元素判断，得到布尔矩阵：
[[False, True, True, True, True],
 [False, False, True, False, True],
 [True, False, True, False, False]]

np.where(a > 5) 返回 两个数组：
(array([0, 0, 0, 0, 1, 1, 2, 2]), array([1, 2, 3, 4, 2, 4, 0, 2]))

第一个数组 → 符合条件元素的 行索引，
第二个数组 → 符合条件元素的 列索引
(0,1) → a[0,1] = 6
(0,2) → a[0,2] = 8
(1,2) → a[1,2] = 88
(2,0) → a[2,0] = 11
(2,2) → a[2,2] = 67

```


```
a = np.array([
[1,2,3,4],
[5,6,7,8],
[9,10,11,12]
])
# 注意numpy里的逐个元素bool则要用符号 &、|、~ 进行逐元素逻辑运算；
# 此处condition是个bool二维数组
condition = (a > 7) & (a < 10)
print(condition)
print(a[condition])
# 将满足条件的元素换为-1
print(np.where(condition, -1, a))
# 满足与满不足条件的都进行更新
b = a-0.1
c = a+0.1
print(np.where(condition, b, c))


[[False False False False]
 [False False False  True]
 [ True False False False]]
[8 9]
[[ 1  2  3  4]
 [ 5  6  7 -1]
 [-1 10 11 12]]
[[ 1.1  2.1  3.1  4.1]
 [ 5.1  6.1  7.1  7.9]
 [ 8.9 10.1 11.1 12.1]]

```

## 查找、is_nan、flatten、ravel


is_nan：判断nan，返回bool数组
argwhere：返回结果为T的索引位置数组
flatten：将所有数据连一起，返回1维数组，会深拷贝，速度慢
ravel：比flatten快很多，没拷贝，是引用

```
data = np.array([1.2, np.nan, 3.4, np.nan])
is_nan = np.isnan(data)
nan_idx = np.argwhere(is_nan)
print(nan_idx)
[[1]
 [3]]

b = np.array([[1, 2, 3],
              [4, 0, 6],
              [0, 8, 9]])

idx = np.argwhere(b == 0)
print(idx)
[[1 1]
 [2 0]]

print(idx.flatten())
[1 1 2 0]
```

## 点乘

- 点乘的2个方式

```
a = np.array([
[1, 2],
[3, 4]
])
b = np.array([
[5, 6],
[7, 8]
])

print(a.dot(b))
print(np.dot(a, b))
```

```
data = np.random.rand(4, 3)
weights = np.random.rand(3, 2)
output = np.dot(data, weights)

print("data shape:", data.shape) # (4, 3)
print("weights shape:", weights.shape) # (3, 2)
print("output shape:", output.shape) # (4, 2)
```

## 加减乘除、累乘、总和、minmax(及索引)、平均值、中位数、标准差、取整、调到范围内

```
# 每个元素都进行的加减乘除
a = np.array([150, 166, 183, 170])
print("a + 3:", a + 3)
print("a - 3:", a - 3)
print("a * 3:", a * 3)
print("a / 3:", a / 3)

print("最大：", np.max(a))
print("最小：", a.min())
print(a.sum())
print("累乘：", a.prod())
print("总数：", a.size)
a = np.array([0, 1, 2, 3])
print("非零总数：", np.count_nonzero(a))

month_salary = [1.2, 20, 0.5, 0.3, 2.1]
print("平均工资：", np.mean(month_salary))
print("工资中位数：", np.median(month_salary))

month_salary = [1.2, 20, 0.5, 0.3, 2.1]
# 标准差越大 → 数据的差异越大（分布更分散）
# 标准差越小 → 数据越集中（大家的值都差不多）
print("标准差：", np.std(month_salary))
```

```
a = np.array([150, 166, 183, 170])
name = ["小米", "OPPO", "Huawei", "诺基亚"]
# minmax的索引号
high_idx = np.argmax(a)
low_idx = np.argmin(a)
print("{} 最高".format(name[high_idx]))
print("{} 最矮".format(name[low_idx]))
a = np.array([150.1, 166.4, 183.7, 170.8])
# 取整，有小数的加1取整
print("ceil:", np.ceil(a)) # [151. 167. 184. 171.]
print("floor:", np.floor(a)) # [150. 166. 183. 170.]
# 将所有数据调整到区间内
print("clip:", a.clip(160, 180)) # [160.  166.4 180.  170.8]
```

## 文件操作

### fromstring

```
row_string = "20131, 10, 67, 20132, 11, 88, 20133, 12, 98, 20134, 8, 100, 20135, 9, 75, 20136, 12, 78"
data = np.fromstring(row_string, dtype=np.int64, sep=",")
data = data.reshape(6, 3)
```

### genfromtxt

可读字符串、自动处理缺失值

```
data = np.genfromtxt("covid19_day_wise.csv", delimiter=",", skip_header=1, dtype=None, encoding='utf-8')
```

### loadtxt

只能读数值的字段
- fname	文件路径或文件对象
- delimiter	分隔符（CSV 一般用 ','）
- skiprows	跳过前几行（如跳过标题行）
- usecols	指定要读取的列，如 (0, 2, 3)
- dtype	数据类型（默认 float）

```
data = np.loadtxt("read-save-data/data.csv", delimiter=",", skiprows=1, dtype=np.int64)
```

### 保存与读取

- 保存为文本

```
print("numpy data:\n", data)
np.savetxt("read-save-data/save_data.csv", data, delimiter=",", fmt='%s')

print("data file in directory:", os.listdir("read-save-data"))
with open("read-save-data/save_data.csv", "r") as f:
    print("\n", f.read())
```

- 保存为二进制，可将多个NumPy数组保存到一个文件中.npz, 是一个压缩的zip文件，里面包含多个 .npy 文件，每个对应一个数组。

```
a = np.array([1, 2, 3])
b = np.array([[4,5,6], [7,8,9]])

# 保存多个数组（默认名字）
np.savez('data.npz', a, b)
loaded = np.load('data.npz')
print(loaded['arr_0'])  # 输出: [1 2 3]
print(loaded['arr_1'])  # 输出: [[4 5 6] [7 8 9]]

# 保存多个数组（自定义名字）
np.savez('data_named.npz', first=a, second=b)
loaded = np.load('data_named.npz')
print(loaded['first'])   # [1 2 3]
print(loaded['second'])  # [[4 5 6] [7 8 9]]

# 使用压缩保存
np.savez_compressed('data_compressed.npz', first=a, second=b)
loaded = np.load('data_compressed.npz')
print(loaded['first'])
```
