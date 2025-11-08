# 基本窗口

## 加载图片、显示、保存、创建窗口、销毁窗口

```
import cv2
img = cv2.imread('lean.jpg', -1)
cv2.namedWindow('image')
cv2.imshow('image', img)
cv2.waitKey(0)
cv2.imwrite('lean2.jpg', img)
cv2.destroyAllWindows()
```

## shape、size、dtype

- shape：行、列、通道数
- size：行*列*通道数
- dtype：像素点的数据类型

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
print(dst.shape, dst.size, dst.dtype)
```

## 默认色彩顺序

原始图像，默认是 BGR 格式（OpenCV 的默认色彩顺序）。

## 自动灰度导入

imread的末尾参数使用0，即使彩色也按照灰度图导入

# 图形处理

## 创建随机灰度图、彩色图

```
m = np.random.randint(10, 99, size=(256, 256), dtype='uint8')
m = np.random.randint(0, 256, size=[256, 256,3], dtype='uint8')
```

## 创建8通道图

```
每个通道保存一个 2 的幂次,实质为8个二进制位
x[:,:,0] = 1
x[:,:,1] = 2
x[:,:,7] = 128
换句话说，x[:,:,i] 对应第 i 位的权值。

x = np.zeros((r, c, 8), dtype='uint8')
for i in range(8):
    x[:,:,i] = 2**i
```

## 读写像素

### 数组方式（逐像素）

```
img = cv2.imread('lean.jpg', -1)
cv2.namedWindow('image')
cv2.imshow('image', img)

for i in range(10, 100):
    for j in range(80, 100):
        img[i,j]=255
cv2.imshow('after', img)
cv2.waitKey(0)
```

### item与itemset（逐像素）

```
m = np.random.randint(10, 99, size=(256, 256), dtype='uint8')
print(m.item(3,2))
m.itemset((3,2), 0)
print(m.item(3,2))
cv2.waitKey(0)
```

```
for i in range(0, 100):
    for j in range(100, 200):
        for k in range(0, 3):
            m.itemset((i,j,k), 128)
```

### ROI（即切片、整片的改）

- m[:,:,0] = 255, B通道，设置为蓝
- m[:,:,1] = 255，G通道，设置为绿
- m[:,:,2] = 255，R通道，设置为红

```
m = np.zeros((300,300,3), dtype="uint8")
# 设置50-100行为绿色
m[50:100,:,1] = 255
# 设置100-200列为红色
m[:,100:200,2] = 255
cv2.imshow("Original", m)
```

```
img = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
# 原图
cv2.imshow('image1', img)
# 局部
cv2.imshow('image2', img[0:150, 0:150])
# 更改原图的局部
img[0:150, 0:150] = np.random.randint(0, 256, size=[150, 150, 3], dtype='uint8')
cv2.imshow('image3', img)
cv2.waitKey(0)
```

### 局部的复制

```
src = np.random.randint(0, 256, size=[256, 256,3], dtype='uint8')
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
dst[0:150, 0:150] = src[0:150, 0:150]
cv2.imshow('image', dst)
cv2.waitKey(0)
```

## 通道

### 拆分通道（切片方式）、改通道值

取3个通道值、修改B通道

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
b = dst[:,:,0]
g = dst[:,:,1]
r = dst[:,:,2]

cv2.imshow('b', b)
cv2.imshow('g', g)
cv2.imshow('r', r)
dst[:,:,0] = 0
cv2.imshow('img', dst)
```

### 拆分通道（split）、合并通道

```
dst = cv2.imread('lean.jpg', cv2.IMREAD_UNCHANGED)
b, g, r = cv2.split(dst)
cv2.imshow('bgr', cv2.merge((b, g, r)))
cv2.imshow('rgb', cv2.merge((r, g, g)))
cv2.waitKey(0)
```

```
import cv2
img=cv2.imread("barbara.bmp")
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv)
v[:,:]=255
newHSV=cv2.merge([h,s,v])
art = cv2.cvtColor(newHSV, cv2.COLOR_HSV2BGR)
cv2.imshow("img",img)
cv2.imshow("art",art)
cv2.waitKey()
cv2.destroyAllWindows()
```

### alpha通道

运行时看不出来，保存后看文件才会有效果。。。

```
import cv2
img=cv2.imread("lenacolor.png")
bgra = cv2.cvtColor(img, cv2.COLOR_BGR2BGRA)
b,g,r,a=cv2.split(bgra)
a[:,:]=125
bgra125=cv2.merge([b,g,r,a])
a[:,:]=0
bgra0=cv2.merge([b,g,r,a])
cv2.imshow("img",img)
cv2.imshow("bgra",bgra)
cv2.imshow("bgra125",bgra125)
cv2.imshow("bgra0",bgra0)
cv2.waitKey()
cv2.destroyAllWindows()
cv2.imwrite("bgra.png", bgra)
cv2.imwrite("bgra125.png", bgra125)
cv2.imwrite("bgra0.png", bgra0)
```

## 运算

### 加法+、add（变亮）

- add： 超过255则等于255（图像变亮）
- +： 超过255则取模（变暗）
- 可以数组+数组，也可以数字+数组

```
m1 = np.random.randint(0, 256, size=(3, 3), dtype='uint8')
m2 = np.random.randint(0, 256, size=(3, 3), dtype='uint8')
print(m1+m2)
print(cv2.add(m1, m2))
print(cv2.add(m1, 100))
```

### 加权（alpha混合）

类似alpha混合，分别对2个src进行浮点设置，权重值通常为0，其实三个数都可以随意

```
rc = cv2.imread('rc.jpg', -1)
img = cv2.imread('lean.jpg', -1)
r = cv2.addWeighted(img, 0.1, rc, 0.9, 0)
cv2.imshow('bgr', r)
```

### 按位与（alpha测试）

mask上像素为255即白全1，则src通过，否则非全1则失败

- 一张图与mask

```
img = cv2.imread('lean.jpg', -1)
mask = np.zeros(img.shape, dtype="uint8")
mask[100:200, 100:200] = 255
c = cv2.bitwise_and(img, mask)
cv2.imshow('bgr', c)
cv2.waitKey(0)
```

- 2张图与mask，2张图按位与然后再mask测试

