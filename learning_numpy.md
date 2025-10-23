# 基础知识

## 术语

### 样本、特征

- 二维行是数据样本（第一维度），列是特征（第二维度）。
- 组合特征：列合并
- 组合样本：行合并

## 创建数据

一维二维三维

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

## 取值

- 取一行
- 取一个
- 取多个

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
```

## 改变维度

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

## 遍历、size、行列数

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

- 切片写法：[start : end : step]，从索引 start 开始，取到但不包括 end，每次跨 step 个。
- 二维写法: [行切片，列切片]，
```
:	表示“从头到尾”
a:b	从第 a 行/列到第 b 行/列（不含 b）
-1	倒数第 1 个
:b	从开头到第 b 行/列（不含 b）
a:	从第 a 行/列到结尾
::2	每隔 2 个取 1 个（步长为 2）
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

## 条件选择

可以使用bool运算检查每个元素的结果，并进行更新

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

## 加减乘除、点乘、累乘、总和、minmax(及索引)、标准差、取整、调到范围内

```
# 每个元素都进行的加减乘除
a = np.array([150, 166, 183, 170])
print("a + 3:", a + 3)
print("a - 3:", a - 3)
print("a * 3:", a * 3)
print("a / 3:", a / 3)

# 点乘的2个方式
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