```
img = cv2.imread('lean.jpg', 1)
w,h,c=img.shape
mask = np.zeros((w,h), dtype="uint8")
mask[100:200, 100:200] = 255
img2 = cv2.imread('rc.jpg', 1)
c = cv2.bitwise_and(img, img2, mask=mask)
cv2.imshow('bgr', c)
```

### 按位或、按位非、按位异或

- bitwise_or
- bitwise_not
- bitwise_xor，常用于图片的加密解密，因为异或（XOR）运算是可逆的：如果 A⊕K=B，那么 B⊕K=A。

```
img = cv2.imread('lena.jpg', 0)
cv2.imshow('lena', img)
r, c = img.shape
k = np.random.randint(0, 256, size=(r, c), dtype='uint8')
enc=cv2.bitwise_xor(img, k)
dec=cv2.bitwise_xor(enc, k)
cv2.imshow('2', k)
cv2.imshow('3', enc)
cv2.imshow('4', dec)
cv2.waitKey(0)
cv2.destroyAllWindows()

```

### 位平面

255是8个二进制位，所以可分成8个位平面（二维数组）

```
import cv2
import numpy as np

# 1. 读取灰度图
img = cv2.imread('lena.jpg', 0)
cv2.imshow('lena', img)
r, c = img.shape
# 创建提取矩阵，因为灰度图是8位，所以8张
x = np.zeros((r, c,8), dtype='uint8')
for i in range(8):
    # 设置提取矩阵的值
    x[:,:,i] = 2**i

# 创建位平面8个
result =np.zeros((r,c,8), dtype='uint8')
for i in range(8):
    # 提取位平面，2**i是对应位平面的掩码，与图片按位或，得到位平面
    result[:, :, i] = cv2.bitwise_and(img, 2**i)
    # 阈值处理、将大于0的点改为真、否则为假，真的改为白色，用于显示
    # mask是二维数组，内容是T、F
    mask = result[:, :, i] > 0
    result[mask, i] = 255
    cv2.imshow(f'Bit plane {i}', result[:, :, i])


cv2.waitKey(0)
cv2.destroyAllWindows()
```

### 数字水印

即将第0位平面替换为同尺寸的二值图

```
import cv2
import numpy as np

# 注意2张图要同尺寸
lena = cv2.imread('lena.jpg', 0)
watermark=cv2.imread("watermark.png", 0)
# 将水印图所有非零像素都设为1,即将其二值化（把灰度水印变为黑白掩码）。
w=watermark[:,:]>0
watermark[w]=1

# 创建矩阵，每个像素值都是 254（即二进制 11111110）。
r,c=lena.shape
t254=np.ones((r,c),dtype=np.uint8)*254
# 关键的“清零最低有效位（LSB）”操作。
lenah7=cv2.bitwise_and(lena,t254)
# 水印嵌入到最低位。每个像素的最低位上写入水印位（0 或 1）。
e=cv2.bitwise_or(lenah7,watermark)

# 提取嵌入后的图像 e 的最低有效位，即“取出”隐藏在图像里的水印。
t1=np.ones((r,c),dtype=np.uint8)
wm=cv2.bitwise_and(e,t1)
# 把提取出的水印放大到可视化范围（0 → 黑，255 → 白）。
w=wm[:,:]>0
wm[w]=255

cv2.imshow('lena', lena)
cv2.imshow('watermark', watermark*255)
cv2.imshow('e', e)
cv2.imshow('wm', wm)
cv2.waitKey(0)
```

### 打码与解码

```
import cv2
import numpy as np
#读取原始载体图像
lena=cv2.imread("lena.jpg",0)
#读取原始载体图像的shape值
r,c=lena.shape

# 掩码矩阵，用于指定“要打码的区域”。全部初始化为 0（黑色）；
# 中间 mask区域设为 1，对应 Lena 的脸部。
mask=np.zeros((r,c),dtype=np.uint8)
mask[110:200,125:175]=1
cv2.imshow("lena",lena)
cv2.imshow("mask",mask*255)


#随机矩阵作为密钥
key=np.random.randint(0,256,size=[r,c],dtype=np.uint8)
cv2.imshow("key",key)
#============获取打码脸============
# 整张图像都与密钥异或，得到加密后的图像。
lenaXorKey=cv2.bitwise_xor(lena,key)
cv2.imshow("lenaXorKey",lenaXorKey)
# 提取出“加密图像中属于脸部的部分”（其余区域清零置黑）。
encryptFace=cv2.bitwise_and(lenaXorKey,mask*255)
cv2.imshow("encryptFace",encryptFace)

#清除原始图像中的脸部（即只保留身体、背景部分）。
# 1-mask是对二值内容进行取反，即1变0，0变1
noFace1=cv2.bitwise_and(lena,(1-mask)*255)
cv2.imshow("1-mask",(1-mask)*255)
cv2.imshow("noFace1",noFace1)

#把加密的脸（encryptFace）加回背景部分（noFace1），
# 得到被打码的 Lena 图像（脸部是加密的）。
maskFace=encryptFace+noFace1
cv2.imshow("maskFace",maskFace)
cv2.waitKey()
cv2.destroyAllWindows()

#============将打码脸解码============
cv2.imshow("maskFace",maskFace)
#将脸部打码的lena与密钥key异或，脸部复原了，但其余部分会变为打码
extractOriginal=cv2.bitwise_xor(maskFace,key)
cv2.imshow("extractOriginal",extractOriginal)

#提取出解码后的脸部。（其余区域清零置黑）。
extractFace=cv2.bitwise_and(extractOriginal,mask*255)
cv2.imshow("extractFace",extractFace)

# 提取图像中不包含脸的部分。
noFace2=cv2.bitwise_and(maskFace,(1-mask)*255)
cv2.imshow("noFace2",noFace2)

# 将解码出的脸与背景部分重新合并，得到完全复原的 Lena。
extractLena=noFace2+extractFace
cv2.imshow("extractLena",extractLena)

cv2.waitKey()
cv2.destroyAllWindows()
```

## 色彩空间

### 转换函数 cvtColor

```
import cv2
import numpy as np
img=np.random.randint(0,256,size=[2,4,3],dtype=np.uint8)
rgb=cv2.cvtColor(img,cv2.COLOR_BGR2RGB)
bgr=cv2.cvtColor(rgb,cv2.COLOR_RGB2BGR)
print("img=\n",img)
print("rgb=\n",rgb)
print("bgr=\n",bgr)
```

```
import cv2
import numpy as np
lena=cv2.imread("lena.jpg")
rgb = cv2.cvtColor(lena, cv2.COLOR_BGR2RGB)
cv2.imshow("lena",lena)
cv2.imshow("rgb",rgb)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 阈值筛选 inRange

#### 颜色识别与分离

- 把图像从 BGR 空间转换到 HSV 空间，再通过设定颜色范围提取蓝、绿、红等区
- inRange用于检测点值是否再指定范围内，并返回二维结果作为mask
- 再使用bitwise_and对mask提取区域

```
import cv2
import numpy as np
opencv=cv2.imread("opencv.jpg")
hsv = cv2.cvtColor(opencv, cv2.COLOR_BGR2HSV)
cv2.imshow('opencv',opencv)
#=============指定蓝色值的范围=============
minBlue = np.array([110,50,50])
maxBlue = np.array([130,255,255])
#生成一个二值掩码mask,落在蓝色范围内的像素值为 255,其他为 0。
mask = cv2.inRange(hsv, minBlue, maxBlue)
#对原图做“按位与”，只保留蓝色区域（其余变黑）。
blue = cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('blue',blue)
#=============指定绿色值的范围=============
minGreen = np.array([50,50,50])
maxGreen = np.array([70,255,255])
#确定绿色区域
mask = cv2.inRange(hsv, minGreen, maxGreen)
#通过掩码控制的按位与，锁定绿色区域
green = cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('green',green)
#=============指定红色值的范围=============
minRed = np.array([0,50,50])
maxRed = np.array([30,255,255])
#确定红色区域
mask = cv2.inRange(hsv, minRed, maxRed)
#通过掩码控制的按位与，锁定红色区域
red= cv2.bitwise_and(opencv,opencv, mask= mask)
cv2.imshow('red',red)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 标记肤色

- 可以使用“&”组合2个二值mask

```
import cv2
img=cv2.imread("lesson2.jpg")

# 分别得到三个单通道图像：
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h,s,v=cv2.split(hsv)

# 保留 色相值在 [5,170] 之间的区域。
# 过滤掉极端的红、紫之类的部分。
minHue=5
maxHue=170
hueMask=cv2.inRange(h, minHue, maxHue)

# 保留饱和度在 [25,166] 之间的区域；
# 饱和度太低的区域（灰度、阴影）或太高的区域（过曝）都会被过滤。
minSat=25
maxSat=166
satMask = cv2.inRange(s, minSat, maxSat)

# 用 按位与运算 (&) 得到综合掩膜；
# 只有同时满足色相范围 和 饱和度范围的像素才会保留；
# 结果是一个二值图像（mask）。
mask = hueMask & satMask
roi = cv2.bitwise_and(img,img, mask= mask)
cv2.imshow("img",img)
cv2.imshow("ROI",roi)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 几何变换

## 缩放 resize

- 通过绝对宽高设置

```
import cv2
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
size=(int(cols*0.9),int(rows*0.5))
rst=cv2.resize(img,size)
print("img.shape=",img.shape)
print("rst.shape=",rst.shape)
cv2.imshow("img",img)
cv2.imshow("rst",rst)
cv2.waitKey(0)
```

- 通过比例设置

```
import cv2
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
rst=cv2.resize(img,None,fx=2,fy=0.5)
print("img.shape=",img.shape)
print("rst.shape=",rst.shape)
cv2.imshow("img",img)
cv2.imshow("rst",rst)
cv2.waitKey(0)
```

## 翻转 flip

- 0：上下
- 1：左右
- -1: 上下+左右

```
img=cv2.imread("lena.bmp")
x=cv2.flip(img,0)
y=cv2.flip(img,1)
xy=cv2.flip(img,-1)
cv2.imshow("img",img)
cv2.imshow("x",x)
cv2.imshow("y",y)
cv2.imshow("xy",xy)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 仿射 warpAffine

仿射变换（Affine Transformation），也就是在不破坏平行线关系的前提下，对图像进行平移、旋转、缩放、错切等组合变换。

### 平移

通过float32创建矩阵，指定xy位移

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
height,width=img.shape[:2]
x=50
y=100
M = np.float32([[1, 0, x], [0, 1, y]])
move=cv2.warpAffine(img,M,(width,height))
cv2.imshow("original",img)
cv2.imshow("move",move)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 旋转

使用getRotationMatrix2D创建矩阵，指定旋转中心、角度与缩放

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
height,width=img.shape[:2]
M=cv2.getRotationMatrix2D((width/2,height/2),45,0.6)
rotate=cv2.warpAffine(img,M,(width,height))
cv2.imshow("original",img)
cv2.imshow("rotation",rotate)
cv2.waitKey()
cv2.destroyAllWindows()
```

### 错切

从3个点变道3个点，但要保持对边的平行性

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
rows,cols,ch=img.shape

# 这是原图像上的三个点：
# 左上角 → (0, 0)
# 右上角 → (cols-1, 0)
# 左下角 → (0, rows-1)
# 在图像中选三个不共线的点，用于定义原始三角形区域。
p1=np.float32([[0,0],[cols-1,0],[0,rows-1]])

# 变换后三角形顶点要映射到的新位置。
# 第1个点：移到了稍微下方；
# 第2个点：往左下方倾斜；
# 第3个点：往右上方偏移。
# 通过改变这三个目标点的位置，可以控制图像的旋转、拉伸或倾斜。
p2=np.float32([[0,rows*0.33],[cols*0.85,rows*0.25],[cols*0.15,rows*0.7]])

# 计算仿射变换矩阵
M=cv2.getAffineTransform(p1,p2)

dst=cv2.warpAffine(img,M,(cols,rows))
cv2.imshow("origianl",img)
cv2.imshow("result",dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 透视 warpPerspective

从4个点变到另外4个点，包含仿射的效果

```

import cv2
import numpy as np
img=cv2.imread('demo.bmp')
rows,cols=img.shape[:2]
print(rows,cols)
# src：定义平行四边形的四个点
pts1 = np.float32([[150,50],[400,50],[60,450],[310,450]])
# dst：定义一个矩形
pts2 = np.float32([[50+100,50],[rows-50-100,50],[50,cols-50],[rows-50,cols-50]])
# 计算3×3 透视变换矩阵，进行透视变换
M=cv2.getPerspectiveTransform(pts1,pts2)
dst=cv2.warpPerspective(img,M,(cols,rows))

cv2.imshow("img",img)
cv2.imshow("dst",dst)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 重映射 remap

- 最强的的存在，可以实现上面的所有变换，相当于告诉 OpenCV：“输出图像上第 (i, j) 个像素，要从原图的 (mapx[i,j], mapy[i,j]) 位置取颜色，然后 OpenCV 根据这两个映射表自动完成插值采样和生成新图
- mapx[i,j], mapy[i,j]分别保存每个点各自的x、 y新位置

```
import cv2
import numpy as np
img=cv2.imread("lena.jpg")
rows,cols=img.shape[:2]
mapx = np.zeros(img.shape[:2],np.float32)
mapy = np.zeros(img.shape[:2],np.float32)
for i in range(rows):
    for j in range(cols):
# 复制
#        mapx.itemset((i, j), j)
#        mapy.itemset((i, j), i)
# 上下翻转
#        mapx.itemset((i,j),j)
#        mapy.itemset((i,j),rows-1-i)
# 左右翻转
#        mapx.itemset((i, j), cols - 1 - j)
#        mapy.itemset((i, j), i)
# 上下左右都翻转
#        mapx.itemset((i, j), cols - 1 - j)
#        mapy.itemset((i, j), rows - 1 - i)
# 行列互换（旋转90度的效果）
#        mapx.itemset((i, j), i)
#        mapy.itemset((i, j), j)
# 缩放
        if 0.25 * cols < i < 0.75 * cols and 0.25 * rows < j < 0.75 * rows:
            mapx.itemset((i, j), 2 * (j - cols * 0.25) + 0.5)
            mapy.itemset((i, j), 2 * (i - rows * 0.25) + 0.5)
        else:
            mapx.itemset((i, j), 0)
            mapy.itemset((i, j), 0)
rst=cv2.remap(img,mapx,mapy,cv2.INTER_LINEAR)
cv2.imshow("original",img)
cv2.imshow("result",rst)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 阈值处理

一般要求输入 灰度图像（单通道），而不是彩色图。若直接传入彩色图像，它会对每个通道分别进行阈值处理。

## 全局固定阈值 threshold

所有像素都使用同一个阈值进行二值化。适合光照均匀的图像，若图像光照不均，这种方式常常效果不理想。

- cv2.THRESH_BINARY	像素 >127 → 255；否则 → 0	二值化图，大于阈值→白，否则→黑
- cv2.THRESH_BINARY_INV	像素 >127 → 0；否则 → 255	反转二值图
- cv2.THRESH_TRUNC	像素 >127 → 127；否则保持原值	截断亮度
- cv2.THRESH_TOZERO	像素 >127 → 保持原值；否则 → 0	保留亮的部分
- cv2.THRESH_TOZERO_INV	像素 >127 → 0；否则保持原值	保留暗的部分

```
import cv2
import numpy as np
img=cv2.imread("lena.bmp")
# t：实际使用的阈值（这里等于 127）
t,THRESH_BINARY=cv2.threshold(img,127,255,cv2.THRESH_BINARY)
t,THRESH_BINARY_INV=cv2.threshold(img,127,255,cv2.THRESH_BINARY_INV)
t,THRESH_TRUNC=cv2.threshold(img,127,255,cv2.THRESH_TRUNC)
t,THRESH_TOZERO_INV=cv2.threshold(img,127,255,cv2.THRESH_TOZERO_INV)
t,THRESH_TOZERO=cv2.threshold(img,127,255,cv2.THRESH_TOZERO)
cv2.imshow("img",img)
cv2.imshow("THRESH_BINARY",THRESH_BINARY)
cv2.imshow("THRESH_BINARY_INV",THRESH_BINARY_INV)
cv2.imshow("THRESH_TRUNC",THRESH_TRUNC)
cv2.imshow("THRESH_TOZERO_INV",THRESH_TOZERO_INV)
cv2.imshow("THRESH_TOZERO",THRESH_TOZERO)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自动阈值 Otsu

- Otsu 自动找到“最合适的分界线”，不需要手动设定阈值。(计算图像灰度直方图；尝试不同阈值；找到使类间方差（前景与背景分布差异）最大的那个阈值；自动使用该阈值进行二值化。)

```
import cv2
import numpy as np
img=cv2.imread("tiffany.bmp",0)
t1,thd=cv2.threshold(img,127,255,cv2.THRESH_BINARY)

使用THRESH_OTSU时候第二个参数写成0
t2,otsu=cv2.threshold(img,0,255,cv2.THRESH_BINARY+cv2.THRESH_OTSU)
cv2.imshow("img",img)
cv2.imshow("thd",thd)
cv2.imshow("otus",otsu)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自适应阈值 adaptiveThreshold

- ADAPTIVE_THRESH_MEAN_C 均值自适应，适合光照不均的图像，自动适应亮度变化，计算稍慢
- ADAPTIVE_THRESH_GAUSSIAN_C 高斯自适应，适合含噪图像，平滑效果好，参数需调试

```
img=cv2.imread("computer.jpg",0)
t1,thd=cv2.threshold(img,127,255,cv2.THRESH_BINARY)

末尾2个参数的作用：
邻域块大小（blockSize）：每个像素以其周围 3×3 区域计算局部阈值。应为奇数且大于1。如3、5、7
C常数：从计算出的局部平均（或高斯加权平均）中减去该常数，微调阈值。

athdMEAN=cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_MEAN_C,cv2.THRESH_BINARY,3,5)
athdGAUS=cv2.adaptiveThreshold(img,255,cv2.ADAPTIVE_THRESH_GAUSSIAN_C,cv2.THRESH_BINARY,3,5)
cv2.imshow("img",img)
cv2.imshow("thd",thd)
cv2.imshow("athdMEAN",athdMEAN)
cv2.imshow("athdGAUS",athdGAUS)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 滤波

## 基本概念与卷积核（Convolution Kernel）

- 是图像处理中最常见的操作之一，用于去噪声、平滑图像或增强边缘。用像素邻域的加权结果替代当前像素值。

- 卷积核是一块带有权值的小矩阵，通过在图像上滑动并与像素区域做加权计算，控制图像的模糊、锐化、边缘检测等效果。本质上就是图像处理的运算规则模板。

- 卷积越大、时间越久、更平滑、但越失真

## 种类对比

| 滤波类型                           | OpenCV函数                                              | 原理                  | 主要参数                            | 优点            | 缺点          | 典型用途           |
| ------------------------------ | ----------------------------------------------------- | ------------------- | ------------------------------- | ------------- | ----------- | -------------- |
| **1️⃣ 均值滤波（Mean Filter）**      | `cv2.blur(src, ksize)`                                | 用邻域像素的平均值替代中心像素     | `ksize=(m,n)` 滤波核大小             | 简单快速，能去除随机噪声  | 模糊边缘，细节丢失   | 图像平滑、去随机噪声     |
| **2️⃣ 方框滤波（Box Filter）**       | `cv2.boxFilter(src, ddepth, ksize, normalize)`        | 类似均值滤波，可控制是否归一化     | `normalize=True/False`          | 控制灵活，可实现加权或求和 | 不归一化会导致亮度偏移 | 特殊加权或亮度操作      |
| **3️⃣ 高斯滤波（Gaussian Filter）**  | `cv2.GaussianBlur(src, ksize, sigmaX)`                | 按高斯分布加权平均，中心权重大     | `ksize`, `sigmaX`, `sigmaY`     | 平滑自然，边缘保留较好   | 计算略慢        | 去高斯噪声、边缘检测前预处理 |
| **4️⃣ 中值滤波（Median Filter）**    | `cv2.medianBlur(src, ksize)`                          | 用邻域像素的中间值替代中心像素     | `ksize`（奇数）                     | 去椒盐噪声能力强，保边缘好 | 对高斯噪声效果一般   | 去椒盐噪声          |
| **5️⃣ 双边滤波（Bilateral Filter）** | `cv2.bilateralFilter(src, d, sigmaColor, sigmaSpace)` | 综合考虑空间距离与颜色相似度的加权平均 | `d`, `sigmaColor`, `sigmaSpace` | 平滑同时保留边缘，效果自然 | 计算量大，速度慢    | 人像磨皮、摄影后期平滑    |
| **6️⃣ 自定义卷积滤波（filter2D）**      | `cv2.filter2D(src, ddepth, kernel)`                   | 通用卷积操作，可自定义任意核      | `kernel`（矩阵）                    | 灵活强大，可实现任意滤波  | 需手动设计卷积核    | 锐化、模糊、边缘检测等    |

## 图像效果直观总结

| 滤波类型       | 视觉效果             |
| ---------- | ---------------- |
| 均值滤波       | 整体模糊，边缘变钝        |
| 方框滤波（不归一化） | 图像亮度变高           |
| 高斯滤波       | 平滑自然，边缘略保留       |
| 中值滤波       | 去除黑白点噪声效果最佳      |
| 双边滤波       | 平滑又保留边缘（最自然）     |
| filter2D   | 效果取决于卷积核，可实现多种滤波 |

## 如何选择滤波方法

| 场景            | 推荐滤波方法                |
| ------------- | --------------------- |
| 图像噪声较多，无需保留边缘 | **均值滤波 / 高斯滤波**       |
| 图像有“椒盐噪声”     | **中值滤波**              |
| 想平滑但保留边缘（如人脸） | **双边滤波**              |
| 想实验自定义效果      | **filter2D**          |
| 想控制亮度         | **方框滤波（normalize=0）** |

## 总结一句话

🟦 均值滤波：平均去噪，模糊边缘

🟩 方框滤波：可控制是否归一化

🟧 高斯滤波：平滑柔和，边缘较清晰

🟥 中值滤波：去椒盐噪声的首选

🟪 双边滤波：平滑 + 保边缘 = 最自然

⚙️ filter2D：万能卷积器，任意自定义滤波核

## 均值滤波（Mean Filtering）

- 是线性平滑滤波，用于去除图像中的随机噪声。用矩阵在图像上滑动，将矩阵覆盖的所有像素的平均值作为中心像素的新值。

- 权值全部相等(矩阵元素都相同)

```
o=cv2.imread("lenaNoise.png")
r5=cv2.blur(o,(5,5))
r30=cv2.blur(o,(30,30))
cv2.imshow("original",o)
cv2.imshow("result5",r5)
cv2.imshow("result30",r30)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 方框滤波（box Filter）

- 如果参数 normalize（归一化）=True（默认）结果是求平均值（即均值滤波）。
- 否则是求加总值，不除以像素个数。所以亮度会显著增（最大255全白）

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
# r=cv2.boxFilter(o,-1,(5,5))
# r=cv2.boxFilter(o,-1,(5,5),normalize=0)
r=cv2.boxFilter(o,-1,(2,2),normalize=0) 
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 高斯滤波（Gaussian Blur，高斯平滑）

- 高斯滤波是一种加权的平滑滤波，利用“高斯分布”控制权重，是让离中心越近的像素权重越大，离得越远权重越小。 平滑噪声更有效，又能较好地保留图像边缘信息，图像预处理、边缘检测前降噪
- 参数σX：X方向标准差控制模糊程度
- 参数σY：Y方向标准差，一般设为 0，表示与 X 相同

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.GaussianBlur(o,(5,5),0,0)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 中值滤波（Median Filtering）

- 与均值滤波不同，它不会计算平均值，而是取“排序后居中的那个值”。来代替中心像素的值。
- 能有效去除椒盐噪声（即随机出现的黑白点噪声）、对边缘结构的破坏小，平滑效果自然

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.medianBlur(o,3)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 双边滤波（Bilateral Filter）

- 既能平滑图像、又能保留边缘的“高级滤波算法”。人像磨皮（光滑皮肤但保留眼鼻等边缘）
- 只有“距离近”且“颜色相似”的像素才参与平均，边缘两侧颜色差很大的像素不会互相混合，因此边缘可以被保留下来。
- 参数d：像素的邻域范围；
- 参数sigmaColor：控制“颜色差异”敏感度，颜色差异更容易被忽略（模糊更强）
- 参数sigmaSpace：控制“空间距离”敏感度，更远的像素也参与平均（模糊更广）

```
import cv2
import numpy as np
o=cv2.imread("lenaNoise.png")
r=cv2.bilateralFilter(o,25,100,100)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 卷积滤波（filter2D）

自定义矩阵进行滤波操作

```
import cv2
import numpy as np
o=cv2.imread("lena.bmp")
kernel = np.ones((9,9),np.float32)/81
r = cv2.filter2D(o,-1,kernel)
cv2.imshow("original",o)
cv2.imshow("filter2D",r)
cv2.waitKey()
cv2.destroyAllWindows(
```

# 形态学操作（Morphological Operation）

## 概念、作用

- 使用kernel（即卷积核、可理解为自定义的刷子）对二值图像、灰度图进行遍历，分析像素局部邻域，从而达到去噪、提取边缘、连接或分离目标、纹理增强、目标检测、工业/医学图像处理。

- Kernel有形状（矩形、十字、椭圆）、大小、执行次数的属性，决定了操作的方向性和强度。

## 总结对比

| 操作                   | 原理          | 效果            | 应用              |
| -------------------- | ----------- | ------------- | --------------- |
| **腐蚀 (Erosion)**     | 白色区域收缩，前景缩小 | 去掉小白噪点，分离物体   | 噪声去除、物体分离       |
| **膨胀 (Dilation)**    | 白色区域扩张，前景增大 | 填补小黑洞，连接白色物体  | 填洞、连接目标         |
| **开运算 (Opening)**    | 先腐蚀再膨胀      | 去除小白噪声，平滑边缘   | 去噪、分离小物体        |
| **闭运算 (Closing)**    | 先膨胀再腐蚀      | 填补小黑洞，平滑边界    | 填洞、连接断裂目标       |
| **形态学梯度 (Gradient)** | 膨胀减去腐蚀      | 提取物体边缘，显示轮廓线  | 边缘检测、轮廓分析       |
| **顶帽变换 (Top-hat)**   | 原图减去开运算     | 提取小亮点，增强局部亮特征 | 亮点检测、高光增强、纹理分析  |
| **黑帽变换 (Black-hat)** | 闭运算减去原图     | 提取小暗点，强化局部阴影  | 暗特征检测、纹理增强、缺陷检测 |



## 腐蚀（Erosion）

- 目标“让白色（前景）区域变小，黑色（背景）区域扩大。”
- 首先定义kernel（是矩阵）用于设置腐蚀的“力度”和“形状（对边缘形态影响不同）”，然后执行erode函数进行腐蚀，iterations腐蚀的重复次数

```
import cv2
import numpy as np
o=cv2.imread("erode.bmp",cv2.IMREAD_UNCHANGED)
kernel = np.ones((9,9),np.uint8)
erosion = cv2.erode(o,kernel,iterations =5)
cv2.imshow("orriginal",o)
cv2.imshow("erosion",erosion)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 膨胀（Dilation）

会让白色前景扩大，用于填补空隙、连接断裂、强化形状，与腐蚀正好相反

```
o=cv2.imread("dilation.bmp",cv2.IMREAD_UNCHANGED)
kernel = np.ones((5,5),np.uint8)
dilation = cv2.dilate(o,kernel,iterations = 9)
cv2.imshow("original",o)
cv2.imshow("dilation", dilation)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 开运算（Opening）

开运算是先腐蚀再膨胀，主要用于去除小白噪声、平滑物体边缘，而不会明显改变主体形状。

```
img1=cv2.imread("opening.bmp")
img2=cv2.imread("opening2.bmp")
k=np.ones((10,10),np.uint8)
r1=cv2.morphologyEx(img1,cv2.MORPH_OPEN,k)
r2=cv2.morphologyEx(img2,cv2.MORPH_OPEN,k)
cv2.imshow("img1",img1)
cv2.imshow("result1",r1)
cv2.imshow("img2",img2)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 闭运算（Closing）

闭运算是先膨胀再腐蚀，主要用于填补小黑洞、连接相邻白区域、平滑边界

```
img1=cv2.imread("closing.bmp")
img2=cv2.imread("closing2.bmp")
k=np.ones((10,10),np.uint8)
r1=cv2.morphologyEx(img1,cv2.MORPH_CLOSE,k,iterations=3)
r2=cv2.morphologyEx(img2,cv2.MORPH_CLOSE,k,iterations=3)
cv2.imshow("img1",img1)
cv2.imshow("result1",r1)
cv2.imshow("img2",img2)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 形态学梯度（Morphological Gradient）

即膨胀减去腐蚀，它的结果是物体的边缘轮廓，常用于边缘检测与目标分割。

```
o=cv2.imread("gradient.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r=cv2.morphologyEx(o,cv2.MORPH_GRADIENT,k)
cv2.imshow("original",o)
cv2.imshow("result",r)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 顶帽（Top-hat）

原图减去开运算结果，用于提取小而亮的区域（噪声）、增强局部亮细节。

```
o1=cv2.imread("tophat.bmp",cv2.IMREAD_UNCHANGED)
o2=cv2.imread("lena.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r1=cv2.morphologyEx(o1,cv2.MORPH_TOPHAT,k)
r2=cv2.morphologyEx(o2,cv2.MORPH_TOPHAT,k)
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 黑帽（Black-hat）

是闭运算减去原图，用于提取小暗区域、增强局部阴影细节。

```
o1=cv2.imread("blackhat.bmp",cv2.IMREAD_UNCHANGED)
o2=cv2.imread("lena.bmp",cv2.IMREAD_UNCHANGED)
k=np.ones((5,5),np.uint8)
r1=cv2.morphologyEx(o1,cv2.MORPH_BLACKHAT,k)
r2=cv2.morphologyEx(o2,cv2.MORPH_BLACKHAT,k)
cv2.imshow("original1",o1)
cv2.imshow("original2",o2)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

## 自定义核函数

可使用3种形状进行自定义那个核刷子的形状，用于影响刷出来的外观

```
o=cv2.imread("kernel.bmp",cv2.IMREAD_UNCHANGED)
kernel1 = cv2.getStructuringElement(cv2.MORPH_RECT, (59,59))
kernel2 = cv2.getStructuringElement(cv2.MORPH_CROSS,  (59,59))
kernel3 = cv2.getStructuringElement(cv2.MORPH_ELLIPSE,  (59,59))
dst1 = cv2.dilate(o,kernel1)
dst2 = cv2.dilate(o,kernel2)
dst3 = cv2.dilate(o,kernel3)
cv2.imshow("orriginal",o)
cv2.imshow("dst1",dst1)
cv2.imshow("dst2",dst2)
cv2.imshow("dst3",dst3)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 图像梯度计算

## 概念作用

- 求每个像素的灰度变化幅度和方向（如果某个区域灰度变化大即梯度大越亮）
- 是提取边缘和局部结构的重要工具。

## 对比总结

| 算子            | 阶数 | 方向      | 核大小         | 特点               | 优点          | 缺点                  | 典型用途           |
| ------------- | -- | ------- | ----------- | ---------------- | ----------- | ------------------- | -------------- |
| **Sobel**     | 一阶 | X/Y 可分开 | 可调 (3,5,7…) | 计算一阶梯度，强调水平/竖直边缘 | 简单，通用       | 对弱边缘和细节敏感度一般        | 边缘检测、特征提取、图像分割 |
| **Scharr**    | 一阶 | X/Y 可分开 | 固定 3x3，优化权重 | Sobel 升级版，更锐利    | 对细节和弱边缘敏感   | 只能单方向，不支持 dx=1,dy=1 | 边缘检测、细节增强      |
| **Laplacian** | 二阶 | 全方向     | 3x3 或 5x5   | 计算二阶导数，全方向边缘一次提取 | 能一次提取所有方向边缘 | 对噪声敏感               | 边缘检测、图像锐化      |

- Sobel：适合一般边缘检测，可调核大小，简单易用。
- Scharr：对细节边缘更敏感，适合高精度边缘检测。
- Sobel与Scharr可以X/Y 梯度先分别求，再加权合成 → 获得完整边缘图
- Laplacian：一次提取全方向边缘，但噪声敏感，常结合平滑（如高斯模糊）使用。可单独用于全方向边缘检测或锐化

## Sobel

- Sobel 算子 = 边缘检测基础工具
- dx/dy 决定梯度方向 → 决定边缘方向
- addWeighted 合并 → 得到全局边缘
- CV_64F + convertScaleAbs → 保证梯度计算准确且可显示
- ksize=3，下面案例未使用，用于设置核大小3x3

```
# 得到竖线边缘信息，x=1,y=0,求x方向导数
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelx = cv2.Sobel(o,cv2.CV_64F,1,0)
sobelx = cv2.convertScaleAbs(sobelx)   # 转回uint8
cv2.imshow("original",o)
cv2.imshow("x",sobelx)
cv2.waitKey()
cv2.destroyAllWindows()

# 得到横线边缘信息,dx=0, dy=1,求 y 方向导数
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobely = cv2.Sobel(o,cv2.CV_64F,0,1)
sobely = cv2.convertScaleAbs(sobely)
cv2.imshow("original",o)
cv2.imshow("y",sobely)
cv2.waitKey()
cv2.destroyAllWindows()


# 得到交叉点信息, x=1,y=1,同时对x和y求导（二阶混合导数，不是简单的 x+y，非下面案例的加权效果）
# 仅角点或斜交区域亮，点状、不连续，线条不明显
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelxy=cv2.Sobel(o,cv2.CV_64F,1,1)
sobelxy=cv2.convertScaleAbs(sobelxy)
cv2.imshow("original",o)
cv2.imshow("xy",sobelxy)
cv2.waitKey()
cv2.destroyAllWindows()

# X+Y分别计算再addWeighted，水平和竖直边缘都保留，连续完整的边缘线
# 0.5权重保证 x、y 贡献相等,得到综合边缘图
o = cv2.imread('sobel4.bmp',cv2.IMREAD_GRAYSCALE)
sobelx = cv2.Sobel(o,cv2.CV_64F,1,0)
sobely = cv2.Sobel(o,cv2.CV_64F,0,1)
sobelx = cv2.convertScaleAbs(sobelx)   # 转回uint8
sobely = cv2.convertScaleAbs(sobely)
sobelxy =  cv2.addWeighted(sobelx,0.5,sobely,0.5,0)
cv2.imshow("original",o)
cv2.imshow("xy",sobelxy)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Scharr

- Scharr 是 Sobel 的升级版，更精确地计算图像梯度，尤其在边缘较明显或细节复杂时比 Sobel 更敏感


```
import cv2
import numpy as np

# X 方向梯度,得到竖线
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrx = cv2.Scharr(o,cv2.CV_64F,1,0)
scharrx = cv2.convertScaleAbs(scharrx)   # 转回uint8
cv2.imshow("original",o)
cv2.imshow("x",scharrx)
cv2.waitKey()
cv2.destroyAllWindows()

# Y 方向梯度,得到横线
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharry = cv2.Scharr(o,cv2.CV_64F,0,1)
scharry = cv2.convertScaleAbs(scharry)
cv2.imshow("original",o)
cv2.imshow("y",scharry)
cv2.waitKey()
cv2.destroyAllWindows()

# X、Y 加权融合，得到综合边缘图
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrx = cv2.Scharr(o,cv2.CV_64F,1,0)
scharry = cv2.Scharr(o,cv2.CV_64F,0,1)
scharrx = cv2.convertScaleAbs(scharrx)   # 转回uint8
scharry = cv2.convertScaleAbs(scharry)
scharrxy =  cv2.addWeighted(scharrx,0.5,scharry,0.5,0)
cv2.imshow("original",o)
cv2.imshow("xy",scharrxy)
cv2.waitKey()
cv2.destroyAllWindows()

# Scharr 不允许 dx=1,dy=1，因为它是专门优化单方向一阶导数的算子。想要综合边缘，必须 X/Y 分开计算再合并。此处会运行出错
o = cv2.imread('scharr.bmp',cv2.IMREAD_GRAYSCALE)
scharrxy11=cv2.Scharr(o,cv2.CV_64F,1,1)
cv2.imshow("original",o)
cv2.imshow("xy11",scharrxy11)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Laplacian

Laplacian 是二阶导数算子，直接检测全方向边缘，常用于边缘检测和图像锐化，但噪声敏感，需要结合平滑处理。

```
o = cv2.imread('Laplacian.bmp',cv2.IMREAD_GRAYSCALE)
Laplacian = cv2.Laplacian(o,cv2.CV_64F)
Laplacian = cv2.convertScaleAbs(Laplacian)
cv2.imshow("original",o)
cv2.imshow("Laplacian",Laplacian)
cv2.waitKey()
cv2.destroyAllWindows()
```

# Canny 边缘检测

是一个经典多阶段边缘检测算法，通过高斯滤波去噪平滑、用 Sobel 或 Scharr计算梯度、非极大值抑制和双阈值连接，能在噪声环境中提取精确、连续的全方向边缘（轮廓、形状、纹理）。

- 双阈值 + 边缘连接 的机制：
- threshold1（低阈值）：弱边缘阈值，梯度值低于这个值的像素被认为不是边缘，直接丢弃
- threshold2（高阈值）：强边缘阈值，梯度值高于这个值的像素被认为一定是边缘
- 梯度值在低阈值和高阈值之间：被认为是“弱边缘”，仅保留与强边缘相连部分
- threshold1 决定弱边缘起点，threshold2 决定强边缘，双阈值 + 边缘连接让 Canny 得到干净、连续的边缘。

```
o=cv2.imread("lena.bmp",cv2.IMREAD_GRAYSCALE)
r1=cv2.Canny(o,128,200)
r2=cv2.Canny(o,32,128)
cv2.imshow("original",o)
cv2.imshow("result1",r1)
cv2.imshow("result2",r2)
cv2.waitKey()
cv2.destroyAllWindows()
```

# 金字塔操作（Pyramid）

## 高频、低频

- 图像可以看成是不同频率成分的叠加：
- 高频：图像中快速变化的部分（边缘、细节、纹理）
- 低频：平滑缓慢变化的部分（大块颜色或光照、轮廓）
- 高斯金字塔保留低频，Laplace金字塔提取高频。

| 图像成分 | 高频 / 低频 |
| ---- | ------- |
| 边缘   | 高频      |
| 纹理   | 高频      |
| 颜色渐变 | 低频      |
| 光照背景 | 低频      |
| 噪声   | 高频      |

## 高斯金字塔 （Gaussian Pyramid）

- 是一种多分辨率图像表示方法，核心就是不断下采样和模糊
- 图像每向上一层，分辨率宽高各减半，同时图像会先进行高斯平滑（去掉高频噪声），保留低频

## pyrUp、pyrDown（上下采样）

- pyrDown：下采样，尺寸减半，同时经过高斯模糊（去除高频，保留低频）
- pyrUp：上采样，尺寸倍增，依然模糊

```
import cv2
import numpy as np
o=cv2.imread("lena.bmp")
r1=cv2.pyrDown(o)
r2=cv2.pyrDown(r1)
r3=cv2.pyrDown(r2)
print("o.shape=",o.shape)
print("r1.shape=",r1.shape)
print("r2.shape=",r2.shape)
print("r3.shape=",r3.shape)
cv2.imshow("original",o)
cv2.imshow("r1",r1)
cv2.imshow("r2",r2)
cv2.imshow("r3",r3)
cv2.waitKey()
cv2.destroyAllWindows()

o=cv2.imread("lenas.bmp")
r1=cv2.pyrUp(o)
r2=cv2.pyrUp(r1)
r3=cv2.pyrUp(r2)
print("o.shape=",o.shape)
print("r1.shape=",r1.shape)
print("r2.shape=",r2.shape)
print("r3.shape=",r3.shape)
cv2.imshow("original",o)
cv2.imshow("r1",r1)
cv2.imshow("r2",r2)
cv2.imshow("r3",r3)
cv2.waitKey()
cv2.destroyAllWindows()
```

## Laplace 金字塔

- 是多分辨率图像表示方法，在高斯金字塔的基础上，要保留每层的高频细节，用于无损恢复
- 原图减去低频的模糊图，剩下的就是清晰的边缘和纹理（高频部分）
- 流程：原图 → 下采样 → 上采样 → 差值 = 高频图

```
O = cv2.imread("lena.bmp")       # 原图
G0 = O                           # 高斯金字塔第0层
G1 = cv2.pyrDown(G0)             # 下采样，得到低频信息
L0 = O - cv2.pyrUp(G1)           # 先上采样恢复尺寸，原图-低频=高频细节，Laplace 金字塔的核心操作
RO = L0 + cv2.pyrUp(G1)          # 通过 Laplace 重建原图
```

```
O=cv2.imread("lena.bmp")
#=================生成高斯金字塔======================
G0=O
G1=cv2.pyrDown(G0)
G2=cv2.pyrDown(G1)
G3=cv2.pyrDown(G2)
#===============生成拉普拉斯金字塔====================
L0=G0-cv2.pyrUp(G1) #拉普拉斯金字塔第0层
L1=G1-cv2.pyrUp(G2) #拉普拉斯金字塔第1层
L2=G2-cv2.pyrUp(G3) #拉普拉斯金字塔第2层
#=================复原G0======================
RG0=L0+cv2.pyrUp(G1)  #通过拉普拉斯图像复原的原始图像G0
print("G0.shape=",G0.shape)
print("RG0.shape=",RG0.shape)
result=RG0-G0  #将RG0和G0做减法
#计算result的绝对值，避免求和时负负为正3+(-3)=0
result=abs(result)  
#计算result所有元素的和
print("原始图像G0与恢复图像RG0差值的绝对值和：",np.sum(result))   
#=================复原G1======================
RG1=L1+cv2.pyrUp(G2) #通过拉普拉斯图像复原G1
print("G1.shape=",G1.shape)
print("RG1.shape=",RG1.shape)
result=RG1-G1  #将o和ro做减法
print("原始图像G1与恢复图像RG1差值的绝对值和：",np.sum(abs(result)))
#=================复原G2======================
RG2=L2+cv2.pyrUp(G3) #通过拉普拉斯图像复原G2
print("G2.shape=",G2.shape)
print("RG2.shape=",RG2.shape)
result=RG2-G2  #将o和ro做减法
print("原始图像G2与恢复图像RG2差值的绝对值和：",np.sum(abs(result)))
```